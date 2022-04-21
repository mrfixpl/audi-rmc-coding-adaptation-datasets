# Audi RMC: Coding, Adaptation, Datasets
* Figuring out how Audi RMC system is configurable by testing coding, adaptation, datasets, and BAP.
* This type of infotainment unit is poorly documented. I hope this is about to be changed.
* My research is based on a 2012 Audi Q3 equipped with Audi `RMC2` non-navigation unit and some parameterization files that I found over the internet.

![Audi RMC with AudiDriveSelect option](https://github.com/mrfixpl/audi-rmc-coding-adaptation-datasets/blob/main/research%20pictures/RMC-AudiDriveSelect.jpg)

## How to tell if I have RMC or other system? ##
* There are different versions of the RMC system, nav and non-nav, with 6.5" and 7" displays.
* Not confirmed yet: `RMC2` and `RMC4` units are using different dataset addresses.
* Not confirmed yet: `RMC2` = `H5x` = 6.5" display; `RMC4` = `H6x` = 7.0" display.
* Enter Red Engineering Menu and check what's your software train. Audi RMC system firmware starts with `rmc`.
* https://youtu.be/R2mUmxFPWBQ

## Control Module address ##
Depending on vehicle and unit version, RMC can be accessed via address `0x56` or `0x5F`.

## RMC2 and RMC4 coding ##
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
Audi `RMC2` features and settings in EEPROM (both **confirmed** and *anticipated*)

### Basic config ###
* `F00000` - **General Settings**
* `F00100` - **HFP**
* `F00200` - **Bluetooth**
* `F00300` - **Phone**
* `F00400` - *Vehicle platform*
* `F00800` - *Bus assignment*
* `F00900` - *Units default (speed, temperature, pressure, fuel economy, etc.)*
* `F00A00` - **Audi Music Interface (AMI) and USB**
* `F00B00` - **AMI BT (A2DP audio streaming)**
* `F00C00` - **Analog Audio AUX**
* `F01300` - **Speech Dialog System (SDS)**

### Sound System settings ###
* `F01500` - **Audio: Speakers diagnostics**
* `F01600` - **Audio: Sound parameters**
* `F02500` - **Audio: Speakers configuration**

### Car Menu options ###
* `F00500` - **CarMenu: Active Cruise Control (ACC)**
* `F00510` - **CarMenu: Interior light (ambient light)**
* `F00520` - **CarMenu: Parking system (APS/RVC)**
* `F00530` - **CarMenu: Braking way reduction (AWV)**
* `F00540` - **CarMenu: Lane departure warning (LDW/HCA)**
* `F00550` - **CarMenu: Lane change assist (SWA)**
* `F00560` - **CarMenu: Exterior lights (CH/LH/DRL?)**
* `F00570` - **CarMenu: Battery level**
* `F00580` - **CarMenu: Windows**
* `F00590` - **CarMenu: Air Condition**
* `F005A0` - **CarMenu: On-board Computer (TripComputer/Kombi)**
* `F005B0` - **CarMenu: Tyre Pressure Monitoring System (TPMS/RDK)**
* `F005C0` - **CarMenu: Wiper Service + Rain Sensor**
* `F005D0` - **CarMenu: Service interval (SIA)**
* `F005E0` - **CarMenu: Comfort Seats (memory)**
* `F005F0` - **CarMenu: Central Lock**
* `F00600` - **CarMenu: Compass**
* `F00610` - **CarMenu: Audi Drive Select (Charisma)**
* `F00620` - **CarMenu: Oil level**
* `F00630` - **CarMenu: VIN + Keys**
* `F00640` - **CarMenu: Clock**
* `F00650` - **CarMenu: Air Suspension**
* `F00660` - **CarMenu: Head-Up Display (HUD)**
* `F00670` - **CarMenu: ZEM (Main Unit settings)**
* `F00680` - **CarMenu: Hybrid**
* `F00690` - **CarMenu: Aux heating (Webasto?)**
* `F006A0` - **CarMenu: Universal Garage Door Opener (HomeLink/UGDO)**
* `F006B0` - **CarMenu: sideview camera**
* `F006C0` - **CarMenu: night vision**
* `F006D0` - **CarMenu: Reverse Seatbelt Tensioner (RGS)**
* `F006E0` - **CarMenu: Driving School Mode**
* `F006F0` - **CarMenu: Custom button MFSW (Joker)**
* `F00700` - *CarMenu: Daylight saving time*
* `F00710` - **CarMenu: Tilt Angle display (Offroad display)**
* `F00720` - **CarMenu: Weariness recognition (MKE)**

### Languages ###
* `F00F00` - **Language: factory default**
* `F01100` - **Language: visible languages**

### Other ###
* `F01400` - **Navigation activation code (FEC/FSC)**
* `F00D00` - *Video In Motion speed limits*

### CarManu values ###
Value determines when option is available (with ignition, at standstill, all the time...)
* `00 E1 F0` - 0, function hidden or not available
* `02 C1 B2` - 2
* `05 B1 55` - 5
* `07 91 17` - 7

Example function activation - parameterization with OBDeleven for Android
* Demo https://youtu.be/jsi80Yr3aoY

## Live Data ##
* `Channel 016` - CD drive temperature; ???, Cooling fan speed, N/A
* `Channel 019` - Up time, ???, ???, ???

## BAP ##
Features available on RMC screen that are coding in other modules and information about it is send over BAP.

## GEM - Green Engineering Menu ##
### Usage ###
* Requires developer mode to be enabled first (check adaptation above).
* Enter GEM with key combination: **[CAR]** + **[MENU]**
* Demo: https://youtu.be/jGcJXQZLzEc

### Custom GEM screens ###
*coming soon...*

## REM - Red Engineering Menu ##
* Enter REM with key combination: **[CAR]** + **[BACK]**
* Demo: https://youtu.be/PRefnQfClug

## System reboot ##
* Enter it with key combination: **[BACK]** + **[Control Wheel]** + **[Upper-Right]**
* Demo: https://youtu.be/KxOsZpEe3cY

## Display screenshot ##
* Make sure there's an SD card inserted and it's not write protected.
* Press and hold buttons **[<]** and **[>]**.
* Wait for LED confirmation on the control panel.
* Demo: https://youtu.be/ASmqbM54rZk

## RMC filesystem access ##
*coming soon...*

## Reference documents and tools used ##
* Equipment code search engine: http://prsearch.planetvag.com
* Checksum calculator: https://crccalc.com
* ASCII table: https://www.rapidtables.com/code/text/ascii-table.html
* OBDeleven diagnostic interface (ref link): http://obdeleven.com/?src=link&ref=Zy245Iacqc6bMTHh
