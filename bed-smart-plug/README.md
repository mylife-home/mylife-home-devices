# Bed Smart Plug

## Besoin

 - Récepteur 433mhz (pour télécommande)
 - Capteur température
 - 4 sorties prises
 - Wifi et (Ethernet ?)
 - Emetteur IR pour piloter clim (au bout d'un câble comme capteur temperature)

## Choix techniques
 - ESP semble suffisant pour le projet (avec shield ethernet si besoin)
 - SSR pour éviter claquement relais
   - BT136 (4A max)
   - Dissipateurs ?
   - Fusible 5x20 à souder
   - résistance de 100k en // de la charge pour éviter déclenchements foireux ampoules leds, à tester ?
 - Prise comme alim de PC, plus facile à mettre en oeuvre
 - Capteur température : ds18b20
 - utiliser jack pour IR et capteur temp
 - capteur temp : avoir un capteur intégré et un capteur avec Jack?

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
