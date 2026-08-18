# BIMU — IMU ESP32 + LSM6DSV16BXTR

Petit module IMU conçu autour d'un `ESP32` et du capteur inertiel `LSM6DSV16BXTR`. Il fournit des mesures d'accélération et de rotation destinées aux calculs de l'exosquelette.

## Objectif
* Communication CAN avec le reste de l'exosquelette
* Refresh rate minimal de 100Hz si possible 200Hz pour futur proof
* Précision de 1° minimum
* Consommation minimale
* Programmation par USB
* 3 DEL pour diagnostic

## Conception
Le `LSM6DSV16BXTR` propose des modes d'échantillonnage configurables, du mode basse fréquence pour économiser l'énergie jusqu'à des ODR élevés (plusieurs centaines de Hz, voire le kHz en modes haute performance selon la fiche technique). Pour la plupart des usages, un réglage entre 200 et 1000 Hz constitue un bon compromis entre réactivité et consommation. Pour des dynamiques très rapides, privilégier `SPI` et activer les modes haute fréquence.

Après étalonnage (offsets, facteurs d'échelle, compensation thermique) et filtrage (filtre complémentaire, filtre de Kalman ou AHRS), on peut viser une précision d'orientation de l'ordre de 0,1° à quelques degrés selon les conditions, la durée d'intégration et la qualité mécanique du montage. Le bruit intrinsèque du capteur est typiquement de l'ordre de quelques µg/√Hz pour l'accéléromètre et quelques mdps/√Hz pour le gyroscope ; la performance finale dépendra du calibrage et du traitement logiciel.

Trois LED facilitent le diagnostic : la LED verte indique la présence de la tension 3,3 V, la LED bleue signale la connexion/heartbeat avec la carte principale, et la LED d'erreur (rouge) s'allume en cas de problème (communication avec le capteur, auto-test ou alimentation instable). Les motifs de clignotement sont configurables dans le firmware pour différencier les types d'anomalies.
<img width="262" height="272" alt="Capture d’écran 2026-08-16 130516" src="https://github.com/user-attachments/assets/1a293852-c854-4f09-bc2d-b45b54dd9554" />

Alimentation et connexions : entrée 5 V (par exemple fournie par l'Ethernet/PoE) avec régulation 3,3 V sur le PCB. Le capteur communique avec l'ESP32 par `SPI`. L'ESP32 communique avec le reste de l'exosquelette via `CAN`. La puce peut être programmée via `USB-C` ou `UART`. Il a bien sûr les boutons pour BOOT et EN l'ESP-32
<img width="276" height="178" alt="Capture d’écran 2026-08-16 130627" src="https://github.com/user-attachments/assets/cf2bd913-6b7f-4a6f-83c5-53b34b7cedbe" />

Les résistances de terminaison CAN sont présentes sur le PCB. Il est important de respecter le côté maître du bus si celui-ci est utilisé. Pour activer la terminaison, souder C210, R211 et R212.
<img width="290" height="209" alt="Capture d’écran 2026-08-16 130715" src="https://github.com/user-attachments/assets/955e798e-47af-47c7-b9e5-65f1f4d8849e" />

À prévoir dans le firmware : une fonction d'étalonnage, une compensation en température, le traitement des données sur l'IMU et une synchronisation via heartbeat. Il faut garder à l'esprit que le PCB ne sera pas nécessairement installé dans l'orientation prévue ; prévoir donc un réglage d'axes dans le firmware.

Il est possible de short des broches pour connecter ou isoler l'UART provenant de l'Ethernet vers l'ESP32 (utile pour communiquer avec le moteur si nécessaire).
|<img width="351" height="301" alt="Capture d’écran 2026-08-16 130741" src="https://github.com/user-attachments/assets/cc47f791-88f1-4c20-9f72-ad30e841f12c" />|<img width="262" height="189" alt="Capture d’écran 2026-08-16 130730" src="https://github.com/user-attachments/assets/fdd0da40-0252-4660-86fe-49c4c8558ad9" />|

