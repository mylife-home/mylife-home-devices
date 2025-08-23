# Gate driver

## Besoin

- piloter le portail
- le plus de contrôle possible
- boitier separé dans garage à côté du moteur de porte

## Design

- Carte avec WeMos D1 mini, fs1000a et boîtier comme clim

## Material

- boitier :
  - https://fr.rs-online.com/web/p/boitiers-pour-usage-general/9190373
- Wemos D1 mini :
  - https://www.amazon.fr/dp/B093G72SHN
- Emetteur :
  - FS100A
  - Oscillateur 433.42MHz
  - changer l'oscillateur : https://github.com/Nickduino/Pi-Somfy
  

## V1

### 3D view

![](v1/3dview.png)

_Note: mettre des pins male pour le FS100A_

### Main

![](v1/schematic.png)

### Images

| | | |
|---|---|---|
|<img src="v1/pictures/inside-top.jpg" width="300">|<img src="v1/pictures/inside-side.jpg" width="300">||
|<img src="v1/pictures/box-hole.jpg" width="300">|<img src="v1/pictures/box-side.jpg" width="300">|<img src="v1/pictures/box-hole.jpg" width="300">|

## Notes

- Sur la sérigraphie, GNC et VCC est inversés
- Trou fait à la perceuse puis lime ronde
- Apparairage :
  - l'émetteur doit être proche du portail
  - mettre le portail en mode appairage (ouvert, etc)
  - Actionner "ouverture" de l'émetteur
  - on peut essayer de poser une télécommande différente sur la cible

---

- https://github.com/rstrouse/ESPSomfy-RTS
- https://pushstack.wordpress.com/somfy-rts-protocol/
- https://github.com/dmslabsbr/esphome-somfy
- https://github.com/Nickduino/Pi-Somfy
- https://github.com/loopj/open-rts
- https://github.com/nicerloop/esphome-somfy-rts
- https://github.com/Legion2/Somfy_Remote_Lib
- appairage: https://forum.eedomus.com/viewtopic.php?f=14&t=2058
- rfxcom : http://www.rfxcom.com/epages/78165469.mobile/en_GB/?ObjectPath=/Shops/78165469/Products/14103&Locale=en_GB
