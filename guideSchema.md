## Règles générales
Les schémas doivent respecter les conventions suivantes :
- Alimentation(5V, 48V) vers le haut
- Masse (GND) vers le bas
- Privilégier les labels plutôt que de longs fils traversant plusieurs zones du schéma.
- Les mounting holes doivent être avec l'alimentation et priorisé les M3
- Séparation par blocs fonctionnels
- Chaque fonction doit être regroupée dans un rectangle avec un titre clair.
- 
<img width="1068" height="547" alt="image" src="https://github.com/user-attachments/assets/cea32143-c941-4061-8d8a-7a29e2df256c" />

- Utilisation des pages hiérarchiques
- Créer une page distincte lorsqu'un bloc devient complexe, un PCB a beaucoup de blocs ou contient plusieurs exemplaires d'un composant.

Chaque PCB a une page:
- ALIMENTATION qui regroupe les protections électriques et les step-up et step-down. 
- CONTROLE qui regroupe le contrôleur, la communication, les connecteurs de signaux et les petits circuits pour le fonctionnement du contrôleur
- CAPTEUR qui regroupe les autres circuits de la carte

<img width="1068" height="725" alt="image" src="https://github.com/user-attachments/assets/1eaf7bf1-19d5-4ebd-93fb-88bb079ce7e1" />

Ajouter des notes lorsque la conception n'est pas évidente.

<img width="901" height="426" alt="image" src="https://github.com/user-attachments/assets/6f9f7326-a656-4970-b93e-89a9c2876344" />

Datasheets

Une datasheet doit être associée à tous les circuits intégrés(chip) pour faciliter les révisions. 

<img width="947" height="897" alt="image" src="https://github.com/user-attachments/assets/0a6a4d0c-9ebd-4882-82d3-7615bc3df9fb" />

Le champ Datasheet doit pointer vers la page officielle du fabricant.

Exemples :

ESP32-C3 Datasheet (Espressif)
LSM6DSV320X Datasheet (STMicroelectronics)
TCAN332 Datasheet (Texas Instruments)

Aucune puce ne doit être utilisée sans avoir consulté sa datasheet.

## Notation des composants

Convention de nommage des composants
| Type | Préfixe | Exemple |
| :--- | :--- | :--- |
| Résistance | R | R101 |
| Condensateur | C | C101 |
| Inductance | L | L101 |
| Ferrite | FB | FB101 |
| Diode | D | D101 |
| LED | D | D101 |
| Transistor BJT | Q | Q101 |
| MOSFET | Q | Q102 |
| Circuit intégré | U | U101 |
| Régulateur | U | U102 |
| Convertisseur DC/DC | U | U103 |
| Quartz | Y | Y101 |
| Oscillateur | Y | Y102 |
| Fusible | F | F101 |
| Interrupteur | SW | SW101 |
| Bouton poussoir | SW | SW102 |
| Connecteur | J | J101 |
| Relais | K | K101 |
| Jumper | JP | JP101 |
| Test Point | TP | TP101 |
| Transformateur | T | T101 |
| Antenne | ANT | ANT1 |
Convention de numérotation

Plage de numéros réservés à chaque sous-système.

| Bloc | Plage |
| :--- | :--- |
| Alimentations/protections | 100–199 |
| Microcontrôleurs/Communication | 200–299 |
| Capteurs | 300–399 |

Gestion des composants pour le BOM

Tous les composants doivent posséder les champs suivants :
| Nom | Quoi | Exemple |
| :--- | :--- | :--- |
| **Reference** | Numéro d'identification du composant | U3, R101 |
| **Value** | Valeur du composant | ESP32-S3-WROOM-1-N16R2, 10pF |
| **Footprint** | Format des pads pour les composants | Resistor_SMD:R_0603_1608Metric_Pad0.98x0.95mm_HandSolder |
| **Datasheet** | Documentation de la puce | Requis seulement pour les puces |
| **Description** | Information particulière | Résistance shunt pour la lecture du courant |
| **Digi-Key_PN** | Numéro Digi-Key des composants pour les BOM automatiques (doit être à jour) | 5407-ESP32-S3-WROOM-1-N16R2CT-ND |
<img width="948" height="900" alt="image" src="https://github.com/user-attachments/assets/f24be2d7-87f8-4cc8-85fe-3bfa98932571" />



Le BOM exporté doit permettre l'importation directe dans :

## DigiKey BOM Manager

Afin de générer automatiquement le panier, il faut que toutes les composantes aient leur **Digi-Key_PN**.
