# ePanel Energy Monitory

## Besoin

 - 12 capteurs
   - abonnement 12KVA ~ 55A
   - 4 sur inter diff (entre 40A et 63A)
   - 8 sur disjoncteurs (entre 16A et 32A)
 - teleinfo
 
## Notes

 - arduino external ADC :
   - ADS1115 - I2C - 16 bits - 4 channels ADC
   - MCP3208 - SPI - 12 bits - 8 channels ADC
   - MCP3008 - SPI - 10 bits - 8 channels ADC
   - Arduino UNO interne 10 bits
   - rpi pico interne 3 ADC utilisables de 12 bits*
   - https://learn.openenergymonitor.org/electricity-monitoring/ct-sensors/yhdc-sct-013-000-ct-sensor-report

## Links

 - CT clamp : https://github.com/openenergymonitor/emontx3
 - teleinfo : http://sarakha63-domotique.fr/nodemcu-teleinformation-wifi/
 - esphome teleinfo : https://esphome.io/components/sensor/teleinfo.html
 - esphome CT clamp : https://esphome.io/components/sensor/ct_clamp.html
 - eshome 3208 : https://esphome.io/components/sensor/mcp3204.html

## Choix techniques

 - ESP32 : ESP32-POE-ISO https://www.olimex.com/Products/IoT/ESP32/ESP32-POE-ISO/open-source-hardware
 - Mcp3208 x2
