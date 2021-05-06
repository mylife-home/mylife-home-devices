# Bed Smart Plug

## Besoin

 - Récepteur 433mhz (pour télécommande)
 - Capteur température
 - 4 sorties prises
 - Wifi et (Ethernet ?)
 - Emetteur IR pour piloter clim (au bout d'un câble comme capteur temperature)

## Choix techniques
 - ESP semble suffisant pour le projet (avec shield ethernet si besoin)
 - SSR pour éviter claquement relais (avec une résistance de 100k en // de la charge pour éviter déclenchements foireux ampoules leds, à tester)
 - Prise comme alim de PC, plus facile à mettre en oeuvre
 - Capteur température : ds18b20

## Matériel
 - Déjà en stock
   - Récepteur 433mhz
   - ds18b20
   - fil éléctrique 1.5mm²
 - Boîtier
   - si assez de place : https://www.leroymerlin.fr/v3/p/produits/bloc-4-prises-avec-terre-mosaic-blanc-legrand-e1401456006
   - Sinon  https://www.leroymerlin.fr/v3/p/produits/bloc-4-prises-avec-terre-mosaic-blanc-legrand-e1401456005
 - Prises : https://www.leroymerlin.fr/v3/p/produits/quadruple-prise-avec-terre-mosaic-legrand-blanc-e41326
 - 4-Channel Solid State Relay : https://www.amazon.fr/dp/B01E6KUMTI
 - Alim ESP : https://www.amazon.fr/dp/B07V7GHK51 (ou HLK 5M05)
 - ESP32 : ESP32-POE-ISO-EA https://www.olimex.com/Products/IoT/ESP32/ESP32-POE-ISO/open-source-hardware
 - Resistances 100k : https://www.amazon.fr/dp/B016TG4QKS
 - Prise pour alim comme PC : https://www.amazon.fr/dp/B07BN7G65F
 - Cosses pour prises PC : https://www.amazon.fr/dp/B01FHAM1M2

## Notes
 - Ethernet ESPhome :
   - https://esphome.io/components/ethernet.html
 - infrarouge
   - https://github.com/mdhiggins/ESP8266-HTTP-IR-Blaster
