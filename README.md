# usb2retroconsole-fw
Work-in-progress Pi Pico (RP2040) based adapter to use USB controllers on a retro consoles.

Use a USB-OTG adapter to connect a controller to the pico's usb port.

Some firmwares have alternative modes of operation that can be changed in real time.<br/>
To change mode, hold the "mode change button" and press A, B, X or Y (input follows the xinput layout)

"Mode change button" changes depending on the device being used and it's buttons.<br/>
It follows this priority: HOME, START+SELECT, START.<br/>
IE: If a device contains a HOME button, use that. If the device only have START, use that.

Some adapters have an alternative firmware for Fightstick.<br/>
It's best fit for using a fightstick as input or a controller that follows the "modern" fightstick mapping.

Advice:
- NEVER connect it to the console and to a usb host (ie: a PC) at the same time.
- Connect the controller and adapter to the console while the console is still powered off.
- Do not use a power hungry controller. IE: a DualSense.
- If you're going to use a controller that contains an internal battery, make sure to fully charge it before using. You don't want it to be charged by the console's controller port.

Firmware and wiring directions are provided to you 'as is' and without any warranties. Use at your own risk.

There's adapters for: <br/>
- [Snes](#usb-to-snes-adapter)
- [Megadrive](#usb-to-megadrive-adapter)
- [Saturn](#usb-to-saturn-adapter)
- [PSX](#usb-to-psx-adapter)

## USB to SNES Adapter

| SNES     | GPIO | Other                     |
|----------|------|---------------------------|
| 7 - GND  | GND  |                           |
| 1 - VCC  | VBUS |                           |
| 2 - CLK  | 0    |                           |
| 3 - LAT  | 1    |                           |
| 4 - DAT1 | 2    |                           |
| 5 - DAT2 | N/C  |                           |
| 6 - SEL  | 6    | **Optional / for rumble** |

| 1 2 3 4 | 5 6 7 )

**All data pins must be level shifted!**<br/>
Pico's GPIO runs at 3.3v and snes runs at 5v.

## USB to Megadrive Adapter

| MegaDrive | GPIO |
|-----------|------|
| D0        | 0    |
| D1        | 1    |
| D2        | 2    |
| D3        | 3    |
| TL        | 4    |
| TR        | 5    |
| TH        | 6    |
| VCC       | VBUS |
| GND       | GND  |

**All data pins must be level shifted!**<br/>
Pico's GPIO runs at 3.3v and megadrive runs at 5v.

Modes
- 6 button pad (led on)
- 3 button pad (led blink fast)
- Twinstick for xenocrisis (led blink slow)
- Cyberstick (led blink slow). This mode is bugged!

## USB to Saturn Adapter

| Saturn | GPIO |
|--------|------|
| D0     | 0    |
| D1     | 1    |
| D2     | 2    |
| D3     | 3    |
| TL     | 4    |
| TR     | 5    |
| TH     | 6    |
| VCC    | VBUS |
| GND    | GND  |

**All data pins must be level shifted!**<br/>
Pico's GPIO runs at 3.3v and saturn runs at 5v.

Usable mode depends on the input controller type:

- Digital Input
  > Digital (led on)
- Dual Stick Input
  > 3D Digital (led on)<br/>
  > 3D Analog (led blink fast)<br/>
  > Twinstick (led blink slow)<br/>
- Racing Wheel Input
  > Wheel (led on)<br/>
  > 3D Analog (led blink fast)<br/>
- Joystick Input
  > Mission Stick 3 Axis (led on)<br/>
  > 3D Analog (led blink fast)<br/>
- Mouse Input
  > Shuttle Mouse (led on)




## USB to PSX Adapter

| PSX      | GPIO  | Other                    |
|----------|-------|--------------------------|
| 4 - GND  | GND   |                          |
| 5 - 3.3V | VBUS* | **Check details bellow** |
| 1 - DAT  | 11    |                          |
| 2 - CMD  | 12    |                          |
| 3 - 9V   | VBUS* | **Check details bellow** |
| 6 - ATT  | 21    |                          |
| 7 - CLK  | 10    |                          |
| 8 - INT  | N/C   |                          |
| 9 - ACK  | 22    |                          |

USB devices requires 5v to operate.<br/>
PS1 and PS2 consoles supply 3.3v and 9v (7.5v or 9v, not sure) at the controller port.
Must convert 3.3v or 9v to 5v.<br/>
Select one pin to use and do not connect the other. Either pin 3 (9v) or pin 5 (3.3v), then step up or down the voltage to 5v.<br/>
I believe using pin 9 is ideal, as it's the pin that drives the rumble motors on a dualshock controller.

Do not connect it to a multitap.

It should work on PS1 and PS2 consoles. But was only tested on PS2.<br/>
It might be incompatible with memorycards on PS1 if connected to the same input port. Be advised that card data corruption might happen.

Usable mode depends on the input controller type:

- Digital Input
  > Digital (led on)
- Dual Stick Input
  > DualShock 2 (digital) (led on)<br/>
  > DualShock 2 (analog) (led blink fast)<br/>
  > Analog stick (led blink slowsest)<br/>
  > Negcon (led blink slow)<br/>
- Racing Wheel Input
  > Negcon (led blink slow)<br/>
- Joystick Input
  > Analog stick (led blink slowsest)<br/>
- Mouse Input
  > Mouse (untested) (led on)
