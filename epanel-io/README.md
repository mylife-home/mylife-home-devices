# ePanel IO

![](mosfet-dimmer.png)

## Notes

 - IRF740 -> 10A
 - Zc : https://electronics.stackexchange.com/questions/215094/how-to-test-if-zero-crossing-is-working
 - Connexion i2c + power : connecteurs DIN 5 broches + cable ? rj11 ? rj45 ?
 - Design: (common with energy monitor)
   - Rpi pico: 2 modules with 10 I/O each with io port0 = Zc + power supply
   - i2c bus
   - master controler olimex esp32 or rpi1 or rpi2? (peut etre dans le tableau electrique)

## Links
