# Fairy lights

## Besoin

- Avec Eléonore
- Guirlande pour sapin
- Intégré ESPHome

## Design

- Guirlande :
  - WS2812B
  - https://amzn.eu/d/6PvWFXF
  - ( https://www.adafruit.com/product/4917 )
- Contrôleur :
  - WeMos D1 mini, sur gpio3 pour DMA
  - config esphome dma
- Alimentation :
  - Puissance guirlande : Alim 5V 6A -> 60ma / led
  - alim 6A (69.5x39x24) : https://fr.rs-online.com/web/p/alimentations-a-decoupage/1358945
  - alim 8A (87x52x29.5) : https://fr.rs-online.com/web/p/alimentations-a-decoupage/1358955
  - alime externe 5V 8A : https://www.amazon.fr/dp/B088FBXTPS : `+` au milieu `-` à l'extérieur, 5.5mm - 2.5mm
- IRLZ44N pour switch l'alim (sans heatsink), sortie esp direct sur Din LEDs : https://fr.rs-online.com/web/p/transistors-mosfet/5410086 541-0086

## Prototype 1

- Sur breadboard
- Verifier qu'on peut piloter la guirlande avec esp8366/esphome

### Pinout de la guirlande

- `+` -> fil avec points noirs
- `D` -> fil du milieu
- `-` -> fil de l'autre côté 

<img src="pictures/fairy-lights-pinout.jpg" width="300">
