# Description
Ce répertoire regroupe les différents PCB de l'exosquelette au fil des compétitions. Il vise aussi à standardiser la création des schémas électriques ainsi que des PCB afin de les rendre plus lisibles et plus faciles à réviser et consulter. Les PCB avant 2026 ne suivent pas nécessairement le standard.

# Structure du repo
```
main
├── ACE2027/
│   ├── README.md
│   ├── Schéma-bloc
│   └── PCB1/
│       ├── README.md
│       ├── Schéma-bloc
│       │   ├── V1_0/
│       │   │   └── Fichiers KiCad
│       │   ├── V1_1/
│       │   │   ├── README.md
│       │   │   └── Fichiers KiCad
│       │   └── V2_0/
│       │       ├── README.md
│       │       └── Fichiers KiCad
│       └── PCB2/
│           └── (Même structure que PCB1)
└── ACE2028
    └── (Même structure que ACE 2027)
```
- Un dossier est créé pour chaque année de compétition
    - Contient un README.md décrivant le fonctionnement global du système électrique et présentant le schéma-bloc
    - Contient le schéma-bloc en image et dans son format original décrivant l'interaction entre les sous-systèmes électriques
    - Un dossier est créé par PCB
        - Contient un README.md qui explique le fonctionnement du PCB, contient les calculs et hypothèse fait pour le pcb et présente le schéma-bloc. Le README.md doit dire où se trouve le contour du pcb s'il a été fait sur ONSHAPE
        - Contient le schéma-bloc en image et dans son format original décrivant l'interaction entre les modules du PCB
            - Un dossier est fait pour chaque version du PCB.
                - La version 1_0 n'a pas besoin de README, mais les versions subséquentes devront en avoir un qui décrit les changements par rapport à la version antérieure.
                - Contient tous les fichiers KiCad

# Branches
Une branche est créée pour chaque PCB. <br>
Cette branche doit contenir le nom du PCB ainsi que sa version et le déroulement de la vie de cette branche se déroule ainsi:
1. Si le pcb est particuliairement complexe, écrire le readme et le shéma bloc qui défini ce que le PCB fait et comment il va le faire
2. Création d'une pull request vers le main afin de faire validé le fonctionnement du PCB
    - Faire les correctifs et demander à nouveau la vérification
3. Création du schéma électrique
4. Création d'une pull request vers le main afin de faire vérifier le schéma
    - Faire les correctifs et demander à nouveau la vérification
5. Création du PCB
6. Création d'une pull request vers le main afin de faire vérifier le PCB
    - Faire les correctifs et demander à nouveau la vérification
7. Suppression de la branche une fois le PCB commandé

## Convention de versions:
- V1.0  Premier prototype
- V1.X  Corrections mineures qui ne demandent pas de recommander le PCB
- VX.0  Révision majeure qui demande de recommander le PCB
- Chaque révision doit être documentée dans le README avec une explication claire des changements par rapport à la version précédente.

# Autres
**Il est très important de sauvegarder les fichiers et de fermer KiCad avant chaque commit**

# Standards à respecter
Les standards pour le schéma électrique se trouvent [ici](guideSchema.md) <br>
Les standards pour le PCB se trouvent [ici](guidePCB.md) <br>
Ces standards doivent être consultés et compris avant d'entamer le travail sur un schéma ou sur un PCB
