# App-controlled LED strip

An LED strip controller built on the Arduino UNO R4 WiFi, with remote control via Arduino Cloud - Circuit plan, PCB files, and firmware.

## Overview
This project demonstrates a universal LED strip controller that works independently of the strip manufacturer. The system is powered by an Arduino UNO R4 WiFi and integrates with the Arduino Cloud, enabling wireless configuration and control from any device.

## What I did
- Schematic & PCB (EasyEDA)
- Firmware (Arduino, C C++)
- BOM, test rig and performance measurements

## Files
- `hardware/LED-strip-schematic.pdf` — printable schematic  
- `hardware/Gerber_Transistor_Circuit.zip` — Gerber file for fabrication
- `hardware/pcb_front` `hardware/pcb_back` — 3D Model of PCB
- `firmware/src.md` — source code
- `firmware/Get_HEX_Codes.md` — test to find out HEX-codes of remote control
- `docs/` — pictures 

## License
Firmware: MIT  
Hardware: CERN-OHL-P
