# Description
Ce répertoire rassemble les divers PCB de l'exosquelette à travers les compétitions. Il vise aussi à standardiser la création des schémas électriques ainsi que les PCB afin de les rendre plus lisibles et plus faciles à réviser et consulter.

# Structure du repo
`On veut bien un README pour chaque PCB? Dans ma tête les README présenterait le fonctionnement du PCB et pourquoi il existe. Il montrerait aussi une image du schéma-bloc et l'expliquerait` <br>
`J'aime pas la redondance entre le code block avec la structure des fichiers et la liste en dessous` <br>
`On veut tu un fichier décrivant les changements pour chaque version du PCB?` <br>
```
main
├── ACE2027
│   ├── README.md
│   ├── Schéma-bloc
│   ├── PCB1
│   │   ├── README.md
│   │   ├── Schéma-bloc
│   │   └── Fichiers KiCad
│   └── PCB2
│       ├── README.md
│       ├── Schéma-bloc
│       └── Fichiers KiCad
└── ACE2028
    └── (Même structure que ACE 2027)
```

- Un dossier est créé pour chaque année de compétition
    - Contient un README.md décrivant le fonctionnement global des PCB et présentant le schéma-bloc
    - Contient le schéma-bloc en image et dans son format original décrivant l'intéraction entre les PCB 
    - Un dossier est créé par PCB
        - Contient un README.md qui explique le fonctionnement du PCB et présente le schéma-bloc
        - Contient le schéma-bloc en image et dans son format original décrivant l'intéraction entre les modules du PCB
        - Contient tous les fichiers KiCad

# Branches
`Selon moi on devrait avoir une branche pour le schéma et pour le PCB` <br>
`Est-ce qu'on veut garder la branche une fois que le PCB est fini? Ça permet de pouvoir aller le remodifier facilement, mais ça va faire beaucoup de branches éventuellement` <br>
`Si je veux changer un PCB qui est en version 1.0 et que je fais une nouvelle branche appelé PCBv1.1 et que je réalise après 1h de travail que j'ai chié un gros truc sur le PCB et qu'il va falloir faire une révison majeure, je fais quoi avec ma branche? Je la delete? Je la push dans main et après je me fais une 2.0?` <br>
`Comment on gère les branches qui modifient les PCB existants? Autant pour les grosses révisions que les petites` <br>
`Est-ce qu'on garde la branche de chaque PCB pour permettre de retourner dans les versions antérieures plus facilement. Si on fait ça, on pourrait pas avoir plusieurs branches pour plusieurs versions` <br>
`Mettre la version du PCB dans le commit à la place?` <br>
Une branche est créée pour chaque PCB. <br>
Cette branche doit contenir le nom du PCB ainsi que sa version et le déroulement de la vie de cette branche se déroule ainsi:
1. Création du schéma électrique
2. Création d'une pull request vers le main afin de faire vérifier le schéma
    - Faire les correctifs et demander à nouveau la vérification
3. Création du PCB
4. Création d'une pull request vers le main afin de faire vérifier le PCB
    - Faire les correctifs et demander à nouveau la vérification
5. Suppression de la branche une fois le PCB commandé

Convention de version:
- V1.0  Premier prototype
- V1.1  Corrections mineures
- V2.0  Révision majeure
- Chaque révision doit être documentée dans le dépôt Git avec un historique clair des modifications.

```
TOUJOURS SAUVEGARDER LES FICHIERS ET FERMER KICAD AVANT DE COMMIT
```

# Standards à respecter
Les standards pour le schéma électrique se trouvent [ici](guideSchema.md) <br>
Les standards pour le PCB se trouvent [ici](guidePCB.md) <br>
Ces standards doivent être consultés et compris avant d'entamer le travail sur un PCB