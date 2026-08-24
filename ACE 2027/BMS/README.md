# BMS

Carte de gestion et de distribution de l'alimentation de l'exosquelette.

Le BMS doit gérer l'arrêt d'urgence, la protection des batteries, la sélection entre deux batteries et la distribution des rails **5 V** et **48 V**. Il transmet également l'état du système au MoBo.

> **État du projet :** conception préliminaire  \
> Plusieurs valeurs et choix de composants restent à valider avec les batteries et les charges réelles.

## Objectifs

* Géré l'arrêt d'urgence de l'exosquelette
* Intégré des fuses de sécurités(une par batterie, une par jambe, une pour le circuit 5V)
* Avoir un circuit contre la reverse polarity(back current EMF)
* Une stratégie de Handshake ou autre pour ne pas shorté les batteries ensembles(mosfet de controle)
* LED pour confirmé que le circuit est alimenté(après les fuses pour connaitre l'état des fuse en même temps)
* Pouvoir géré 4A à 48V continue
* Pouvoir delivré 2.5A à 5V continue (5*200mA par BIMU et 400 mA pour le MOBO, le reste est pour le BMS) 
* Pouvoir donner le pourcentage de batterie restante
* Avoir une connection XT ??? par batterie
* Avoir une conenction Ethernet pour la connection 5V et CAN
* Avoir une connection XT30 par jambe
* Pouvoir automatiquement changé de batterie
* Avoir des lumières d'état autour des batterie


## Conception


- Seuls les ESP32 du **MoBo** et du **BMS** disposent d'une connectivité sans fil. Les deux sont inclus dans le budget de puissance, mais seul le sans-fil du MoBo sera utilisé en fonctionnement normal. La consommation **MISC** représente une estimation des pertes du PCB, des pertes de conversion, des petits composants et des LED. **LED_BMS** correspond à la puissance disponible pour d'éventuelles LED décoratives. Elle ne fait pas partie du total et sera calculée lorsque les autres besoins seront figés.

### Budget de puissance 5 V

Les estimations ci-dessous utilisent le rail 3,3 V et une marge de conversion de 20 %.

| Charge | Hypothèse | Puissance estimée |
| --- | --- | ---: |
| MoBo | `(300 mA + 100 mA MISC) x 3,3 V` | **1,32 W** |
| BIMU | `(35 mA + 100 mA MISC) x 3,3 V` | **0,45 W** |
| BMS | `(300 mA + 100 mA MISC) x 3,3 V` | **1,32 W** + `LED_BMS` |

Un rendement de **80 %** est retenu pour le convertisseur principal vers 5 V. Cette hypothèse reste volontairement prudente, car la tension de batterie peut varier fortement et le convertisseur doit couvrir une grande plage de tension d'entrée.

### Estimation

```text
P nécessaire = (1,32 W + 0,45 W + 1,32 W) / 0,80
			 = 3,87 W

I sous 5 V  = 3,87 W / 5 V
			 = 0,774 A
```

Un convertisseur **5 V / 1 A** couvrirait donc l'estimation actuelle. Cependant, le câble Ethernet envisagé avec des conducteurs de **23 AWG** est donné pour environ **0,7 A par conducteur**. Avec trois conducteurs 5 V et trois conducteurs GND, la capacité théorique atteindrait `0,7 A x 3 = 2,1 A`.

Par prudence et pour conserver une marge d'évolution, le convertisseur cible sera choisi dans une plage de **2 à 4 A**, selon les besoins confirmés et les composants disponibles. Un fusible de **2 A** en amont du câble est envisagé.

## Points à confirmer

- Référence exacte des batteries, tension minimale et tension maximale.
- Type de connecteur batterie (`XT ?`) et courant admissible réel.
- Courant de démarrage et courant continu de chaque jambe.
- Méthode de mesure de l'état de charge et précision attendue.
- Protocole du handshake de sélection de batterie et comportement en cas de défaut.
- Validation thermique du convertisseur 5 V, des MOSFET et des fusibles.
- Courant admissible du câble Ethernet utilisé pour le 5 V sur la longueur finale.