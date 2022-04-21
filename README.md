# Audi RMC: Coding, Adaptation, Datasets
* Figuring out how Audi RMC system is configurable by testing coding, adaptation, datasets, and BAP.
* This type of infotainment unit is poorly documented. I hope this is about to be changed.
* My research is based on a 2012 Audi Q3 equipped with Audi `RMC2` non-navigation unit and some parameterization files that I found over the internet.
* Most likely `RMC2` and `RMC4` units are using different dataset addresses.

![Audi RMC with AudiDriveSelect option](https://github.com/mrfixpl/audi-rmc-coding-adaptation-datasets/blob/main/research%20pictures/RMC-AudiDriveSelect.jpg)

## How to tell if I have RMC or other system? ##
* There are different versions of the RMC system, nav and non-nav, with 6.5" and 7" displays.
* Enter Red Engineering Menu and check what's your software train. Audi RMC system firmware starts with `rmc`.
* https://youtu.be/R2mUmxFPWBQ

## Control Module address ##
Depending on vehicle and unit version, RMC can be accessed via address `0x56` or `0x5F`.

## Coding ##
* `Byte 00`:`bit 0-3` - `0000`=no maps; `0001`=Europe maps; `0010`=NAR maps
* `Byte 01`:`bit 0` - `0`=LHD; `1`=RHD
* `Byte 02`:`bit 0-3` - `0000`=sedan; `0001`=avant; `0100`=sportback, `0101`=allroad; `0110`=SUV
* `Byte 03`:`bit 0-1` - Boot screen `00`=default; `01`=S-Line; `10`=S; `11`=RS
* `Byte 04`:`bit 0-1` - Car Model `00`=A1; `01`=A6/A7; `10`=Q3
* `Byte 05`:`bit 7` - Ambient Illumination
* `Byte 06`:`bit 1` - Parking Sensors
* `Byte 06`:`bit 2` - Rear View Camera
* `Byte 07`:`bit 6` - Comfort Seats
* `Byte 08`:`bit 0` - Lane Assist
* `Byte 08`:`bit 1` - Side Assist
* `Byte 08`:`bit 3` - Pause Recommendation
* `Byte 14`:`bit 0` - `0`=Internal Audio Amplifier; `1`=External Audio Amplifier

## Adaptation ##
* `005` - `0` - developer mode off, `1` developer mode on.

## RMC2 Datasets ##
Audi RMC features and settings in EEPROM (both **confirmed** and *anticipated*)

### Sound System settings ###
* `F01500` - **Audio: Speakers diagnostics**
* `F01600` - **Audio: Sound parameters**
* `F02500` - **Audio: Speakers configuration**

### Car Menu options ###
* `F00500` - **Car Menu: Active Cruise Control (ACC)**
* `F00510` - **Car Menu: Interior light (ambient light)**
* `F00520` - **Car Menu: Parking system (APS/RVC)**
* `F00530` - **Car Menu: Braking way reduction (AWV)**
* `F00540` - **Car Menu: Lane departure warning (LDW/HCA)**
* `F00550` - **Car Menu: Lane change assist (SWA)**
* `F00560` - **Car Menu: Exterior lights (CH/LH/DRL?)**
* `F00570` - **Car Menu: Battery level**
* `F00580` - **Car Menu: Windows**
* `F00590` - **Car Menu: Air Condition**
* `F005A0` - **Car Menu: On-board Computer (TripComputer/Kombi)**
* `F005B0` - **Car Menu: Tyre Pressure Monitoring System (TPMS/RDK)**
* `F005C0` - **Car Menu: Wiper Service + Rain Sensor**
* `F005D0` - **Car Menu: Service interval (SIA)**
* `F005E0` - **Car Menu: Comfort Seats (memory)**
* `F005F0` - **Car Menu: Central Lock**
* `F00600` - **Car Menu: Compass**
* `F00610` - **Car Menu: Audi Drive Select (Charisma)**
* `F00620` - **Car Menu: Oil level**
* `F00630` - **Car Menu: VIN + Keys**
* `F00640` - **Car Menu: Clock**
* `F00650` - **Car Menu: Air Suspension**
* `F00660` - **Car Menu: Head-Up Display (HUD)**
* `F00670` - **Car Menu: ZEM (Main Unit settings)**
* `F00680` - **Car Menu: Hybrid**
* `F00690` - **Car Menu: Aux heating (Webasto?)**
* `F006A0` - **Car Menu: Universal Garage Door Opener (HomeLink/UGDO)**
* `F006B0` - **Car Menu: sideview camera**
* `F006C0` - **Car Menu: night vision**
* `F006D0` - **Car Menu: Reverse Seatbelt Tensioner (RGS)**
* `F006E0` - **Car Menu: Driving School Mode**
* `F006F0` - **Car Menu: Custom button MFSW (Joker)**
* `F00700` - *Car Menu: Daylight saving time*
* `F00710` - **Car Menu: Tilt Angle display (Offroad display)**
* `F00720` - **Car Menu: Weariness recognition (MKE)**

### Languages ###
* `F00F00` - **Language: factory default**
* `F01100` - **Language: visible languages**

### Other ###

Values to upload (value determinates when option is available - with ignition, at standstill...)
* `00 E1 F0` - 0, not available
* `02 C1 B2` - 2
* `05 B1 55` - 5
* `07 91 17` - 7

Example using OBDeleven
* https://youtu.be/jsi80Yr3aoY

## Live Data ##
* `Channel 016` - CD drive temperature; ???, Cooling fan speed, N/A
* `Channel 019` - Up time, ???, ???, ???

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
* [BACK] + [Control Wheel] + [Upper-Right]
* https://youtu.be/KxOsZpEe3cY

## Display screenshot ##
* Make sure there's an SD card inserted and it's not write protected.
* Press and hold buttons [<] and [>].
* Wait for LED confirmation on the control panel.
* https://youtu.be/ASmqbM54rZk
