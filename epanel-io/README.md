# ePanel IO

![](mosfet-dimmer.png)

## Besoin
 - 20 IO au moins
 - mettre un Switch ou jumper pour relier les phases et neutres de 2 entrées sorties voisines (pour pouvoir relier ensemble ceux qui viennent du même disjoncteur)

## Notes

 - IRF740 -> 10A
 - Zc : https://electronics.stackexchange.com/questions/215094/how-to-test-if-zero-crossing-is-working
 - Rpi pico: 2 modules with 10 I/O each with io port0 = Zc + power supply

## Notes design ePanel (common with energy monitor)

 - i2c bus
 - Connexion i2c + power : connecteurs DIN 5 broches + cable ? rj11 ? rj45 ?
 - master controler olimex esp32 or rpi1 or rpi2? (peut etre dans le tableau electrique)
 - Adresse 7 bits
   - 4bits forts pour type de composants
   - 3bits faibles pour adressage du composant (paramétrable avec jumper si possible)

_ou_

 - uart
 - esp32 Ethernet + rpi pico sur chaque board
 - Switch dans tableau ?
 - avantages
   - chaque board est indépendante (Ethernet)
   - uart est bidirectionnel (pas de master/slave)
   - uart messaging semble simple à mettre en œuvre

## Links

220v current sensor (input) : https://arduino.stackexchange.com/questions/37044/127v-220v-ac-sensor-whats-the-role-of-this-particular-resistor
