# Audi RMC: Codin, Adaptation, Datasets
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

## Dataset ##

## GEM - Green Engineering Menu ##
* Requires to be enabled first with adaptation.
* Enter it with key combination.

## REM - Red Engineering Menu ##
* Enter it with key combination.
