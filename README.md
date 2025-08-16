# A2CDVI_SMD

This is a project for a digital DVI/HDMI video cards for Apple IIc or IIc+. It directly produces a digital video stream from the Apple IIc's digital video output connector. The signal is output via an HDMI connector, connecting the Apple IIc to modern displays with HDMI (or DVI) inputs. No more analog signal conversion required.

![A2CDVI v2.1.0 Board](https://github.com/MrTechGadget/A2C_DVI_SMD/blob/1c6c0517c162baf9940b768525fd8b74470f6342/A2C_DVI_2.1.0_Hires.jpg)

## BACKGROUND
### Mike Neil's [Inspiration](https://github.com/FarLeftLane/A2C_DVI_Board)
> I have been working on a project using an ESP32-C6 to take the digital video signals from the Apple IIc DB15 video connector and allow remote viewing of the screen on a PC (watch this account for the ViewIIc plans).  The circuit design was pretty simple, a DB15 connector, a 74VLC245 for level conversion (5V to 3.3V) and a ESP32-C6 module. It occured to me that I could take those same Apple IIc signals and using the picoDVI libraries create a IIc to HDMI solution using an RP2040 or RP2350 (Raspberry Pi Pico). This is the same HW that is on an A2DVI card for a slotted Apple II (RP2040 and 245's). The Protype takes the A2DVI card out of the machine and instead of connecting to Apple II bus signals (address, data, etc), we feed the Apple IIc digital video signals into the cards pins and use custom firmware to recreate the display out to HDMI.

## HARDWARE
### Protoype

My first version was designed from Mike's schematic and mapping those through the the needed components found on the A2DVI card itself. It utilized a Raspberry Pi Pico device for simplicity, but the overall size was too big and it blocked access to the composite video

### Version 2

Inspired by the working prototype, I decided I could make it MUCH smaller by implementing the RP2040 directly on the board. 

### Version 2.5

Fixed compatibility issues with some HDTVs and added hardware support for Mike Neil's latest firmware features!

## Availability

This card is available for purchase in the US for $35 plus shipping on my Tindie Store [MrTechGadget's Gadgets](https://www.tindie.com/products/mrtechgadget/a2cdvi/)

## Flashing Firmware
The latest firmware can be found on Mike Neil's [A2C_DVI_Firmware repo](https://github.com/FarLeftLane/A2C_DVI_Firmware/tree/master/Releases)

To load the firmware use a microUSB cable to your PC/Mac with the A2CDVI card plugged into the Apple IIc. It is the exact same process as flashing a Raspberry Pi Pico. There is a small BOOTSEL button in the middle of the board close to the DA15 connector, above the word HOTPLUG.  Hold that button down, and while holding it, plug the USB cable into your PC/Mac.  You should see a volume appear on the PC/Mac.  Copy the "A2C_DVI_v1.7.6.uf2" file to this volume and the card should update and reboot.   If you have a HDMI monitor attached to the card, you should see the A2C_DVI splash screen.  Unplug the card from USB.  Never Hotplug the DA15 connector to the Apple IIc.


**SPECIAL THANKS**

- Mike Neil ( https://github.com/FarLeftLane/ )
- Ralle Palaveev ( https://github.com/rallepalaveev/A2DVI )
- Thorsten Brehm ( https://github.com/ThorstenBr/A2DVI-Firmware )
- David Kuder ( https://github.com/V2RetroComputing/analog )

