# RGB box

## Besoin

- 4 spots 24V 0.6W IDTOLight Monte Carlo LO681004ABX
  - pinout : + Black commun
- 2 spots 12V 10W
  - common +
- étanche
- ethernet
- tient dans regard

## Design

- esp32 poe
- petite alim pour ESP
- grosse alim + relais pour spots
- Mosfets:
  - IRLZ44N D2PAK
  - résistance de 10k - 100k entre commande et gnd, évite que ça flotte
- spot 12V 10W:
  - Resistances:
    - Red: 10Ω => https://jlcpcb.com/partdetail/Yageo-RC2512JK0710RL/C137014
    - Green, Blue: 5.1Ω => https://jlcpcb.com/partdetail/Koa_SpeerElec-RK73BW3ATTE5R1J/C514891
  - TODO:
    - tester passage cable
    - dessouder led
    - design pour embarquer, avec si possible bornier (voir si on a assez de place dessous pour les pins, et dessus) sinon souder directement les cables dessus
  - Footprint https://forum.fritzing.org/t/power-led-10w-rgb/6441

## Matériel

- Boîtiers : https://fr.rs-online.com/web/c/boitiers-coffrets-et-armoires/boitiers/boitiers-pour-usage-general/
- Alims :
  - 12V/30W : https://fr.rs-online.com/web/p/alimentations-a-decoupage/1358946
  - 24V/20W : https://fr.rs-online.com/web/p/alimentations-a-decoupage/1812126