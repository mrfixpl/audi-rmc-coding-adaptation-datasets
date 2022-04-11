# Audi RMC: Coding, Adaptation, Datasets
Figuring out how #Audi #RMC system is configurable by testing coding, adaptation and datasets.
This type of infotainment unit is poorly codumented. I hope this is about to be changed.
I'm basinc my research on 2012 Audi Q3 equipped with Audi RMC non-navigation unit.

## How to tell if I have RMC or other system? ##
Enter Red Engineering Menu and check what's your software train. Audi RMC system firmware starts with `rmc`.

## Control Module address ##
Depending on vehicle and unit version, RMC can be accessed via address `0x56` or `0x5F`.

## Coding ##

## Adaptation ##
* `005` - `0` - developer mode off, `1` developer mode on.

## Datasets ##
RMC features and settings in EEPROM
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

## REM - Red Engineering Menu ##
* Enter it with key combination.

## System reboot ##
* Key combination

## Display screenshot ##
* Key combination
