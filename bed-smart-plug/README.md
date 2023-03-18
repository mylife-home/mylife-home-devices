# Bed Smart Plug

## Besoin

- Récepteur 433mhz (pour télécommande)
- Capteur température
- 4 sorties prises
- Wifi et Ethernet
- Emetteur IR pour piloter clim (au bout d'un câble comme capteur temperature)

### Emplacements

- chambre parents
- chambre Eléonore
- chambre Éloïse
- chambre d'amis
- rdc derrière TV
- bibliothèque pour lampe pot de fleurs + température ?

---
- 1 par clim + capteur température par pièce
- 1 par lit
- 1 télécommande 433 par chambre + 1 RDC

## Choix techniques

- ESP semble suffisant pour le projet (avec shield ethernet si besoin)
- SSR pour éviter claquement relais
  - BT136 (4A max)
  - Dissipateurs ?
  - Fusible 5x20 à souder
- Prise comme alim de PC, plus facile à mettre en oeuvre
- Capteur température : ds18b20
- utiliser jack pour IR et capteur temp
- capteur temp : avoir un capteur intégré et un capteur avec Jack?
- Idées :
  - Sorties prises IEC C13 pour avoir un format plus compact ?
  - Sortie USB direct sur la prise pour brancher le switch dessus en ethernet si besoin ?
  - Format prise : https://www.leroymerlin.fr/produits/electricite-domotique/interrupteur-et-prise/interrupteur-et-prise-en-saillie/bloc-5-prises-avec-terre-saillie-blanc-82016676.html ?
- Télécommande :
  - Renkforce 1208459
  - https://amzn.eu/d/fGBrWJP
  - https://www.conrad.fr/fr/p/renkforce-1208459-sans-fil-telecommande-interieure-1208459.html

## Observations Prototype-1 epanel-io

- cf [epanel-io/README.md#observations](../epanel-io/README.md#observations) - Triac
- si on enleve snubber du phototriac, toujours une fuite (couper la piste entre C3 et C4)
- si on enleve les 2 snubbers, plus de fuite, spot led 10w reste eteint (couper la piste entre C3 et le triac)

## Prototype-1

### Objectifs

- Triac: snubbers/bruit/fuite
  - spot 10w
  - guirlande boules
  - lampe incandescence train
  - lampe bureau
  - lampe chevet
  - alim a decoupage
  - test BT136-600E
    - https://www.farnell.com/datasheets/97984.pdf (fig. 8)
  - test BTA08-600TWRG (snubberless)
    - http://www.sper.hr/eng/solid_state_relay_scheme.htm
    - https://fr.rs-online.com/web/p/triac/7142577
    - http://wiring.org.co/learning/basics/lightbulb.html
    - __https://www.sonelec-musique.com/electronique_realisations_interfaces_230v_001.html__
- 433MHz receiver
  - binding avec telecommandes
- ds18b20 + jack pinout
- Led IR
  - jack pinout
  - binding avec clim
- prises comme PC
- fusibles
- triac dissipateurs

## Notes

- Ethernet ESPhome :
  - https://esphome.io/components/ethernet.html
- infrarouge
  - https://github.com/mdhiggins/ESP8266-HTTP-IR-Blaster
- Schémas
  - https://electronics.stackexchange.com/questions/531528/relay-circuit-with-moc3021-and-bt136
  - https://electronics.stackexchange.com/questions/488518/triac-switch-circuit-using-moc3021-and-bt136
  - http://www.farnell.com/datasheets/97984.pdf (bottom)
  - R 39ohm => 0,02496mW
  - R 360ohm => (very low)
  - R 470ohm => 7,52mW
  - C: 400V
  - Attention a garder le port USB accessible
  - Dessiner des mouting holes
- triacs
  - comparaison specs : https://www.esr.co.uk/components/products/frame-triacs.htm

## Matériel

- Déjà en stock
  - fil électrique 1.5mm²
- Alim ESP : https://fr.rs-online.com/web/p/alimentations-a-decoupage/9058755/
- ESP32 : ESP32-POE-ISO-EA https://www.olimex.com/Products/IoT/ESP32/ESP32-POE-ISO/open-source-hardware
- Récepteur 433MHz : AM-RX9-433P https://fr.rs-online.com/web/p/modules-rf/8607236/
- Prise comme alim de PC => C14 :
  - montage CI : https://fr.rs-online.com/web/p/connecteurs-iec/2615840/
  - voir si montage a cosses ?
- LED IR avec rallonge : https://www.amazon.fr/dp/B01MT59LFO
- ds18b20 + jack ??
- Composants:
  - C 50nF : https://fr.rs-online.com/web/p/condensateurs-polyethylene-naphtalate-pen/1649855/
  - C 10nF : https://fr.rs-online.com/web/p/condensateurs-polyester/6224779/
  - Dissipateurs : https://fr.rs-online.com/web/p/dissipateurs-de-chaleur/1898101/
  - Porte fusible : https://fr.rs-online.com/web/p/porte-fusible-pour-ci/1739698/
  - Connecteur Jack LED IR : https://fr.rs-online.com/web/p/connecteurs-jacks/9131011/

## Ancien matériel

- 4-Channel Solid State Relay : https://www.amazon.fr/dp/B01E6KUMTI
- Alim ESP : https://www.amazon.fr/dp/B07V7GHK51 (ou HLK 5M05)
- Récepteur 433mhz
- Resistances 100k : https://www.amazon.fr/dp/B016TG4QKS
- Prise pour alim comme PC : https://www.amazon.fr/dp/B07BN7G65F
- Cosses pour prises PC : https://www.amazon.fr/dp/B01FHAM1M2
- Boîtier
  - si assez de place : https://www.leroymerlin.fr/v3/p/produits/bloc-4-prises-avec-terre-mosaic-blanc-legrand-e1401456006
  - Sinon  https://www.leroymerlin.fr/v3/p/produits/bloc-4-prises-avec-terre-mosaic-blanc-legrand-e1401456005
- Prises : https://www.leroymerlin.fr/v3/p/produits/quadruple-prise-avec-terre-mosaic-legrand-blanc-e41326
