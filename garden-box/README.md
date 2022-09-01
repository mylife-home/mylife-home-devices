# Garden box

## Besoin

- capteur températeur
- capteur humidité sol
- drivers électrovannes
- drivers RGB 24v
- driver lanterne/guirlande

## Design

- 1 place pour un switch
- esp32 poe
- convertisseur 12v -> 5v OU alim 220v -> 5v?
- 1 transfo 24v AC pour electrovannes (capable d'alimenter 3 ou 4 electrovannes), avec un relais
- 6 sorties relais, switchable (par jumper) entre 220v et 24v
- ds 18b20
- capteur humidité avec ADC

## Notes

 - Bus avec 230v, 12v ondulé, ethernet
 - Boite avec couvercle transparent
 - Presses etoupe
---
 - Boite et bus + contrôleur (rpi) + mini switch ethernet 5 ports standards
 - Composants intérieurs (relai, transfo, rgb) + I/O custom
