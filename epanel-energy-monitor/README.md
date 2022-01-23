# ePanel Energy Monitory

## Besoin

 - 12 capteurs
   - abonnement 12KVA ~ 55A
   - 4 sur inter diff (entre 40A et 63A)
   - 8 sur disjoncteurs (entre 16A et 32A)
 - teleinfo
 
## Notes

 - arduino external ADC :
   - Mcp3208 12 bits
   - Mcp3008 10 bits
   - Arduino UNO interne 10 bits
   - rpi pico interne 3 ADC utilisables de 12 bits

## Links

 - CT clamp : https://github.com/openenergymonitor/emontx3
 - teleinfo : http://sarakha63-domotique.fr/nodemcu-teleinformation-wifi/
 - esphome teleinfo : https://esphome.io/components/sensor/teleinfo.html
 - esphome CT clamp : https://esphome.io/components/sensor/ct_clamp.html
 - eshome 3008 : https://esphome.io/components/sensor/mcp3008.html

## Choix techniques

 - ESP32 : ESP32-POE-ISO https://www.olimex.com/Products/IoT/ESP32/ESP32-POE-ISO/open-source-hardware
 - Mcp3208 x2
