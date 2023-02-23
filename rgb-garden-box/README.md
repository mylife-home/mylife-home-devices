# RGB box

## Besoin

- 4 spots 24V 0.6W IDTOLight Monte Carlo LO681004ABX
  - pinout : + Black commun
- 2 spots 12V 10W
  - TODO:
    - tester passage cable
    - dessouder led
    - design pour embarquer, avec si possible bornier (voir si on a assez de place dessous pour les pins, et dessus) sinon souder directement les cables dessus
  - common +
  - Resistances:
    - Red: 10Ω
    - Green, Blue: 5.1Ω
- étanche
- ethernet
- tient dans regard

## Design

- esp32 poe
- petite alim pour ESP
- grosse alim + relais pour spots
- Mosfets: IRLZ44N D2PAK

## Matériel

- Boîtiers : https://fr.rs-online.com/web/c/boitiers-coffrets-et-armoires/boitiers/boitiers-pour-usage-general/
- Alims :
  - 12V/30W : https://fr.rs-online.com/web/p/alimentations-a-decoupage/1358946
  - 24V/20W : https://fr.rs-online.com/web/p/alimentations-a-decoupage/1812126