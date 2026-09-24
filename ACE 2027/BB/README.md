# BIMU — IMU ESP32 + LSM6DSV16BXTR

Petit module qui gère tout l'exo squelette conçu autour d'un `ESP32`. Il gère entre autre la communication entre les différents modules comme les les BIMU, le BMS et les moteurs

## Objectif
* Basé sur unesp-32-S3(numéro digikey: 1965-ESP32-S3-WROOM-1U-N16R8CT-ND)
* Communication CAN avec le reste de l'exosquelette
* Consommation minimale
* Taille minimale  minimale(5 cm par 5 cm)
* Programmation par USB
* 3 Port Ethernet(1 spécial pour le BMS et 1 pour chaque jambe)
* 3 DEL pour diagnostic( une pour alimentation de la carte, une pour les erreurs, une communication(genre le heartbeat))
* Possibilité d'avoir une carte SD
* Protection contre les ground loop si alimenté par l'ordinateur et le BMS
* protection retour tension des jambes

## Conception
Le 

