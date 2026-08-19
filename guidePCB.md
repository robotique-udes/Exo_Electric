Création d'un PCB

Les sections sont placées dans l'ordre auquel elles devraient être faites. Ne changez pas trop les réglages par défaut de Kicad, les valeurs sont bien.

## Contour(Edge cut)
Il est recommandé de faire le contour sur Onshape pour pouvoir avoir une meilleure forme et plus simple à mettre à jour. 
Oubliez pas d'inclure des trou pour des vis ou d'autres méthodes de fixation, sinon l'équipe structure ne vont pas vous aimée.
Limitez la taille à 10 cm par 10 cm, car sinon les coûts explosent.

## Placement des composants
Placez les connecteurs et les éléments utilisateur(LED/bouton) en premier pour qu'ils soient facilement accessibles et logiquement placés.
Placer par la suite les composants importants ou qui ont des exigences complexes. Exemple : un ESP-32 est connecté à plusieurs affaires, donc une place centrale est utile. Un IMU doit être loin des sources électromagnétiques.
Placé par la suite les composants qui on un placement critique. Par exemple, des condensateurs pour des puces doivent être proches des puces.
Si le PCB a un enjeu de température, essayez de distancier les composants qui chauffent. Pensez à ceux qui vont soudé le PCB en plaçant les composant( pas trop proche si possible).
Pensez à la hauteur des composants en les plaçant.

## Tracé les pistes
Essayez de rester sur 2 couches si possible.
Tracer les pistes en priorisant les pistes différentielles et celles qui doivent être particulièrement courtes. Pour les pistes différentielles, limité la différence entre les pistes à un maximum de 1 mm.

<img width="710" height="509" alt="image" src="https://github.com/user-attachments/assets/c21afacc-8541-4768-b4fc-19b742e0c18a" />

Faites ceux de puissance par la suite. Utilisez l'outil de calcul sur Kicad pour connaître la largeur des pistes requise. Limitez l'augmentation de température(Temperature rise) à 10ºC. Gardez les épaisseurs de cuivre à 1 oz/ft^2.
Si vous avez l'espace, faites un ground plane. Ceci permet d'éviter les ground loops et diminue les perturbations et différences de tension sur le ground.
Quand vous faites un plan (plane), mettez des thermal relief sinon ça va être horrible à souder.
NE JAMAIS FAIRE DES ANGLE DE 90 DEGRES DANS LES PISTES.

Mettez plusieurs vias quand pas mal de courant est prévu pour limiter les pertes causées par la résistance des vias.

<img width="292" height="205" alt="image" src="https://github.com/user-attachments/assets/50810d25-b1e0-491b-a87b-3f65043b3d1f" />

Ne pas mettre de Vias sur un footprint sauf s'il est impossible de faire autrement. C'est une mauvaise pratique.

<img width="728" height="710" alt="image" src="https://github.com/user-attachments/assets/78b9c20c-c039-4921-bdb1-d3a9c0cb3500" />

Mettre des tests-points quand c'est possible pour aider le débogage. Ceux qui vont devoir reglé les problèmes vous remercie.

## Sérigraphie/Silkscreen
Il est important de mettre des informations pertinentes sur le PCB. IL est important de laisser le dessus professionnel. Pour le dessous, vous pouvez avoir un peu plus de fun.

### Information à mettre
* Numéro des petits composants ou une méthode d'identification (nom de composant, utilité) Certains numéros peuvent être omis s'il y a un manque clair d'espace et aucune autre méthode.
* Marquage important (Exemple sens d'un IMU)
* Symbole Biogenius (rajouté ceux de Robotique UdeS s'il a la place)
* Nom des concepteurs et des validateurs (vous faites du bon travail soyez fier!)

<img width="917" height="780" alt="image" src="https://github.com/user-attachments/assets/a19bc6eb-76de-4aef-b698-c02d419a6e27" />

### Warning qui peuvent être toléré

* Des silkscreens qui se supperpose
* Des FOOTPRINTS manquant(causés par une modification des silkscreens )
* Footprints not matching the one in the library (causés par une modification des silkscreens )
