# ZX Bus Adapter - Spectrum peripheral RC2014 interface card

This is an adapter card to connect Spectrum 48K/128K devices to the RC2014 bus. The primary purpose is to use standard devices with the ZX128 Spectrum board [(link)](https://github.com/ZXQuirkafleeg/ZX128).

It is not a complete implementation as some signals, such as video and +2A/+3 ROM control, are not available on the RC2014 system.

Notable features are:

*	Two edge connectors - one native and one through a riser board
* Separate power inputs for +9, -5, +12 and -12V supplies
* Jack socket for more common +9V supply (centre +ve or -ve)
* Interface 2 compatible ROM socket
* Optional inverted clock and IORQGE generation

![ZX128 Development system](https://github.com/ZXQuirkafleeg/ZX-Bus-Adapter/blob/main/Images/ZX%20Expansion%20V1.0%20-%20front.jpg)

## Edge Connectors

The top of the board has a standard Spectrum edge connector.

An additional edge connector or dupont test connection can be created by populating the white connector with pin header socket.  Using the Project Speccy [(link)](https://projectspeccy.com/projects/) horizontal adapater [(link)](https://projectspeccy.com/Projects/Horiz_Ext/Spectrum_Backplane_Horizontal_Adaptor-KiCad.zip) should give a second edge connector - though this is untested.

## Power Supply

The 5V supply is provided from the RC2014 bus.  However, should other voltages be needed these can be provided via J6.  CN1 is a jack socket for providing a more usually required 9V supply (e.g. Currah Microspeech and Microdrives), and centre -ve (Sinclair) or centre +ve supplies (almost everything else) can be selected by setting J5.

There is no protection on the power supply inputs.  All of the usual Spectrum rules about connecting/disconnecting devices when the power is off apply.

## Cartridge Socket

The cartridge slot provides an Interface 2 compatible socket.  There's a wealth of details of the mechanism and how to expand it beyond 16K on fruitcake's website [(link)](http://www.fruitcake.plus.com/Sinclair/Interface2/Cartridges/Interface2_RC_Cartridges.htm).  Simple ROM PCBs can be found [here](https://github.com/mosaicmap/ZXS_I2_kartridz) and [here](https://trastero.speccy.org/cosas/droy/zxflash/zxflashcart_e.htm).

## Inverted clock and IORQGE

Some peripherals may need an inverted CPU clock and IORQGE.  Should it be needed, fitting U2 will invert the CPU clock at the edge connector.  Either clock or inverted clock is selected using J4.  U2 is not needed for a non-inverted clock 

Fitting U2 will also create the edge connector IORQGE signal should it be needed.  Note - this is output only and cannot be used to disable the ULA I/O ports as per a standard spectrum.  

## Build
All components are though-hole and standard density.  A schematic can be found [here](https://github.com/ZXQuirkafleeg/ZX-Bus-Adapter/blob/main/PCB/ZX%20Expansion%20-%20Schematic%20-%20V1.0.pdf) and BOM here [here](https://github.com/ZXQuirkafleeg/ZX-Bus-Adapter/blob/main/PCB/BOM%20-%20ZX%20Expansion%20Adapter%20-%20V1.0.csv).

### PCB

For the PCB, EasyEDA (V6.5.22) design files can be found [here](https://github.com/ZXQuirkafleeg/ZX-Bus-Adapter/tree/main/PCB) and gerbers [here](https://github.com/ZXQuirkafleeg/ZX-Bus-Adapter/blob/main/PCB/Gerber_PCB_RC2014%20-%20ZX%20Adapter_2022-09-17%20V1.0.zip).  The PCB is a standard two layer board approx. 100mm by 60mm.  

### Cartridge Socket

The ROM socket is a 30 pin 2.54 edge connector socket.  Pin 5 (upper and lower) are removed and replaced with an edge connector key.  A 3D printable key is also on the Project Speccy site [(link)](http://projectspeccy.com/Projects/Slot_Key/Guenter_Bruetting_ZX_Slot_Key.zip).

### Optional components

Populate the power components as needed.  Simple devices like joystick interfaces generally need only 5V which is drawn from the RC2014 bus.  Sound devices generally need 9V for internal amps and regulators.  The Sinclair interface 1 needs both 9V (microdrives) and +/-12V (RS232).

U2 only need to be populated if the peripheral needs an inverted CPU clock or IORQGE (unlikely).  Otherwise simply short pins 1&2 on J4 for the non-inverted  clock. 

## Jumpers and Connectors

* J1 – RC2014 Bus connector
* J2 – RC2014 Extended bus connector (if required)
* J3 – ROMCS and NMI jumpers – used connect ROMCS to U1 and NMI to U2 of RC2014 bus
* J4 – Clock / inverted clock select
* J5 – 9V External power supply supply (CN1) centre +ve or -ve select
* J6 – External power supply connector

## System Test

Install the CPU, ZX128 and ZX bus boards in the backplane.  Connecting a kempston joystcik interface or inserting a ROM cartridge should work as expected.  Additional current draw should be that required by the peripheral only.
