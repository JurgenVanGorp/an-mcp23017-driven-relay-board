Guide creation date: 13-Nov-2021

# an-mcp23017-driven-relay-board
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

![alt text](https://github.com/JurgenVanGorp/MCP23017-multi-IO-control-on-a-Raspberry-Pi-with-I2C/blob/main/mcp23017control/mcp23017monitor.png "Example monitor view.")

The GERBER PCB Files are included in the package, so you don't need to compile these for yourself.







Next topic: [A sensor (relay) board for sensing 240V high power states with an MCP23017.](https://github.com/JurgenVanGorp/an-MCP23017-driven-high-voltage-sensor-board)