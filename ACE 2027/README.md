L'objectif de l'exo est de faire que tout fonctionne par communication CAN.
## Composants

### MoBo
C'est la carte mère(MOtherBOard) de l'exosquelette. Il a le ESP-32 qui controle tout l'exosquelette. Il a un convertisseur 5V à 3.3V et tout le reste est de la filtration de tension et des connecteurs.

### BMS
Il gère la gestion des batteries, les fuses et le l'arrêt d'urgence. Le but est aussi de pouvoir communiqué avec le MoBo pour lui donné des états sur les batteries.

### BIMU 
C'est des IMU qui font le traitement brutes des données directement sur le module avant de les préparé et les envoyés.

### Moteur 

Il a une carte d'interface sur le moteur pour pouvoir facilement Daisy Chains les cables et pouvoir utilisé les cables ethernet avec les moteurs.

## Communication
Toutes la communication à lieu avec des cables ethernets. Le principal branchement est le suivant:

<img width="800" height="496" alt="Screenshot from 2026-08-21 22-36-26" src="https://github.com/user-attachments/assets/140933d3-990f-4e91-aace-11097b0aaab1" />

<img width="267" height="229" alt="Screenshot from 2026-08-21 23-15-49" src="https://github.com/user-attachments/assets/fea70deb-7522-4bc5-b99a-96a7c220ccae" />

Il branche tout sur l'exo sauf entre le MoBo et le BMS, car cette connection à besoin de plus de courant. Entre le MoBo et le BMS, il a cette conection:

<img width="618" height="550" alt="Screenshot from 2026-08-21 23-17-47" src="https://github.com/user-attachments/assets/0700c2c6-d3f0-442d-a39f-77646378ff67" />
