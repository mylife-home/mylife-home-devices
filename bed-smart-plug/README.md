# Bed Smart Plug

## Besoin

- Récepteur 433mhz (pour télécommande)
- Capteur température
- 4 sorties prises entre 5W et 200W
- Wifi et Ethernet
- Boitier :
  - peut etre relativement large/long, mais plat
  - avec les prises sur un côté
  - comme un switch
  - comme ca on peut le mettre sous un meuble, ou derriere un meuble debout

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
- Jack DS18B20 :
  - https://www.amazon.fr/dp/B075FYYLLV/
  - https://fr.rs-online.com/web/p/connecteurs-jacks/5051299
- Récepteur 433MHz : (modulation ASK)
  - ~~ AM-RX12A-433P https://fr.farnell.com/rf-solutions/am-rx12a-433p/recepteur-module-rf-433-92-110dbm/dp/2759279 ~~ (frais de gestion trop chers)
  - QAM-RX10-433 https://fr.rs-online.com/web/p/modules-rf/1258208
  - pinout compatible
  - normalement 5V, tester en broadboard avec alim 5V + pont diviseur sur les data pour passer a 3.3V
- Triac : BT136-600E https://fr.rs-online.com/web/p/triac/7271120
  + Dissipateur https://fr.rs-online.com/web/p/dissipateurs-de-chaleur/1898101/
- Porte fusible : https://fr.rs-online.com/web/p/porte-fusibles/1769047
  + Fusible : https://fr.rs-online.com/web/p/fusibles-cartouches/6686007
- Prises :
  - entree C14 : https://fr.rs-online.com/web/p/connecteurs-iec/8117207
  - sortie C13 : https://fr.rs-online.com/web/p/connecteurs-iec/8117193
  - (cf datasheet pour le montage)
  - branchements par cosses 4.8x0.8
  - cosses : https://fr.rs-online.com/web/p/cosses-faston/0534749
  - cable souple 1.5mm2 : https://www.amazon.fr/dp/B01FHJJY96 (bleu)

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
    - lampe bureau
    - lampe chevet
    - alim a decoupage
- 433MHz receiver
  - binding avec telecommandes
- ds18b20
  - jack pinout: voir quelles broches sur chaque prise matchent + selectionner le pinout qu'on veut.
- fusibles

TODO
- boitier avec sortie RJ45 + jack + fixations C13/C14

### Schematic

- [Schematic](prototype-1/schematic.png)

### Pinout

- GPIO02 : Triac
- GPIO13 : DS18B20
- GPIO36 : Récepteur 433MHz

### Observations

- Dissipateur :
  - Rapprocher dissipateur et triac de 0.5 - 1 mm
  - Fixation dissipateur/triac : écrou M3 + reprendre vis M3 anti-deserrage garden-box
- Fusibles : OK
- Triac :
  - spot 10w :
    - triac snubber => fuite (KO)
    - opto snubber => fuite (KO)
    - sans snubber => pas de bruit (OK)
  - Perceuse à colonne :
    - puissance : 1.6A au démarrage puis 0.8
    - Avec/Sans snubber : pas de bruit mais la perceuse fait elle du bruit
    - apres 5 mins dissipateur + triac froids 
  - Lampe chevet Éloïse
    - puissance : 26.5ma
    - Avec snubber : KO bruit quand off
    - Sans snubber : OK sans bruit
  - Guirlande Éloïse
    - Avec snubber : KO clignote
    - Sans snubber : OK sans bruit
    - puissance très instable semble avec des pics a 600ma puis revient a 0ma (problème multimètre ?)
  - Lampe bureau
    - puissance semble 25ma (problème multimètre ?)
    - Avec snubber : KO bruit quand off
    - Sans snubber : OK sans bruit
  - Lampe chevet Eléonore
    - puissance 1.5a???? (problème multimètre ?) -> Ampoule à incandescence 40W
    - Avec snubber : OK sans bruit
    - Sans snubber : OK sans bruit
- Prise jack 
  
  <img src="pictures/jack-pinout.jpg" width="300">
  
  (de gauche à droite) 
  - 1 : corps
  - 2 : pin penché 
  - 3 : base pin central
  - 4 : extrémité pin central

  Attention : bien enfoncer la prise

- Récepteur 433mhz
  - Les 2 pins data sont reliés ensemble 
  - Connecter au 5V, et mettre un point diviseur :
    - R1 = 10k (entre output recepteur et input ESP)
    - R2 = 2x 10k en série (entre input ESP et GND)
  - Config dump : 
```yaml
    remote_receiver:
      pin: GPIO36
      dump:
      - rc_switch
      tolerance: 50%
      filter: 250us
      idle: 4ms
      buffer_size: 2kb
```
  - Valeurs (le repeat est très rapproché) : 
  
  _Config télécommande grise : 1 = ON, 5 = ON_
  
| Action | code télécommande | code ABCD | ?? | on/off |
|---|---|---|---|---|
| A on   | 00 01 01 01 00 | 00 01 01 01 | 01 | 00 01 |
| A off  | 00 01 01 01 00 | 00 01 01 01 | 01 | 01 00 |
| B on   | 00 01 01 01 00 | 01 00 01 01 | 01 | 00 01 |
| B off  | 00 01 01 01 00 | 01 00 01 01 | 01 | 01 00 |
| C on   | 00 01 01 01 00 | 01 01 00 01 | 01 | 00 01 |
| C off  | 00 01 01 01 00 | 01 01 00 01 | 01 | 01 00 |
| D on   | 00 01 01 01 00 | 01 01 01 00 | 01 | 00 01 |
| D off  | 00 01 01 01 00 | 01 01 01 00 | 01 | 01 00 |

  _Config télécommande grise : 1 = ON, 2 = ON_
  => Code télécommande : 00 00 01 01 01, le reste semble correspondre

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
- boitier
  - fusion 360
  - https://www.thingiverse.com/thing:3700953 (esp32-poe box case, pour la taille + le socket)
  - https://www.printables.com/model/476196-esp32poe-box-v12 (esp-poe box case, pour le maintien du boitier + la taille + le socket)
  - https://www.thingiverse.com/thing:410003 (rapsberry-pi box case, pour les vis + inspiration)
