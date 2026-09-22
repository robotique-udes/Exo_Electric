# Batterie custom et BMS (Battery management system)
Batterie fait sur mesure pour l'exosquelette ainsi que son BMS permettant de réduire le poids et répondre à nos demandes énergétiques exactes.

# Objectifs
## Batterie
- Tension nominale de la batterie à 48V
- Capacité d'environ 5Ah permettant d'alimenter l'exo pendant au moins 1h
- Fournir 48V à 4A en continue
- Offrir une puissance maximale d'environ 200W permettant à tous les moteurs d'être actif à la fois avec un peu de jeu
- Limiter le poids le plus possible
- Implémenter un système d'éjection de la batterie en cas de danger

## BMS
- Convertir la tension de 48V à du 5V et du 3.3V pour les sous-systèmes de l'exo à l'aide de convertisseur DC/DC
- Surveiller la tension de chaque paquet de cellules en série et de la batterie au complet
- Faire l'équilibrage des cellules
- Gérer les current spikes que demandent les moteurs lorsqu'ils démarrent
- Mesurer la température dans la batterie, sur les MOSFETs, sur les DC/DC converters et toute autre composants pouvant chauffer
- Signaler l'état de charge de la batterie en temps réel
- Permettre la vérification de l'état de santé de la batterie
- Avoir un arrêt d'urgence déconnectant la batterie de l'exo
- Protéger les composants sur l'exo à l'aide de fusibles à la sortie de la batterie