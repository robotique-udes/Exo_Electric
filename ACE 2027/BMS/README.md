# BMS


Description simple du PCB

## Objectif
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
Le ESP-32 du MOBO et du BMS sont les seul avec la possibilité de sans-fil. Ils sont dans les calculs, mais seulement celui du MoBo sera utilisé. Pour le budget puissance, les MISC c'est les pertes sur le PCB, les pertes de conversion, les autres petits composants et les LED. C'est une valeur estimé par règle du pouce. Elle est bien sur estimé pour confirmé le bon fonctionnement

### Budget Puissance 5V

* MOBO (300mA(ESP-32)+100mA(MISC))*3.3V=
* BIMU (35mA(ESP-32)+100mA(MISC))*3.3V=