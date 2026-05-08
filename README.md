# Dual_BLDC_IoT_Control_Synchronisation_System - STM32F407, STEVAL-SPIN3201, ESP32 MQTT

Projet embarque de controle differentiel de deux moteurs PMSM/BLDC. Le systeme utilise une carte STM32F407 comme controleur maitre, deux cartes STEVAL-SPIN3201 pour le controle moteur FOC, et une passerelle ESP32 pour publier la telemetrie vers MQTT/Node-RED.

## Architecture

```text
Potentiometre -> STM32F407 -> UART -> 2 x STEVAL-SPIN3201 -> Moteurs
                    |
                    +-> UART -> ESP32 -> MQTT -> Node-RED Dashboard
```

## Fonctionnalites

- Lecture potentiometre via ADC sur STM32F407.
- Calcul de vitesse differentielle gauche/droite.
- Commande START/STOP/SPEED vers deux cartes STEVAL-SPIN3201.
- Controle moteur FOC via ST Motor Control SDK.
- Telemetrie UART vers ESP32.
- Publication MQTT des vitesses et de l'angle potentiometre.
- Visualisation possible via Node-RED Dashboard.

## Technologies

- STM32F407VGTx, STM32F031C6Tx, ESP32.
- STM32CubeIDE / STM32CubeMX.
- STM32 Motor Control Workbench / MCSDK 6.3.2.
- Arduino ESP32, PubSubClient.
- UART 115200 8N1.
- MQTT via HiveMQ public broker.

## Structure actuelle

```text
code_esp32_MQTT/          Sketch Arduino ESP32 UART -> MQTT
stm_maitre/               Firmware STM32F407 maitre
STEVAL_SPIN3201/          Firmware STEVAL-SPIN3201 / MCSDK
photo pour rapport/       Figures de documentation
photo de rapport/         Captures et images supplementaires
docs/                     Documentation generee
```

## Points techniques importants

- Trame UART F407 -> SPIN3201 : `0xAA, cmd, value_lsb, value_msb, xor`.
- Commandes : START `0x01`, STOP `0x02`, SPEED `0x10`.
- Periode controle F407 : 20 ms.
- Periode telemetrie : 100 ms.
- PWM moteur SPIN3201 : 14 kHz.

## A corriger avant demonstration finale

- Harmoniser le format de telemetrie STM32F407/ESP32.
- Supprimer les identifiants Wi-Fi du sketch avant publication.
- Aligner les limites RPM entre STM32F407 et MCSDK.
- Exclure les dossiers `Debug/` et les artefacts binaires du depot.

## Documentation

- [Analyse technique complete](ANALYSE_TECHNIQUE_PROJET.md)
- [Guide d'installation](docs/INSTALLATION.md)

## Demo video

La video locale `Projet vidéo.mp4` est trop volumineuse pour un depot GitHub standard. Pour un portfolio, publier la video via GitHub Releases, Git LFS, YouTube non liste ou Google Drive, puis ajouter le lien ici.

## Licence

Le code applicatif original peut etre publie sous licence MIT. Les composants STMicroelectronics, STM32 HAL, CMSIS et MCSDK conservent leurs licences respectives.

# Architecture système

![Architecture](docs/figures/ArchitectureGeneraleDuSysteme.png)

## Features

- Dual PMSM/BLDC motor control
- Differential speed correction
- STM32F407 master controller
- FOC motor control using ST MCSDK
- ESP32 UART-to-MQTT gateway
- Node-RED real-time dashboard
- UART custom protocol
- Real-time telemetry
- MQTT IoT monitoring

## Tech Stack

### Embedded
- STM32F407VG
- STM32F031
- ESP32

### Software
- STM32CubeIDE
- STM32CubeMX
- STM32 MCSDK
- Arduino IDE
- Node-RED

### Communication
- UART
- MQTT
- Wi-Fi

### Motor Control
- BLDC
- Sensorless FOC
