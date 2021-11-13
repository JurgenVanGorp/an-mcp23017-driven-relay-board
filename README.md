Guide creation date: 13-Nov-2021

# An MCP23017 driven relay board for Home Assistant on a Raspberry Pi
A schematic and hardware board for an MCP23017 multi-I/O controller driven relays.

Previous topic: [Step 4: Controlling the MCP23017 from within Home-Assistant.](https://github.com/JurgenVanGorp/MCP23017-multi-I-O-Control-with-Raspberry-Pi-and-Home-Assistant)

## Introduction

In the previous topics it was shown how an MCP23017 can be used for controlling toggle relays with an MCP23017 multi-I/O chip. The examples made use of an MCP23017 chip on a breadboard. For real life usage we will need a PCB that can be properly installed in a rack.

This guide describes a simple PCB board in Eurocard format (10cm x 16cm) that allows connecting an MCP23017 to a Raspberry Pi with Home Assistant, over the I2C bus. The board has 15 open ended relays. The 16th output is used to drive an "identification" LED. It can be used to identify the board if you are using multiple boards, and for verification that the communication is working properly.

The board needs a 12V power supply. The 12V is converted to 5V on the board, and is also used to power the mini relays. With some modifications you can also use the board with 5V directly, but you would need to replace the relays with pin-compatible 5V relays. I am using 12V for the simple reason that all switches in my house operate on 12V. The translation to higher voltages is only done in the power box.

**WARNING** Even though the PCB board described below does provide you with physical segregation with relays, IT IS NOT SUITED FOR HIGH VOLTAGE OR HIGH CURRENT USE. The low voltage and high voltage lines on the PCB are not sufficiently separated on the PCB for safe use with high voltages. The board can be used with low-voltage (max 48V) toggle relays (aka teleruptors) at a maximum of 500 milliAmps.

## Using and changing the files in this repository

I have created the schematic and PCB in this repository with the open and free [KiCad EDA](https://www.kicad.org/) software. I cannot express enough how much I am grateful to [the developers](https://www.kicad.org/about/kicad/) of this PCB software. As far as I'm concerned the times of too-expensive PCB software are over.

The PCB file looks as follows.

![alt text](https://github.com/JurgenVanGorp/an-mcp23017-driven-relay-board/blob/main/images/PCB_Overview.png)

The GERBER PCB Files are included in the package, so you don't need to compile these for yourself.

There are many companies that will be able to create the PCB files for you. My personal favorite is [Eurocircuits.eu](https://www.eurocircuits.com/), but that's a personal choice of course. You can also create your own PCBs; the PDF file is added in the repository. But let's be honest, ordering the PCB looks a lot more professional and will last longer.

![alt text](https://github.com/JurgenVanGorp/an-mcp23017-driven-relay-board/blob/main/images/DriverPCB.png)

**INFO** In honnesty: the image above does not fully match the PCB you can find in the repository. In this prototype I made use of RJ10 connectors for the I2C connections, but these connectors are difficult to find. If you find one, it will probably have a slightly footprint. For that reason I used 'standard' 3-pin connectors in the final PCB layout.

## Components used.

This is the list of components used, and where I have found them.

| Quantity | Component    | Value                     | Source                 | Cost Estimate |
|:--------:|--------------|--------------------------:|------------------------|--------------:|
| 1        | IC           | MCP23017                  | [mouser.com](https://eu.mouser.com/ProductDetail/Microchip/MCP23017-E-SP?| 2        | Resistor     | 470 |  |  | 
| 16       | Diode        | 1N4007 | [conrad.com](https://www.conrad.com/p/diotec-si-rectifier-1n4007-do-204al-1000-v-1-a-162272) | € 0.09 | 
| 15       | Resistor     | 4K7 | [conrad.com](https://www.conrad.com/p/tru-components-tc-mf0w4ff4701a50203-metal-film-resistor-47-k-axial-lead-0207-025-w-1-1-pcs-1585059) | € 0.10 | 
| 1        | Capacitor    | 22nF  | [conrad.com](https://www.conrad.com/p/tru-components-tc-k22nf5-ceramic-capacitor-tht-22-nf-100-v-20-1-pcs-1589451) | € 0.10 | 
| 3        | Capacitor    | 220nF | [conrad.com](https://www.conrad.com/p/kemet-c320c224m5u5ta-ceramic-capacitor-radial-lead-220-nf-50-v-20-l-x-w-x-h-508-x-318-x-584-mm-1-pcs-1420328) | € 0.60 | 
| 2        | Capacitor     | 220uF | [conrad.com](https://www.conrad.com/p/europe-chemicon-eky-500ell221mj16s-electrolytic-capacitor-radial-lead-5-mm-220-f-50-v-20-x-h-10-mm-x-16-mm-1-pc-1505568) | € 0.50 | 
| 15       | Transistor   | BC547 (***) | [conrad.com](https://www.conrad.com/search?search=bc547&searchType=regular) | € 0.20 | 
qs=sGAEpiMZZMsVgcksf1EMUq%252Bl%252ByrW%252Br2s) | € 1.30 | 
| 1        | 12V to 5V DC | OKI-78SR-5_1.5-W36H-C (*) | [mouser.com](https://eu.mouser.com/ProductDetail/Murata/OKI-78SR-5-15-W36H-C?qs=sGAEpiMZZMsbRVlHDoeFZD%252BySXGErvIJc3su7QBo1Is%3D) | € 3.64 | 
| 15       | Relay 12V    | G5V-1-DC12 (**)           | [mouser.com](https://eu.mouser.com/ProductDetail/Omron/G5V-1-DC12?qs=sGAEpiMZZMv0NwlthflBi%2Fae0vpIDW5L) | € 8.00 |
| 3        | Jumper       | N/A      | e.g. [conrad.com](https://www.conrad.com/p/tru-components-shorting-jumper-contact-spacing-254-mm-pins-per-row2-content-100-pcs-1693950) | € 0.35 | 
| 1        | Connector    | 1 x 2    |  |  | 
| 2        | Connector    | 1 x 3    |  |  | 
| 5        | 1x6 Spring connector | PTR 54191060051E | [conrad.com](https://www.conrad.com/p/ptr-54191060051e-spring-loaded-terminal-075-mm-number-of-pins-6-pebble-grey-1-pcs-569770) | € 0.36 | 
| 1        | LED "IDENT"  | Green 5 mm |  | € 0.20 | 
| 1        | LED "POWER"  | Red 5 mm |  | € 0.20 | 

(*) The OKI-78SR is a 12V DC to 5V DC converter. It is pin-compatible with an [LM7805](https://eu.mouser.com/ProductDetail/Texas-Instruments/LM7805CT?qs=sGAEpiMZZMsFKQfwwdJx%2FxW4Tr%252BxPyoqmeSSFfZw3i4%3D). The current drawn is very low, so feel free to replace it with an LM7805 if you prefer.
(**) You can also power the board with 5V. In that case you will need to bridge the DC/DC converter and replace the 12V relays with the 5V [G5V-1-DC5 version](https://eu.mouser.com/ProductDetail/Omron/G5V-1-2-DC5?qs=sGAEpiMZZMsKEdP9slC0YbH1hXJZnuIH7AhUMezYhKg%3D).
(***) Also known as 2N3904 / BC547 / PN2222 / 2N4401 / NTE123AP. Make your pick, this is a "standard" NPN transistor. 

The assembled board should look something like the following. Please mind that the below board is the prototype and looks slightly different from the PCB.

![alt text](https://github.com/JurgenVanGorp/an-mcp23017-driven-relay-board/blob/main/images/DriverPCBassembled.png)



Next topic: [A sensor (relay) board for sensing 240V high power states with an MCP23017.](https://github.com/JurgenVanGorp/an-MCP23017-driven-high-voltage-sensor-board)