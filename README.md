# A2C_DVI_Prototype

This is a prototype of an adapter to let an Apple IIc use an A2DVI card. 4/15/25

USE AT YOUR OWN RISK.   MIT LICENSE

This has only been tested with an A2DVI v2 card and a 8BitDevices A2DVI V3 DVI/HDMI ( https://www.8bitdevices.com/product/a2dvi/ ).  I don't think the firmware will work on a v4 card, I have one on order to try.

BACKGROUND

I have been working on a project using an ESP32-C6 to take the digital video signals from the Apple IIc DB15 video connector and allow remote viewing of the screen on a PC (watch this account for the ViewIIc plans).   The circuit design was pretty simple, a DB15 connector, a 74VLC245 for level conversion (5V to 3.3V) and a ESP32-C6 module.   It occured to me that I could take those same Apple IIc signals and using the picoDVI libraries create a IIc to HDMI solution using an RP2040 or RP2350 (Raspberry Pi Pico).   This is the same HW that is on an A2DVI card for a slotted Apple II (RP2040 and 245's).  The Protype takes the A2DVI card out of the machine and instead of connecting to Apple II bus signals (address, data, etc), we feed the Apple IIc digital video signals into the cards pins and use custom firmware to recreate the display out to HDMI.

PROTOTYPE

The prototype is pretty simple.   A male DB15 connector, with wires to a breadboard, holding a 50-pin slot for the A2DVI card to plug into.  It also has a button/resitors to access the config menu and a 7805 regulator to convert +12V on the DB15 to +5V for the card.  You can power the card from a USB connection, but you need a +5V to make the config button work.  The +5V pin on the slot is protected by a diode, so it doesn't produce +5V when you are plugged into USB.  You could solder on a wire to the 5V pin on the pico and do away with teh 7805, but I didn't want to modify the card and I'd like it to be self powered.

SCHEMATIC:
I'm also building a small PCB board that integrates all of this (watch for that Board project on this account).   This is the schematic for the board, which is pretty much the same scematic as the Prototype (ignore the power connector and ground 42 and 43).

WIRING:
Take one of the breadboard modules and remove the power rails on one side.   Take the 50-pin slot connector and plug it into the edge with one row of pins in the breadboard and the other row hanging off the edge.  This is a little weird, but it was the easiest way to do it and other than +5V, all of the pins we need are on one side.

Cut the female ends off 7 of the female to male wires that come with the breadboard.  Strip the ends to use with the DB15 connector.  Wire as follows.  A2C is the DB15 connector and A2E is the 50 pin slot with pin 50 being at the right of the connector (looking across the breadboard).

PIN_SEROUT  //  A2C Pin 11 - A2E Pin 49
PIN_14M     //  A2C Pin 2  - A2E Pin 48
PIN_WNDW    //  A2C Pin 7  - A2E Pin 47
PIN_TEXT    //  A2C Pin 1  - A2E Pin 46
PIN_GR      //  A2C Pin 10 - A2E Pin 45
PIN_GND     //  A2C Pin 13 - Breadboard ground rail.  Connect ground to A2E Pin 26 (the left most pin connected to the breadboard)
PIN_+12V    //  A2C Pin 8 - Unconnected Breakboard location for the 7805 circuit (other side of the breadboard from the 50-pin slot)

To load the firmware use a USB cable to your PC/Mac with the A2DVI card not slotted into anything.   There is a BOOTSEL button on the pico module.  Hold that button down, and while holding it, plug the USB cable into your PC.   You should see a volume appear on the PC/Mac.  Copy the "A2C_DVI_v1.7.1.uf2" file to this volume and the card should update and reboot.   If you have a HDMI monitor attached to the card, you should see the A2C_DVI splash screen.  Unplug the card from USB.  Never Hotplug the card in the slot or the DB15 conenctor to the Apple IIc.

At this point, you can ground A2E pins 42, 43, 44, slot in the A2DVI card with components facing away, plug the DB15 into your IIc and plug the card into USB power.  If everything is wired correctly, you should see Apple IIc video on your HDMI monitor.

7805 and Button
Follow the schematic on how to conenct the 7805 and the 2 capacitors to the +12V line.  Take the 7805 +5V output and using a male to female wire, hook the female end onto pin 25 of the 50-pin slot, this pin will be in the upper left, hanging off the edge of the bread board.

For the Button, unground pin 44 from the slot and connect a wire there.  The circuit for the button is:
+5V -> 1k resistor -> Button -> Line to pin 44 -> 10k Resistor -> GND

BOM:

You can certainly source these components from places like DigiKey or Mouser for a lot less, but I'm just listing the Amazon links because yuo can typically get them overnight.

DB15: https://www.amazon.com/dp/B07JPHR9JZ

Breadboard: https://www.amazon.com/dp/B08Y59P6D1

Button: https://www.amazon.com/dp/B07QH9WV12

7805 Regulator: https://www.amazon.com/dp/B0BRV3HTXY

Resistors: https://www.amazon.com/dp/B0CDWW5BFH

50-pin slot: https://www.amazon.com/dp/B0BPP5794Z

USAGE:

With the 7805 working, the card should power on when you turn on you IIc.  To access the config menu, you make a long press on the button.   Short presses to navigate the menus and long presses to select an option.  Long press on Save to store the settings for subsiquent boots.

ISSUES:

This is just a prototype and proof-of-concept.  USE AT OWN RISK.

The 1.7.1 firmware has known issues with double high res (dhgr).

COMING SOON:

A PCB version of the prototype using through hole parts for hobbyists to assemble.

The firmware source code.

Hopefully someone will take the idea and build a Iic specific turnkey card.


SPECIAL THANKS:
Chris Auger ( https://www.8bitdevices.com/product/a2dvi/ )
Jonathan Adar
Jawaid Bazyar
Ralle Palaveev ( https://github.com/rallepalaveev/A2DVI )
Thorsten Brehm ( https://github.com/ThorstenBr/A2DVI-Firmware )


Pictures:

Wiring:
![IMG_9583](https://github.com/user-attachments/assets/db2454a1-fe21-46ba-a97c-f622e7adc96e)

Hanging 25 over the edge:
![IMG_9584](https://github.com/user-attachments/assets/aacbc47c-f8d5-4ea8-af98-b17cc606463b)

Config screen:
![DEFAULT](https://github.com/user-attachments/assets/00f029e0-050e-4da7-86ac-1dbc8562bdf5)

DP15 Pinouts
![IMG_8899](https://github.com/user-attachments/assets/4d250206-9c86-4687-9743-096d6ff55ef8)

7805 Circuit:
![image](https://github.com/user-attachments/assets/ae684c7b-1a18-4d3e-9874-b82fae98b99a)




