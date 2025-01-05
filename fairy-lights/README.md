# Fairy lights

## Besoin

- Avec Eléonore
- Guirlande pour sapin
- Intégré ESPHome

## Design

- WS2812B
- https://amzn.eu/d/6PvWFXF
- ( https://www.adafruit.com/product/4917 )
- WeMos D1 mini, sur gpio3 pour DMA
- config esphome dma
- Puissance guirlande : Alim 5V 6A -> 60ma / led
  - alim 6a (69.5x39x24) : https://fr.rs-online.com/web/p/alimentations-a-decoupage/1358945
  - alim 8a (87x52x29.5) : https://fr.rs-online.com/web/p/alimentations-a-decoupage/1358955
- IRLZ44N pour switch l'alim (sans heatsink), sortie esp direct sur Din LEDs : https://fr.rs-online.com/web/p/transistors-mosfet/5410086 541-0086