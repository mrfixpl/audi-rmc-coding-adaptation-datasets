# Audi RMC: Coding, Adaptation, Datasets
* Figuring out how Audi RMC system is configurable by testing coding, adaptation, datasets, and BAP.
* This type of infotainment unit is poorly documented. I hope this is about to be changed.
* My research is based on a 2012 Audi Q3 equipped with Audi `RMC2` non-navigation unit and some parameterization files that I found over the internet.

![Audi RMC with Driving School Mode option](https://github.com/mrfixpl/audi-rmc-coding-adaptation-datasets/blob/main/research%20pictures/RMC-DrivingSchoolMode.jpg?raw=true)

## How to tell which RMC system I have?
* There are different versions of the RMC system, nav and non-nav, with 6.5" and 7" displays, pre-facelift and facelift.
* Not confirmed yet: `RMC2` and `RMC4` units are using different dataset addresses.
* Not confirmed yet: part# `4G0`/`8X0` = `H5x` = `RMC2`;
* Not confirmed yet: part# `4G1`/`8X1` = `H6x` = `RMC4`.
* There's also `H4x` option available. Not sure what it exactly is.
* Enter Red Engineering Menu and check what's your SW Train. Audi RMC system firmware starts with `rmc`.
* https://youtu.be/R2mUmxFPWBQ

## Control Module address
Depending on vehicle and unit version, RMC can be accessed via address `0x56` or `0x5F`.

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
  * `bit 7` - **Ambient Illumination** (`1`=installed)
* `Byte 06`
  * `bit 1` - *Parking Sensors* (`1`=installed)
  * `bit 2` - *Rear View Camera* (`1`=installed)
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
* `Byte 05`
  * `bit 6` - *TPMS?* (`1`=installed)
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
| --- | --- | --- |
| General Settings | `F00000` | --- |
| Hands-Free Profile (HFP) | `F00100` | --- |
| BlueTooth (BT) | `F00200` | --- |
| Phone | `F00300` | --- |
| Vehicle platform | `F00400` | --- |
| CarMenu: Active Cruise Control (ACC) | `F00500` | --- |
| CarMenu: Interior lights (ambient light) | `F00510` | --- |
| CarMenu: Audi Parking System (APS/RVC) | `F00520` | --- |
| CarMenu: Braking Way Reduction (AWV) | `F00530` | --- |
| CarMenu: Lane departure warning (LDW/HCA) | `F00540` | --- |
| CarMenu: Lane Change Assist (SWA) | `F00550` | --- |
| CarMenu: Exterior Lights (CH/LH/DRL?) | `F00560` | --- |
| CarMenu: Battery level | `F00570` | --- |
| CarMenu: Windows | `F00580` | --- |
| CarMenu: Air Condition | `F00590` | --- |
| CarMenu: On-board Computer (TripComputer/Kombi) | `F005A0` | --- |
| CarMenu: Tyre Pressure Monitoring System (TPMS/RDK) | `F005B0` | --- |
| CarMenu: Wiper Service Position + Rain Sensor | `F005C0` | --- |
| CarMenu: Service Intervals (SIA) | `F005D0` | --- |
| CarMenu: Comfort Seats (memory) | `F005E0` | --- |
| CarMenu: Central Lock | `F005F0` | --- |
| CarMenu: Compass | `F00600` | --- |
| CarMenu: Audi Drive Select (ADS/Charisma) | `F00610` | --- |
| CarMenu: Oil Level | `F00620` | --- |
| CarMenu: VIN + Keys | `F00630` | --- |
| CarMenu: Clock | `F00640` | --- |
| CarMenu: Air Suspension | `F00650` | --- |
| CarMenu: Head-Up Display (HUD) | `F00660` | --- |
| CarMenu: ZEM (Central Unit settings) | `F00670` | --- |
| CarMenu: Hybrid | `F00680` | --- |
| CarMenu: Aux Heater (Webasto?) | `F00690` | --- |
| CarMenu: Universal Garage Door Opener (HomeLink/UGDO) | `F006A0` | --- |
| CarMenu: Sideview Camera | `F006B0` | --- |
| CarMenu: Night Vision | `F006C0` | --- |
| CarMenu: Reverse Seatbelt Tensioner (RGS) | `F006D0` | --- |
| CarMenu: Driving School Mode (DSM) | `F006E0` | --- |
| CarMenu: Custom button MFSW (Joker) | `F006F0` | --- |
| *CarMenu: Daylight Saving Time* | `F00700` | --- |
| CarMenu: Tilt Angle display (Offroad display) | `F00710` | --- |
| CarMenu: Weariness recognition (MKE) | `F00720` | --- |
| Bus assignment | `F00800` | --- |
| Audi Music Interface (AMI) and USB | `F00A00` | --- |
| AMI BT (A2DP audio streaming) | `F00B00` | --- |
| Analog Audio (AUX input) | `F00C00` | --- |
| Speech Dialog System (SDS) | `F01300` | --- |
| Audio: Speakers diagnostics | `F01500` | *unknown* |
| Audio: Sound parameters | `F01600` | *unknown* |
| Audio: Speakers configuration | `F02500` | *unknown* |
| Regional: default units | `F00900` | --- |
| Regional: speed limits (VIM) | `F00D00` | `F01100` |
| Regional: default language | `F00F00` | `F03700` |
| Regional: visible languages | `F01100` | `F03100` |
| Navigation activation code (FEC/FSC) | `F01400` | *unknown* |

### Checksums ###
* Last 2 bytes is checksum. It's generated with CRC16-CCITT(FALSE).
* Example: 3 bytes `00 E1 F0` contain value `00` and checksum `E1 F0`.

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

## Credits, Reference, Tools ##
* Equipment code search engine: http://prsearch.planetvag.com
* Checksum calculator: https://crccalc.com
* RMC2 vw RMC4, optional equipment reserach: https://www.drive2.ru/l/7508336/
* ASCII table: https://www.rapidtables.com/code/text/ascii-table.html
* OBDeleven diagnostic interface (ref link): http://obdeleven.com/?src=link&ref=Zy245Iacqc6bMTHh
