# Audi RMC: Coding, Adaptation, Datasets
Figuring out how Audi RMC system is configurable by testing coding, adaptation, datasets, and BAP.
This type of infotainment unit is poorly codumented. I hope this is about to be changed.
My research is based on a 2012 Audi Q3 equipped with Audi RMC2 non-navigation unit.

## How to tell if I have RMC or other system? ##
* There are different versions of the RMC system, nav and non-nav, with 6.5" and 7" displays.
* Enter Red Engineering Menu and check what's your software train. Audi RMC system firmware starts with `rmc`.
* https://youtu.be/R2mUmxFPWBQ

## Control Module address ##
Depending on vehicle and unit version, RMC can be accessed via address `0x56` or `0x5F`.

## Coding ##

## Adaptation ##
* `005` - `0` - developer mode off, `1` developer mode on.

## Datasets ##
Confirmed Audi RMC features and settings in EEPROM
* `F005C0` - Car Menu: Wiper Service + Rain Sensor
* `F00610` - Car Menu: Audi Drive Select (Charisma)
* `F00630` - Car Menu: VIN + Keys
* `F006F0` - Car Menu: Custom button MFSW (Joker)
* `F00F00` - Language: factory default
* `F01100` - Language: visible languages

## BAP ##
Features available on RMC screen that are coding in other modules and information about it is send over BAP.

## GEM - Green Engineering Menu ##
* Requires developer mode to be enabled first (check adaptation above).
* Enter GEM with key combination.
* https://youtu.be/jGcJXQZLzEc

## REM - Red Engineering Menu ##
* Enter it with key combination.
* https://youtu.be/PRefnQfClug

## System reboot ##
* Key combination

## Display screenshot ##
* Make sure there's an SD card inserted and it's not write protected.
* Press and hold buttons [<] and [>].
* Wait for LED confirmation on the control panel.
* https://youtu.be/ASmqbM54rZk
