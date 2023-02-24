# RGB garden box

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
   - [Design](../rgb-spot-10w/README.md)

## Matériel

- Boîtiers : https://fr.rs-online.com/web/c/boitiers-coffrets-et-armoires/boitiers/boitiers-pour-usage-general/
- Alims :
  - 12V/30W : https://fr.rs-online.com/web/p/alimentations-a-decoupage/1358946
  - 24V/20W : https://fr.rs-online.com/web/p/alimentations-a-decoupage/1812126