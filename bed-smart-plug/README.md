# Bed Smart Plug

## Besoin

- Récepteur 433mhz (pour télécommande)
- Capteur température
- 4 sorties prises entre 5W et 200W
- Wifi et Ethernet

### Emplacements

- chambre parents
- chambre Eléonore
- chambre Éloïse
- chambre d'amis ?
- rdc derrière TV ?
- bibliothèque pour lampe pot de fleurs + température ?

## Choix techniques

- ESP32 ethernet ou wifi
- SSR pour éviter claquement relais
  - BT136 (4A max)
  - Dissipateurs
  - Fusible 5x20 à souder
- Entree Prise alim IEC C14
- Sorties prises IEC C13 pour avoir un format plus compact
- Capteur température :
  - DS18b20
  - avec Jack
  - possible souder jack a la main sinon
  - capteur integré inutile (mesure la temperature de l'esp/des triac pas de la piece)
- Télécommande 433MHz:
  - Renkforce 1208459
  - https://amzn.eu/d/fGBrWJP
  - https://www.conrad.fr/fr/p/renkforce-1208459-sans-fil-telecommande-interieure-1208459.html

## Design

- Board : ESP32-POE https://www.olimex.com/Products/IoT/ESP32/ESP32-POE/open-source-hardware
- Alim 220v -> 5V 1A : https://fr.rs-online.com/web/p/alimentations-a-decoupage/1812200
- DS18B20 avec Jack : https://amzn.eu/d/hBWke13
- Récepteur 433MHz : AM-RX9-433P https://fr.rs-online.com/web/p/modules-rf/8607236/
- Triacs : BT136-600E https://fr.rs-online.com/web/p/triac/7271120
  + heatsink
- ?? Prise entree C14 : https://fr.rs-online.com/web/p/connecteurs-iec/2615840/ ? (montage ci ?)
- ?? Dissipateurs : https://fr.rs-online.com/web/p/dissipateurs-de-chaleur/1898101/
- ?? Porte fusible : https://fr.rs-online.com/web/p/porte-fusible-pour-ci/1739698/
- ?? Connecteur Jack LED IR : https://fr.rs-online.com/web/p/connecteurs-jacks/9131011/

## Observations Prototype-1 epanel-io

- cf [epanel-io/README.md#observations](../epanel-io/README.md#observations) - Triac
- si on enleve snubber du phototriac, toujours une fuite (couper la piste entre C3 et C4)
- si on enleve les 2 snubbers, plus de fuite, spot led 10w reste eteint (couper la piste entre C3 et le triac)

## Prototype-1

### Objectifs

- Triac: 
  - dissipateurs
  - snubbers/bruit/fuite
    - spot 10w
    - guirlande boules
    - lampe incandescence train
    - lampe bureau
    - lampe chevet
    - alim a decoupage
- 433MHz receiver
  - binding avec telecommandes
- ds18b20
  - jack pinout
- prises C13/C14
- fusibles

## Notes

- Schémas
  - **https://innovatorsguru.com/switching-ac-load-using-triac/**
  - https://www.sonelec-musique.com/electronique_realisations_interfaces_230v_001.html
  - http://www.sper.hr/eng/solid_state_relay_scheme.htm
  - https://fr.rs-online.com/web/p/triac/7142577
  - http://wiring.org.co/learning/basics/lightbulb.html
  - https://www.sonelec-musique.com/electronique_realisations_relais_statique_001.html
  - https://electronics.stackexchange.com/questions/531528/relay-circuit-with-moc3021-and-bt136
  - https://electronics.stackexchange.com/questions/488518/triac-switch-circuit-using-moc3021-and-bt136
  - http://www.farnell.com/datasheets/97984.pdf (fig. 8)
  - Attention a garder le port USB accessible
- triacs
  - comparaison specs : https://www.esr.co.uk/components/products/frame-triacs.htm
