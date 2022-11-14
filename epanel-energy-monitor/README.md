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


## Links

- CT clamp : https://github.com/openenergymonitor/emontx3
- teleinfo :
  - http://sarakha63-domotique.fr/nodemcu-teleinformation-wifi/
  - https://github.com/schmurtzm/Teleinfo-TIC-with-ESPhome
- esphome teleinfo : https://esphome.io/components/sensor/teleinfo.html
- esphome CT clamp : https://esphome.io/components/sensor/ct_clamp.html
- eshome 3208 : https://esphome.io/components/sensor/mcp3204.html
## Choix techniques


- ESP32 : ESP32-POE-ISO https://www.olimex.com/Products/IoT/ESP32/ESP32-POE-ISO/open-source-hardware
- Mcp3208 x2

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

### Observations

- Teleinfo
  - ne fonctionne pas
  - WeMos TIC fonctionne, schematic : https://cdn.tindiemedia.com/images/resize/s_ZnNZRPrxDSvn3I8rBo9nkt9-8=/p/fit-in/1370x912/filters:fill(fff)/i/5857/products/2021-11-24T17%3A07%3A47.675Z-WeMos-TIC-sch.png?1637747448
  - Note : les valeurs des resistances correspondent bien au schematic
- CT Clamp MCP3008
  - GPIO15 = strapping pin