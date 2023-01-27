# Audi RMC: Coding, Adaptation, Datasets
* Figuring out how Audi RMC system is configurable by testing coding, adaptation, datasets, and BAP.
* This type of infotainment unit is poorly documented. I hope this is about to be changed.
* My research is based on a 2012 Audi Q3 equipped with Audi `RMC2` non-navigation unit and some parameterization files that I got from community and found over the internet.

![Audi RMC with Driving School Mode option](https://github.com/mrfixpl/audi-rmc-coding-adaptation-datasets/blob/main/research%20pictures/RMC-DrivingSchoolMode.jpg?raw=true)

## How to tell which RMC system I have?
* There are different versions of the RMC system, nav and non-nav, with 6.5" and 7" displays, pre-facelift and facelift.
* Distinguish RMC from MMI: enter Red Engineering Menu and check what's your SW Train. Audi RMC system firmware starts with `rmc`, MMI starts with `bbt`, `bnav`, `hnav`. Check this: https://youtu.be/R2mUmxFPWBQ
* `RMC2` and `RMC4` units are using different dataset addresses.
* part # `4G0`/`8X0` = `H5x` = `RMC2`; part # `4G1`/`8X1` = `H6x` = `RMC4`.
* There's also `H4x` option available. Not sure what it exactly is. Maybe old `RMC` (`RMC1`)?
* RMC is usually available at address `0x5F` - infotainment. But in some cases at `0x56` - radio.

## `RMC2` and `RMC4` coding
### My findings
...both **confirmed** and *anticipated*.
* `Byte 00`
  * `bit 0` - *Coding confirmation* (`1`=coded)
* `Byte 01`
  * `bit 0` - **Steering Wheel** (`0`=LHD; `1`=RHD)
* `Byte 02`
  * `bits 0-3` - **Car Body** (`0000`=sedan; `0001`=avant; `0100`=sportback, `0101`=allroad; `0110`=SUV)
* `Byte 03`
  * `bits 0-1` - **Boot screen** (`00`=default; `01`=S-Line; `10`=S; `11`=RS)
* `Byte 04`
  * `bits 0-1` - **Car Model** (`00`=A1; `01`=A6/A7; `10`=Q3)
* `Byte 05`
  * `bit 0` - **Air Condition** (`1`=installed)
  * `bit 6` - **Tire Pressure Monitoring System** (`1`=installed)
  * `bit 7` - **Ambient Illumination** (`1`=installed)
* `Byte 06`
  * `bit 1` - *Parking Sensors* (`1`=installed)
  * `bit 2` - *Rear View Camera* (`1`=installed)
  * `bit 3` - *Rain Sensor* (`1`=installed)
  * `bit 4` - *Central Lock* (`1`=installed)
  * `bit 5` - *Rear Blind* (`1`=installed)
  * `bit 6` - *Gear Recommendation / Speed Warning* (`1`=installed)
* `Byte 07`
  * `bit 6` - *Comfort Seats* (`1`=installed)
* `Byte 08`
  * `bit 0` - *Lane Assist* (`1`=installed)
  * `bit 1` - *Side Assist* (`1`=installed)
  * `bit 3` - *Pause Recommendation* (`1`=enabled)
* `Byte 09`
  * `bit 4` - *Tow bar* (`1`=installed)
* `Byte 12`
  * `bits 0-1` - *Radio Antenna* (`01`=A6/A7 specific; `02`=with Sirius; `03`=A1/Q3 specific)
* `Byte 14`
  * `bit 0` - *Sound System* (`0`=Internal; `1`=External)

### To investigate
* `Byte 05`:`bit 5` OR `Byte 07`:`bit 5`
*Something A6 Allroad related* (*Air Suspension?* OR *Tilt Display?*)
* `Byte 08`
  * `bit 6` - *Reverse Seatbelt Tensioner (RGS)?* (`1`=installed)
* `Byte 10`
  * `bit 1` - *APS/RVC* (`1`=installed)
  * `bit 2` - *???* (`0`=A1/Q3; `1`=A6/A7)
* `Byte 11`
  * `bit 0` - *Mic drivers side?* (`1`=installed)
  * `bit 1` - *Mic passengers side?* (`1`=installed)
* `Byte 16`
  * `bit 0` - *Looks like GPS related (100% accuracy in A1/Q3, not so good match in A6/A7)*

## `RMC2` and `RMC4` Adaptation
...both **confirmed** and *anticipated*.
* `005` - **developer mode** (`0`=off; `1`=on)
* `009` - *bluetooth* (`0`=off; `1`=on)
* `023` - *display test pattern* (`0`=off; `1`=on)
* `034` - *Door speaker channel test*
* `035` - *Voice Command test*
* `058` - *Speakers test* (`0`=off; `1`=on)

## `RMC2` and `RMC4` Datasets
Audi `RMC2` and `RMC4` features and settings in EEPROM (confirmed, *anticipated*, and *unknown*).

| Function | `RMC2` address | `RMC4` address |
| --- | :---: | :---: |
| Config: MOST | *N/A* | `0xF00000` |
| Config: General system settings | `0xF00000` | `0xF00100` |
| Config: Hands-Free Profile (HFP) | `0xF00100` | *N/A* |
| Config: BlueTooth (BT) | `0xF00200` | *N/A* |
| Config: Phone | `0xF00300` | *N/A* |
| Config: NAD, HFP, BT | *N/A* | `0xF00300` |
| Config: UMTS | *N/A* | `0xF03C00` |
| Config: Vehicle platform | `0xF00400` | `0xF00500` |
| Config: Bus assignment | `0xF00800` | `0xF03600` |
| Config: Speech Dialog System (SDS) | `0xF01300` | --- |
| Config: WLAN | *N/A* | `0xF03A00` |
| CarMenu: Active Cruise Control (ACC) | `0xF00500` | `0xF00600` |
| CarMenu: Interior lights (ambient illumination) | `0xF00510` | `0xF00610` |
| CarMenu: Audi Parking System / Rear View Camera (APS/RVC) | `0xF00520` | `0xF00620` |
| CarMenu: Braking Way Reduction (AWV) | `0xF00530` | `0xF00630` |
| CarMenu: Lane departure warning (LDW/HCA) | `0xF00540` | `0xF00640` |
| CarMenu: Lane Change Assist (SWA) | `0xF00550` | `0xF00650` |
| CarMenu: Exterior Lights (CH/LH/DRL) | `0xF00560` | `0xF00660` |
| CarMenu: Battery level | `0xF00570` | `0xF00670` |
| CarMenu: Windows | `0xF00580` | `0xF00680` |
| CarMenu: Air Condition (AC) | `0xF00590` | `0xF00690` |
| CarMenu: On-board Computer (TripComputer/Kombi) | `0xF005A0` | `0xF006A0` |
| CarMenu: Tyre Pressure Monitoring System (TPMS/RDK) | `0xF005B0` | `0xF006B0` |
| CarMenu: Wiper Service Position + Rain Sensor | `0xF005C0` | `0xF006C0` |
| CarMenu: Service Intervals (SIA) | `0xF005D0` | `0xF006D0` |
| CarMenu: Comfort Seats (memory) | `0xF005E0` | `0xF006E0` |
| CarMenu: Central Lock | `0xF005F0` | `0xF006F0` |
| CarMenu: Compass | `0xF00600` | `0xF00700` |
| CarMenu: Audi Drive Select (ADS/Charisma) | `0xF00610` | `0xF00710` |
| CarMenu: Oil Level | `0xF00620` | `0xF00720` |
| CarMenu: VIN + Keys learned | `0xF00630` | *N/A* |
| CarMenu: VIN | *N/A* | `0xF00730` |
| CarMenu: Keys learned | *N/A* | `0xF00840` |
| CarMenu: Clock | `0xF00640` | `0xF00740` |
| CarMenu: Air Suspension | `0xF00650` | `0xF00750` |
| CarMenu: Head-Up Display (HUD) | `0xF00660` | `0xF00760` |
| CarMenu: ZEM (Central Unit settings) | `0xF00670` | `0xF00770` |
| CarMenu: Hybrid | `0xF00680` | `0xF00780` |
| CarMenu: On-board manual | *N/A* | `0xF00790` |
| CarMenu: Stand heating / Aux heater (Webasto?) | `0xF00690` | `0xF007F0` |
| CarMenu: Universal Garage Door Opener (HomeLink/UGDO) | `0xF006A0` | `0xF007A0` |
| CarMenu: Sideview Camera | `0xF006B0` | `0xF007C0` |
| CarMenu: Night Vision | `0xF006C0` | `0xF007B0` |
| CarMenu: Reverse Seatbelt Tensioner (RGS) | `0xF006D0` | `0xF007D0` |
| CarMenu: Driving School Mode (DSM) | `0xF006E0` | --- |
| CarMenu: Custom button MFSW (Joker) | `0xF006F0` | `0xF007E0` |
| CarMenu: Daylight Saving Time | `0xF00700` | `0xF03500` |
| CarMenu: Tilt Angle display (Offroad display) | `0xF00710` | `0xF00850` |
| CarMenu: Traffic Sign Recognition (VZE) | *N/A*  | `0xF00810` |
| CarMenu: Rear Seat Entertainmant (RSE) | *N/A* | `0xF00820` |
| CarMenu: Weariness recognition (MKE) | `0xF00720` | `0xF00830` |
| Media: Audi Music Interface (AMI) and USB | `0xF00A00` | *N/A* |
| Media: AMI BT (A2DP audio streaming) | `0xF00B00` | *N/A* |
| Media: Analog Audio (AUX input) | `0xF00C00` | *N/A* |
| Media: Import (coping and ripping) | *N/A* | `0xF00400` |
| Media: AMI, A2DP, AUX | *N/A* | `0xF01000` |
| Audio: Speakers diagnostics | `0xF01500` | *unknown* |
| Audio: Sound parameters | `0xF01600` | *unknown* |
| Audio: Speakers configuration | `0xF02500` | *unknown* |
| Audio: Input gain offset | --- | `0xF03B00` |
| Regional: default units | `0xF00900` | --- |
| Regional: speed limits (VIM) | `0xF00D00` | `0xF01100` |
| Regional: system language | `0xF00F00` | `0xF03000` |
| Regional: visible languages | `0xF01100` | `0xF03100` |
| Regional: country setting | --- | `0xF03700` |
| Regional: emergency number | --- | `0xF03800` |
| Navigation activation code (FEC/FSC) | `0xF01400` | `0xF10000` |

### Checksums
* Last 2 bytes is checksum. It's generated with CRC16-CCITT(FALSE).
* Example: 3 bytes `00 E1 F0` contain value `00` and checksum `E1 F0`.

Example function activation - parameterization with OBDeleven for Android
* Demo https://youtu.be/jsi80Yr3aoY

## Live Data
| Channel | Data1 | Data2 | Data3 | Data4 |
| --- | :---: | :---: | :---: | :---: |
| 016 | CD drive temp. | ??? | Cooling fan RPM | N/A |
| 019 | Up time | ??? | ??? | ??? |

## BAP
Features available on RMC screen that are coding in other modules and information about it is send over BAP.

## GEM - Green Engineering Menu
### Usage
* Requires developer mode to be enabled first (check adaptation above).
* Enter GEM with key combination: **[CAR]** + **[MENU]**
* Demo: https://youtu.be/jGcJXQZLzEc

### Custom GEM screens
*coming soon...*

## REM - Red Engineering Menu
* Enter REM with key combination: **[CAR]** + **[BACK]**
* Demo: https://youtu.be/PRefnQfClug

## System reboot
* Enter it with key combination: **[BACK]** + **[Control Wheel]** + **[Upper-Right]**
* Demo: https://youtu.be/KxOsZpEe3cY

## Display screenshot
* Make sure there's an SD card inserted and it's not write protected.
* Press and hold buttons **[<]** and **[>]**.
* Wait for LED confirmation on the control panel.
* Demo: https://youtu.be/ASmqbM54rZk

## RMC filesystem access
*coming soon...*

## Credits, Reference, Tools
* Huge thanks to everyone involved in this research!
* Equipment code search engine: http://prsearch.planetvag.com
* Checksum calculator: https://crccalc.com
* RMC2 vw RMC4, optional equipment reserach: https://www.drive2.ru/l/7508336/
* ASCII table: https://www.rapidtables.com/code/text/ascii-table.html
* OBDeleven diagnostic interface (ref link): http://obdeleven.com/?src=link&ref=Zy245Iacqc6bMTHh
