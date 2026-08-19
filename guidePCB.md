# Création d'un PCB

Les sections sont placées dans l'ordre dans lequel elles devraient être faites. Ne changez pas trop les réglages par défaut de KiCad : les valeurs proposées sont généralement adaptées.

> **À garder en tête**
> - Pensez à la fabrication, à l'assemblage et au débogage dès le début.
> - Limitez les changements de dernière minute : ils compliquent la validation du PCB.

## 1. Contour (*Edge Cuts*)

Il est recommandé de faire le contour sur Onshape afin d'obtenir une meilleure forme, plus simple à mettre à jour.

- N'oubliez pas d'inclure les trous de vis et les autres méthodes de fixation. L'équipe structure vous en remerciera.
- Limitez la taille à **10 cm × 10 cm**, car les coûts augmentent rapidement au-delà de cette dimension.

## 2. Placement des composants

Suivez cet ordre de priorité :

1. Placez les connecteurs et les éléments accessibles à l'utilisateur (LED, boutons, etc.) afin qu'ils soient facilement accessibles et logiquement disposés.
2. Placez les composants importants ou ayant des exigences complexes. Par exemple, un ESP32 est connecté à plusieurs éléments : une position centrale est donc utile. Un IMU doit être éloigné des sources électromagnétiques.
3. Placez les composants dont le positionnement est critique. Les condensateurs de découplage doivent notamment être proches des puces qu'ils servent.
4. Si le PCB présente un enjeu thermique, éloignez les composants qui chauffent. Pensez également à l'espace nécessaire pour souder le PCB.

> **Vérification mécanique**
> Pensez à la hauteur des composants lors de leur placement et vérifiez qu'ils ne gênent pas l'intégration finale.

## 3. Tracé des pistes

- Essayez de rester sur **deux couches** si possible.
- Tracez les pistes en priorisant les pistes différentielles et celles qui doivent être particulièrement courtes. Pour les pistes différentielles, limitez l'écart entre les deux pistes à **1 mm maximum**.

<p align="center"><img width="710" height="509" alt="Exemple de tracé de pistes différentielles" src="https://github.com/user-attachments/assets/c21afacc-8541-4768-b4fc-19b742e0c18a" /></p>

Tracez ensuite les pistes de puissance. Utilisez l'outil de calcul de KiCad pour connaître la largeur requise. Limitez l'augmentation de température (*temperature rise*) à **10 °C** et gardez l'épaisseur de cuivre à **1 oz/ft²**.

Si vous avez l'espace nécessaire, créez un plan de masse (*ground plane*). Il permet d'éviter les boucles de masse et de réduire les perturbations ainsi que les différences de tension sur la masse. Lorsque vous créez un plan, utilisez des connexions thermiques (*thermal relief*) : le PCB sera beaucoup plus facile à souder.

> **Règle absolue**
> **Ne faites jamais d'angles de 90° dans les pistes.**

Placez plusieurs vias lorsqu'un courant important est prévu afin de limiter les pertes causées par leur résistance.

<p align="center"><img width="292" height="205" alt="Exemple de vias multiples" src="https://github.com/user-attachments/assets/50810d25-b1e0-491b-a87b-3f65043b3d1f" /></p>

N'ajoutez pas de vias sur un footprint, sauf s'il est impossible de faire autrement. C'est une mauvaise pratique.

<p align="center"><img width="728" height="710" alt="Exemple de vias à éviter sur un footprint" src="https://github.com/user-attachments/assets/78b9c20c-c039-4921-bdb1-d3a9c0cb3500" /></p>

Ajoutez des points de test lorsque c'est possible pour faciliter le débogage. Les personnes qui devront régler les problèmes vous en remercieront.

## 4. Sérigraphie (*Silkscreen*)

Ajoutez des informations pertinentes sur le PCB. Le dessus doit rester professionnel; pour le dessous, vous pouvez vous permettre un peu plus de fantaisie.

### Informations à ajouter

- Numéro des petits composants ou méthode d'identification (nom du composant, utilité). Certains numéros peuvent être omis en cas de manque d'espace évident et s'il n'existe aucune autre méthode d'identification.
- Marquages importants, par exemple le sens d'un IMU.
- Symbole Biogenius, ainsi que ceux de Robotique UdeS si l'espace le permet.
- Nom des concepteurs et des validateurs. Vous faites du bon travail, soyez-en fiers!

<p align="center"><img width="917" height="780" alt="Exemple de sérigraphie" src="https://github.com/user-attachments/assets/a19bc6eb-76de-4aef-b698-c02d419a6e27" /></p>

### Avertissements tolérés

- Sérigraphies qui se superposent.
- Footprints manquants, causés par une modification de la sérigraphie.
- Footprints qui ne correspondent plus à ceux de la bibliothèque, à la suite d'une modification de la sérigraphie.
