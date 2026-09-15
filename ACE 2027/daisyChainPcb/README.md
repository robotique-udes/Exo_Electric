# PCB daisy chain

Ce PCB permet de passer les alimentations et les signaux de l'exo à travers celui-ci à la chaîne afin d'éviter les câbles superflus. Il sera sur les moteurs et permettra en même temps la communication et l'alimenation de ceux-ci.

## Objectifs
- Passer l'alimentation 48V d'un côté du PCB à l'autre
- Alimenter les moteurs
- Passer l'alimentation 5V d'un côté du PCB à l'autre
- Alimenter une puce permettant la conversion du 5V au 3.3V pour la communication I2C
- Remettre à niveau le signal I2C afin de s'assurer de sa bonne transmission
- Le rendre compatible avec l'exo 2026 et 2027
    - Être capable de passer la communication CAN tout en gardant la communication I2C au cas où elle doit être utilisé
- Se monter sur les moteurs de facon compacte et fiable
- Transmettre le signal UART (RX/TX) afin de communiquer de cette méthode avec les moteurs si c'est nécessaire (Certaines données peuvent être récuperer seulement dans un mode de communication et non l'autre)

## Conception

### Alimentation
Ce PCB doit gérer à la fois une alimentation de 48V et de 5V. Il y a deux grounds séparé. Le premier est celui de l'alimentation 48V et le deuxième est celui de l'alimentation de 5V. Le PCB a deux ground planes qui sont associés avec l'alimentation 5V. Cette décision a été prise afin de s'assurer de l'intégrité des signaux en donnant la plus grande surface de ground pour le circuit qui transporte les signaux. Ainsi, le ground lié à l'alimentation 48V est seulement connecté par des traces normales. La séparation de ces deux grounds permet aussi de s'assurer de ne pas avoir de tensions parasites qui passent par les IMU ou autre processeurs plus sensibles et évite donc de les détruire.

La communication I2C se fait à une tension de 3.3V. Il y a donc, sur le PCB, un convertisseur DC/DC qui transforme la tension de 5V vers 3.3V. Cette tension est ensuite envoyé vers les signaux I2C à travers une résistance de 1k.

### Disposition du PCB et choix de conception
Le PCB s'attache aux moteurs du côté des connecteurs de ce dernier. Il est donc important qu'il soit assez petit pour ne pas gêner aux mouvements de l'utilisateur. C'est pourquoi il n'y a pas de connecteurs pour l'alimentation et les signaux du côté du PCB. Seulement des beignes sont présents afin de souder des fils qui, eux, auront un connecteur au bout afin de se connecter aux moteurs.

Nous avons deux ground planes pour l'alimentation de 5V qui ont pleins de vias afin de bien connecter les deux planes ensemble.

Les traces qui transmettent les signaux sont le plus près possible l'un de l'autre et ont les mêmes longeurs. L'utilisation des vias a aussi été évité le plus possible.