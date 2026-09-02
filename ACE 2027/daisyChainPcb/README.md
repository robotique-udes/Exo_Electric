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

## Conception
Information importante sur la conception et comment l'utilisé
