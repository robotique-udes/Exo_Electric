# BMS — Battery Management System

> Carte de gestion, de protection et de distribution de l'alimentation de l'exosquelette.

Le BMS est responsable de la gestion, de la protection et de la distribution de l'énergie du système. Il supervise les deux batteries, gère les séquences de commutation, protège les circuits contre les défauts et alimente les sous-systèmes critiques, notamment les rails **5 V** et **48 V**.

## Vue d'ensemble

Le BMS doit notamment :

- gérer l'arrêt d'urgence de l'exosquelette ;
- protéger chaque batterie individuellement ;
- sélectionner automatiquement ou manuellement la source d'alimentation active ;
- distribuer les tensions **5 V** et **48 V** aux sous-systèmes ;
- communiquer l'état du système au module principal (**MoBo**) ;
- sécuriser les circuits vis-à-vis des courts-circuits, de la polarité inversée et des surintensités.

## Objectifs fonctionnels

- gérer l'arrêt d'urgence de l'exosquelette ;
- intégrer des fusibles de sécurité : un par batterie, un par jambe et un pour le circuit 5 V ;
- inclure une protection contre la polarité inversée (back-EMF / courant inverse) ;
- mettre en place une stratégie de handshake ou équivalent pour éviter le court-circuit entre les batteries ;
- ajouter des LED indiquant l'état d'alimentation après les fusibles pour vérifier rapidement leur état ;
- gérer un courant continu de **4 A à 48 V** ;
- fournir **2,5 A à 5 V continu** pour les sous-systèmes (BIMU, MoBo et alimentation du BMS) ;
- fournir un indicateur de pourcentage de batterie restante ;
- intégrer une connexion de batterie de type **XT ?** ;
- prévoir une connexion Ethernet pour la distribution 5 V et le bus CAN ;
- intégrer une connexion **XT30** par jambe ;
- permettre le basculement automatique entre les batteries ;
- inclure des indicateurs visuels d'état autour des batteries.

# Conception

- Seuls les ESP32 du **MoBo** et du **BMS** disposent d'une connectivité sans fil. Les deux sont inclus dans le budget de puissance, mais seul le module sans fil du MoBo sera utilisé en fonctionnement normal.
- La consommation **MISC** correspond à une estimation des pertes du PCB, des pertes de conversion, des composants annexes et des LED.
- **LED_BMS** représente la puissance disponible pour des LED décoratives ou d'usage non critique. Elle ne fait pas partie du total de puissance de base et pourra être calculée une fois les besoins principaux fixés.

### Budget de puissance 5 V

Les estimations ci-dessous supposent un rail **3,3 V** et une marge de conversion de **20 %**.

| Charge | Hypothèse | Puissance estimée |
| --- | --- | ---: |
| MoBo | `(300 mA + 100 mA MISC) × 3,3 V` | **1,32 W** |
| BIMU | `(35 mA + 100 mA MISC) × 3,3 V x 5` | **2,25 W** |
| BMS | `(300 mA + 100 mA MISC) × 3,3 V` | **1,32 W** + `LED_BMS` |

Un rendement de **80 %** est retenu pour le convertisseur principal vers **5 V**. Cette hypothèse est volontairement prudente, car la tension de batterie peut varier significativement et le convertisseur doit couvrir une large plage d'entrée.

### Estimation des besoins du circuit 5 V

```text
P nécessaire = (1,32 W + 2,25 W + 1,32 W) / 0,80
            = 6,12 W

I sous 5 V = 6,12 W / 5 V
           = 1,224 A
```

Un convertisseur **5 V / 1.5 A** couvrirait donc l'estimation actuelle. Cependant, le câble Ethernet envisagé, avec des conducteurs **23 AWG**, est généralement estimé à environ **0,7 A par conducteur**. Avec trois conducteurs 5 V et trois conducteurs GND, la capacité théorique atteint :

```text
0,7 A × 3 = 2,1 A
```

Par prudence et pour garder une marge d'évolution, le convertisseur cible sera choisi dans une plage de **2 à 4 A**, selon les besoins confirmés et les composants disponibles. Un fusible de **2 A** en amont du câble est envisagé.

### Estimation des pertes de la diode de contrôle

Le courant traversant la diode est estimé dans le pire cas : **4 A sous 5 V**.

```text
I diode = 4 A × 5 V / 0,8 / 60
        = 0,42 A
```

En appliquant la formule donnée dans la documentation :

```text
P = 0,54 × IF + 0,08 × IF^2
P = 0,54 × 0,42 A + 0,08 × (0,42 A)^2
P = 0,24 W
```

Cette valeur correspond au pire cas et semble acceptable à ce stade. La température de fonctionnement devra toutefois être vérifiée avec le boîtier et le PCB définitifs.

---

## Sécurité et protection des fusibles

### Estimation du courant requis pour le rail 48 V

Le système est composé de :

- 4 moteurs, chacun consommant jusqu'à **0,8 A sous 48 V** ;
- une charge auxiliaire (contrôle) de **1 A sous 5 V**.

#### Courant nominal des moteurs

```text
I moteurs = 4 × 0,8 A
          = 3,2 A
```

#### Courant équivalent de la charge 5 V

En considérant un rendement du convertisseur de **80 %** :

```text
I 5V = (0,8 × 48 V) / (5 V × 1 A)
     = 0,13 A
```

#### Courant total

```text
I total = 3,2 A + 0,13 A
        = 3,33 A
```

#### Marge de sécurité

Avec une marge de sécurité de **25 %** :

```text
I fusible = 3,33 A × 1,25
          ≈ 4,17 A
```

Un fusible de **4 A** serait une valeur limite. Il serait judicieux d'envisager un fusible de **5 A** pour conserver une marge de fonctionnement plus confortable.

### Courant de démarrage

Le fusible doit supporter les pointes de courant produites lors du démarrage des moteurs sans ouvrir prématurément.

Le courant réel pendant le démarrage est :

```text
I start = I normal + I spike
```

Pour un courant de démarrage approximativement constant :

```text
I²t = I start² × t start
```

Une marge de sécurité peut ensuite être appliquée :

```text
I²t requis = I²t × M
```

où **M** représente la marge de sécurité.

### Calcul de la valeur de fusible pour un type slow blow

Pour calculer la valeur de fusible adaptée à une protection de type **slow blow**, il faut utiliser la formule suivante :

```text
I²t = I peak² × t pulse
```

et déterminer la valeur requise pour la fusible en fonction du profil de courant.

Un exemple de référence compatible avec ce type de besoins est disponible ici :

https://www.littelfuse.com/products/fuses-overcurrent-protection/fuses/axial-radial-thru-hole-fuses#Zi1zZXJpZXM9MzcyJm5mLW1heGltdW1fYWNfdm9sdGFnZV92X2RlY2ltYWw9NzAuLi4xMDAwJm5mLW5vbWluYWxfbWVsdGluZ19pX3NxdWFyZWRfdF9hX3NxdWFyZWRfcGVyX3NlY29uZF9kZWNpbWFsPTE2Li4uMzImY3E9KCU0MGxldmVsdGhyZWVjYXRlZ29yeSUzRCUzRCUyMkF4aWFsJTIwUmFkaWFsJTIwVGhydSUyMEhvbGUlMjBGdXNlcyUyMiklMjAoJTQwbGV2ZWxudW1iZXIlM0QlM0Q3KSUyMCglNDBsZXZlbHR3b2NhdGVnb3J5JTNEJTNEJTIyRnVzZXMlMjIpJTIwKCU0MGxldmVsb25lY2F0ZWdvcnklM0QlM0QlMjJGdXNlcyUyMCUyNiUyME92ZXJjdXJyZW50JTIwUHJvdGVjdGlvbiUyMik=

Mini fuse verre
https://www.digikey.ca/en/products/detail/littelfuse-inc/0225002-MXP/777781


https://www.digikey.ca/en/products/filter/fuses/139?s=N4IgjCBcoGwJxVAYygMwIYBsDOBTANCAPZQDaIAzHAKw0UgC6hADgC5QgDKrATgJYA7AOYgAvoTBwAHAmggUkDDgLEyIAAyNxIAExgALPsQg2HAKoC%2BrAPKoAsrnTYArj1whCzjgDUPIALaCHPpSfv7oAB4cBpraALQ6xgq8ziokkOTUWtqJGSCoznhaQA

## Choix mosfet
La priorité est de minimisé le RDS on pour limité les pertes durant l'utilisation. Il faut aussi gardé 20V de marge sur l'utilisation. Pour finir il faut gardé un Gate charge raisonnable pour limité le temps de transition des mosfet:

Premier choix 80V(31mO, 45nC)
https://www.digikey.ca/en/products/detail/vishay-siliconix/SQS181ELNW-T1-GE3/20512189

Deuxième choix 80V(17mO, 93nC)
https://www.digikey.ca/en/products/detail/mcc-micro-commercial-components/MCAC017P08Y-TP/25965041

Premier choix 100V(30mO, 68nC)
https://www.digikey.ca/en/products/detail/vishay-siliconix/SQJ211ELP-T1-GE3/13540573

Deuxième choix 100V(31mO, 73nC)
https://www.digikey.ca/en/products/detail/goford-semiconductor/GT250P10T/19524544

## calcul led 

Consommation maximum de 11W/m pour les bandes LEDS https://www.amazon.ca/BTF-LIGHTING-Similar-Individually-Addressable-Lighting/dp/B0F62XVXNS/ref=ast_sto_dp_puis?th=1
Donc on parle de 1.1W/m ou 0.22A

Mais une consommation normal serait plus 30% à 40% voir moins(le but est de les voir, mais sans plus), donc on parle de 0.44W/m ou 0.088A. 
---

## Points à confirmer avant validation finale

- référence exacte des batteries, tension minimale et tension maximale ;
- type de connecteur batterie (**XT ?**) et courant admissible réel ;
- courant de démarrage et courant continu de chaque jambe ;
- méthode de mesure de l'état de charge et précision attendue ;   comptage de columbs
- protocole de handshake pour la sélection de batterie et comportement en cas de défaut ;  Utilisation de 3 lectures de tensions
- validation thermique du convertisseur 5 V, des MOSFET et des fusibles ;  Probablement Négligeable

Faire circuit led pour support batterie

## Résumé

Le BMS est un élément central du système d'alimentation. Il doit offrir une protection robuste, une gestion fiable de la source d'énergie, un basculement entre batteries sans court-circuit, ainsi qu'une alimentation stable de la logique de contrôle et des sous-systèmes. Les estimations actuelles indiquent que le rail 5 V doit être dimensionné pour un convertisseur de l'ordre de **2 à 4 A**, tandis que la protection du rail 48 V doit être étudiée avec une marge suffisante pour supporter les pointes de démarrage des moteurs.
