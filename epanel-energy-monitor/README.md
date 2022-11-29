# ePanel Energy Monitory

## Besoin

- 12 capteurs
  - abonnement 12KVA ~ 55A
  - 4 sur inter diff (entre 40A et 63A)
  - 8 sur disjoncteurs (entre 10A et 32A)
- teleinfo
 
## Notes

- arduino external ADC :
  - ADS1115 - I2C - 16 bits - 4 channels ADC
  - MCP3208 - SPI - 12 bits - 8 channels ADC
  - MCP3008 - SPI - 10 bits - 8 channels ADC
  - Arduino UNO interne 10 bits
  - rpi pico interne 3 ADC utilisables de 12 bits
  - https://learn.openenergymonitor.org/electricity-monitoring/ct-sensors/yhdc-sct-013-000-ct-sensor-report
- Calcul burden : `1,65 / (val * √2 / 2000)` val = max courant en Amperes https://tyler.anairo.com/projects/open-energy-monitor-calculator
- Alimentation : 
  - rpi pico: < 100ma
  - esp32 poe: 200ma
  - mcp3208: 0.4ma
  - alim 220v -> 5V 1A : https://fr.rs-online.com/web/p/alimentations-a-decoupage/1812200
- mettre un switch pour couper l'alimentation, permet de hard-reboot en cas de plantage
  - on peut aussi rajouter une led de power et une d'état https://esphome.io/components/status_led.html
  - a voir comment implanter ca dans le couvercle du boitier DIN


## Links

- CT clamp : https://github.com/openenergymonitor/emontx3
- teleinfo :
  - http://sarakha63-domotique.fr/nodemcu-teleinformation-wifi/
  - https://github.com/schmurtzm/Teleinfo-TIC-with-ESPhome
- esphome teleinfo : https://esphome.io/components/sensor/teleinfo.html
- esphome CT clamp : https://esphome.io/components/sensor/ct_clamp.html
- eshome 3208 : https://esphome.io/components/sensor/mcp3204.html

## Choix techniques

- ESP32 : ESP32-POE https://www.olimex.com/Products/IoT/ESP32/ESP32-POE/open-source-hardware
- MCP3208 x2 _ou_ ADS1115 x4

## Prototype-1

![](prototype-1/schematic.png)

### Tests

### Observations

- Teleinfo
  - mauvais composant pour optocoupleur :
    - courant LTV-8141
    - correct: LTV-814 (C125118)
  - voir si on doit mettre une résistance de 4.7K, 1.2K ou 1K
- CT Clamp
  - les prises jack a souder sont très peu épaisses, elles doivent être au board du PCB ou changer de modèle
  - test avec aspirateur:
    - Théoriquement: 1300W /230V = 5.6A
    - Mesure avec ampèremètre sur directement sur le courant secteur : 6.12A
    - Mesure avec voltmètre aux bornes du burden resistor 120ohm : 0.31V /120Rb *2000 = 5.16A
    - Mesure avec oem_clamp recodé : 7.55A à l'allumage puis 6.35A après (instable). Note : le 0 est à 0.06A

### A faire pour proto 2:

- TIC
  - LTV-814
  - plusieurs choix de résistances pour TIC : 1k, 1.2k, 2k, 3.3k, 4.7k
  - mettre des pins headers pour pouvoir mesurer a l'oscillo si problème
- CT Clamp
  - mettre un MCP3208
  - jumper pour passer soit par MCP3208 soit direct sur ESP32
  - attention: GPIO2 et GPIO4 ne semble pas etre valides pour ADC avec esphome. GPIO32 et GPIO33 oui
  - mettre des pins headers pour pouvoir mesurer au voltmètre
  - plusieurs burden possibles:
    - 10A 233ohm -> 220 (10.6A)
    - 16A 146ohm -> 150 (15.6A)
    - 20A 117ohm -> 120 (19.4A)
    - 32A 73ohm -> 75 (31.1A)
    - 60A 39ohm -> 33 (70.7A)
- test emplacement ESP32
  - avec le connecteur ethernet vers le bas
  - sur la partie droite, mais pas collé (sinon les ergo vont gener)
  - au milieu en hauteur
  - on decoupera le boitier au dremel pour faire la place pour le connecteur ethernet

## Prototype-2

![](prototype-2/schematic.png)

### Tests

- CT Clamp avec ADC ESP32 - Burden 220ohm (10A) sur sèche cheveux 1500W
  - eteint : 0.030A - 0.036A
  - level1 : 2.321A - 2.323A = 533W
  - level3 : 6.395A - 6.431A = 1470W - 1479W

- CT Clamp avec MCP3008 - Burden 220ohm (10A) sur sèche cheveux 1500W
  - eteint : 0.043A - 0.105A
  - level1 : 2.316A = 532.68W
  - level3 : 6.335A = 1457W

- CT Clamp avec MCP3008 - Burden 75ohm (32A) sur SPA
  - au "repos" : 0.117A - 0.258A -> 26,91W - 59,34W
  - filtration? : 0.551A -> 126,73W
  - au "travail" (chauffage ?) : 11.751A -> 2700W

- CT Clamp comparaison avec Schneider avec MCP3008 - Burden 75ohm sur sèche cheveux 1500W - level3
  - Mesure avec CT clamp YHDC : 6.3 - 6.4
  - Mesure avec multimetre : 6.36
  - Mesure schneider config 1600 turns => 5.6
  - Mesure schneider config 2000 turns => 7
  => en faisant le ratio, CT clamp Schneider = 1800 turns

- CT Clamp comparaison avec Schneider avec MCP3008 - Burden 75ohm sur ampoule 40W
  - Mesure schneider config 1800 turns : 0.27
  - Mesure schneider config 1600 turns : 0.24
  - Mesure avec multimetre : 0.15
  - 40W = 0.17
  => en faisant le ratio, CT clamp Shneider = 1000 turns => tres peut precis, mais 0.27A sur 32A < 1%

- CT Clamp comparaison avec Schneider avec MCP3008 - Burden 220ohm sur ampoule 40W
  - Mesure schneider config 1800 turns : 0.18
  - Mesure avec multimetre : 0.15
  - 40W = 0.17


### Observations

- Teleinfo
  - ne fonctionne pas
  - WeMos TIC fonctionne, schematic : https://cdn.tindiemedia.com/images/resize/s_ZnNZRPrxDSvn3I8rBo9nkt9-8=/p/fit-in/1370x912/filters:fill(fff)/i/5857/products/2021-11-24T17%3A07%3A47.675Z-WeMos-TIC-sch.png?1637747448
  - Note : les valeurs des resistances correspondent bien au schematic
- CT Clamp MCP3008
  - GPIO15 = strapping pin
  - rajouter Voltage sensor pour pouvoir calculer la puissance réelle
    - https://learn.openenergymonitor.org/electricity-monitoring/voltage-sensing/measuring-voltage-with-an-acac-power-adapter
    - https://fr.rs-online.com/web/p/transformateurs-pour-circuits-imprimes/1213819
  - tester reactivité ESP32 avec 16 mesures (meme si pas de CT clamp, juste pour etre sur que ca ne perde pas en reactivite)
  - trouver des CT Clamp plus petits ? comme ceux de Schneider ?
    - ceux de Schneider:
      - https://www.amazon.fr/Transformateurs-courant-ferm%C3%A9s-80a-Lot/dp/B01G5M1MT4
      - https://www.se.com/fr/fr/product/EER39200/wiser-energy-lot-de-5-tc-transformateurs-de-courant-ferm%C3%A9s-80a/
      - semble etre 80A:50mA => en fait 1800 turns
      - tore d'une seule pièce
  - faire une sortie screwterminal a cote du jack pour pouvoir tester d'autres CT Clamp
  - burdens:
    - essayer d'optimiser les valeurs en pouvant les mettre en //
    - attention : schneider CT turns = 1800, YHDC CT turns = 2000
- Montage ESP32 dans DIN box
  - trop sur le côté, décaler de 2-3mm vers le milieu
  - la prochaine fois faire un truc moins cochon au Dremel
- Montage prises Jack
  - l'emplacement est parfait, mais on ne peut pas en mettre de chaque coté de la board et la faire rentrer dans le boitiers car ils depassent

### A faire pour proto 3

- Teleinfo
  - doit fonctionner
  - ajouter une led
- CT Clamp
  - ajouter un ADS1115 pour tester la difference de précision, avec un autre switch
    - datasheet : https://www.ti.com/lit/ds/symlink/ads1115.pdf
    - avec un burden pour 60A et la precision de l'ADC, cela suffit peut etre sans burden en plus ?
  - ajouter capteur de tension
    - Transfo : 6V -> https://fr.rs-online.com/web/p/transformateurs-pour-circuits-imprimes/7320525
    - 6V RMS
    - = 8.5V peak
    - = 17V peak-peak
    - ratio: 12 / (100 + 12) = 0,107
    - = 1,819V
  - ajouter ampli op
    - https://learn.openenergymonitor.org/electricity-monitoring/ctac/acac-buffered-voltage-bias
    - pour chaque capteur, switch ampli op ou pont diviseur
  - mettre plusieurs capteurs de courant pour etre sur que l'ampli op fonctionne pour plusieurs, eg : 3 capteurs CT + 1 tension
  - mettre des terminalscrews au lieu des jacks pour tester CT Schneider
  - jeu de burden resistances pour CT turns 1800
    - 10A 210ohm -> 200 (10.5A)
    - 16A 131ohm -> 130 (16.2A)
    - 20A 105ohm -> 100 (21A)
    - 32A 66ohm -> 62 (33.9A)
    - 60A 35ohm -> 33 (63.6A)
  - tester avec vraie alim (pour tester la stabilité des mesures avec l'alim)
  - diodes pour protéger les ADC : https://openenergymonitor.github.io/forum-archive/sites/default/files/MyInputCircuits_0.jpg
    - ADS a deja des protections dans son MUX
  - pour chaque capteur, switch ADS vs MCP vs ESP
- Montage ESP32
  - corriger l'emplacement sur la board

## Prototype-3

![](prototype-3/schematic.png)

### Tests

### Observations

- Teleinfo
  - LTV-814 : mauvais footprint, le bon est plus "écarté", cf jlcpcb/parts
  - BSS138: mauvais pinout/footprint, cf jlcpcb/parts
