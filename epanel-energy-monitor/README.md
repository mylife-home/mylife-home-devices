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
   - Calcul burden : `1,65÷(val×√2÷2000)` val = max courant en Amperes https://tyler.anairo.com/projects/open-energy-monitor-calculator

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
  - TODO: recoder esphome CT clamp pour etre adapter au montage OpenEnergyMonitor

### A faire pour proto 2:

- TIC
  - LTV-814
  - plusieurs choix de résistances pour TIC : 1k, 1.2k, 2k, 3.3k, 4.7k
  - mettre des pins headers pour pouvoir mesurer a l'oscillo si problème
- CT Clamp
  - mettre un MCP3208
  - jumper pour passer soit par MCP3208 soit direct sur ESP32
  - mettre des pins headers pour pouvoir mesurer au voltmètre
  - plusieurs burden possibles:
    - 20A 117ohm
    - 60A 39ohm
    - 16A 146ohm
    - 32A 73ohm
    - 10A 233ohm
