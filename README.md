# attiny-neopixel-flasher
quick and dirty lipo + neopixel flasher making use of parts on hand

## Circuit
Power provided by a lipo battery using a 1mm pitch 4-pin jst connector.
Power connects to the ATTINY85 and neopixels
Button connects to reset - the ATTINY keeps track of which pattern it's on in eeprom, and plays the next one at reset.

## Power saving hack
WS2182's consume 1mA when off, discharging the 1000mAh pack in a day, so now I power them with ATTINY GPIO pins. ATTINY GPIO pins provide max 40mA each 60mA combined, so I scratched off the trace and soldered a bodge wire to two pins (2+3) and the vcc pin of the neopixel ring

## PCB
Using all built-in footprints, manually placed 1x1 headers for connection to the 16-neopixel rings i have on hand. Optimized for milling with fat bits, so i removed pins 2,3,6,7 from the attiny footprint. Still need to use a V bit to get the space between the power connector pins but the rest is 1/32" flat end. Sized to match the batteries i had lying around.

## Software
Based on adafruit's neopixel strandtest with minor additions:
* use EEPROM to store/load state on reset
* choose patterns based on switch statement of eeprom state
* looped patters to each last ~60s
* use sleep.h features to go to sleep after pattern runs through
* toggle pins 3&4 to provide power for neopixels
* added rainbowall pattern to do same rainbow color to all leds
Used Arduino IDE with https://github.com/SpenceKonde/ATTinyCore for attiny85 support.
