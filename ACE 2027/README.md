# ACE 2027

Projet d’électronique et de communication pour l’exosquelette électrique.

> **Objectif principal** : faire communiquer les différents modules de l’exosquelette via un bus CAN fiable, tout en distribuant l’alimentation et en assurant les fonctions de sécurité.

## Sommaire

- [Architecture](#architecture)
- [Modules](#modules)
- [Communication](#communication)
- [Documentation du dépôt](#documentation-du-dépôt)
- [À documenter](#à-documenter)

## Architecture

Le système est organisé autour d’une carte mère (**MoBo**, *Motherboard*) qui coordonne les modules. Le **BMS** supervise les batteries et la sécurité. Les **BIMU** mesurent les mouvements, tandis que les cartes d’interface des moteurs assurent leur raccordement au réseau.

## Modules

| Module | Rôle | Éléments principaux |
| --- | --- | --- |
| **MoBo** | Carte mère et coordination de l’exosquelette | ESP32, conversion 5 V vers 3,3 V, filtrage de tension, connecteurs |
| **BMS** | Gestion des batteries et fonctions de sécurité | Fusibles, arrêt d’urgence, suivi de l’état des batteries |
| **BIMU** | Mesure et prétraitement des mouvements | IMU, traitement local des données, transmission via CAN |
| **Moteur** | Raccordement des moteurs au réseau | Carte d’interface, chaînage (*daisy chain*), connecteurs de type Ethernet |

### MoBo

La MoBo est la carte mère de l’exosquelette. Elle contient l’ESP32, qui coordonne le système, ainsi qu’une conversion 5 V vers 3,3 V, le filtrage des tensions et les connecteurs nécessaires.

### BMS

Le BMS gère les batteries, les fusibles et l’arrêt d’urgence. Il doit également communiquer avec la MoBo afin de transmettre l’état des batteries.

### BIMU

Chaque BIMU effectue localement le traitement initial des données de son ou de ses capteurs IMU, puis transmet les données préparées sur le bus CAN.

### Moteurs

Une carte d’interface est placée au niveau des moteurs. Elle facilite le chaînage des câbles et permet l’utilisation de câbles Ethernet pour le raccordement physique.

## Communication

Les modules communiquent principalement sur un bus CAN transporté par des câbles Ethernet. Le branchement général est représenté ci-dessous.

![Schéma général du réseau de l’exosquelette](https://github.com/user-attachments/assets/140933d3-990f-4e91-aace-11097b0aaab1)

![Détail du raccordement des modules](https://github.com/user-attachments/assets/fea70deb-7522-4bc5-b99a-96a7c220ccae)

La liaison entre la MoBo et le BMS est particulière : elle doit fournir davantage de courant que les autres liaisons. Son raccordement est présenté ci-dessous.

![Liaison entre la MoBo et le BMS](https://github.com/user-attachments/assets/0700c2c6-d3f0-442d-a39f-77646378ff67)

### Règles CAN à définir

Les éléments suivants doivent être précisés pour rendre l’architecture exploitable par toute l’équipe :

- débit du bus CAN et longueur maximale des câbles ;
- brochage des connecteurs et câblage exact de l’alimentation ;
- identifiants CAN attribués à chaque module ;
- format des messages, périodicité et unités des mesures ;
- terminaison du bus et emplacement des résistances ;
- comportement attendu en cas de perte de communication ou d’arrêt d’urgence.

