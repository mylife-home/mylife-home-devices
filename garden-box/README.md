# Garden box

## Besoin

- capteur températeur
- capteur humidité sol
- drivers électrovannes
- drivers RGB 24v
- driver lanterne/guirlande

## Design

### generic

- 1 place pour un switch
- esp32 poe
- convertisseur 12v -> 5v
- 1 transfo 24v AC pour electrovannes (capable d'alimenter 3 ou 4 electrovannes), avec un relais
- 6 sorties relais, switchable (par jumper) entre 220v et 24v
- led en face de chaque relais (sortie + transfo 24v)
- ds 18b20
- capteur humidité sol avec ADC

### led driver

_TODO_

## Notes

- Bus avec 230v, 12v ondulé, ethernet
- Boite avec couvercle transparent
- Presses etoupe
- Electrovannes : Solénoïde robuste : 24 V c.a., courant d'appel de 370 mA, courant de maintien de 190 mA, 60 cycles ; courant d'appel de 475 mA, courant de maintien de 230 mA, 50 cycles
- Transfo : https://fr.rs-online.com/web/p/transformateurs-pour-circuits-imprimes/3472846 (36VA - 77.5x60x48.5)
- RS online has symbol library, convertible to kicad
- convertisseur 12v -> 5v : https://fr.rs-online.com/web/p/regulateurs-a-decoupage/1934032 (2A - regarder la datasheet il faut mettre des condensateurs avec)
- relais : 
  - Omron G6DN-1A-L DC5
  - https://fr.rs-online.com/web/p/relais-de-puissance/2051958 (En stock à partir du 27/03/2023)
  - https://fr.farnell.com/omron/g6dn-1a-l-dc5/relais-puissance-spst-no-5a-250v/dp/2831773
- capteur humidité sol : https://www.amazon.fr/gp/product/B07RGJHQ1L
- schema pilotage relais : https://i.stack.imgur.com/04BfF.jpg
- switch : https://eu.dlink.com/fr/fr/products/go-sw-5e GO-SW-5E
- boitier : https://fr.rs-online.com/web/c/boitiers-coffrets-et-armoires/boitiers/boitiers-pour-usage-general/?applied-dimensions=4294547633,4294564706,4294564365,4294256070,4292584295