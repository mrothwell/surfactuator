# Surf Actuator
Arduino GPS Surf Actuator controller 

![Surfgate](https://raw.githubusercontent.com/jonthompson/surfgate/master/surfgate.png)

An Arduino/GPS controller to automatically deploy and retract your actuator controlled DIY wake gates/tabs at apprioriate speeds.

Depends on https://github.com/SlashDevin/NeoGPS/

If you are not using an Arduino Mega 2560 you'll also need either https://github.com/PaulStoffregen/AltSoftSerial or https://github.com/SlashDevin/NeoSWSerial

# Parts List (Simple):
* Arduino Nano: https://www.amazon.com/HiLetgo-ATmega328P-Micro-controller-Development-Compatible/dp/B00E87VWY4/

If you want a screw shield instead of soldering (https://www.amazon.com/Aideepen-Terminal-Adapter-Expansion-ATMEGA328P-AU/dp/B0788MLRLK/ref=sr_1_1?ie=UTF8&qid=1527559143&sr=8-1&keywords=nano+screw+shield)

* L298N Motor Bridge (https://www.amazon.com/Stepper-Controller-Mega2560-Duemilanove-IFANCY-TECH/dp/B01GZ1QUHO  (only need 1, but a backup doesn't hurt)

* LM2596 Buck Converter (https://www.amazon.com/eBoot-LM2596-Converter-3-0-40V-1-5-35V/dp/B01GJ0SC2C (only need 1 but they are super handy and cheap)

* GPS Module with antenna (https://www.amazon.com/dp/B01MRNN3YZ) 

* Any 3 way switch you want (SPDT - not momentary) - IE: https://www.amazon.com/Blue-Sea-Systems-WeatherDeck-Toggle/dp/B000MMFJ02

* (Optional) a status LED grab one you like (7v - 12v) iE: https://www.amazon.com/dp/B013TI6CE2/ref=twister_B0150XWQ8U?_encoding=UTF8&th=1

* (Optional) A rotary encoder with a button -- I use these (this is a 5 pack) (https://www.amazon.com/Cylewet-Encoder-15%C3%9716-5-Arduino-CYT1062/dp/B06XQTHDRR/)


# Wiring Instructions

## Relays:
* Do NOT try to drive your lenco relays directly(!)  You need to use marine relays to drive them (https://www.amazon.com/PACK-AMP-Waterproof-Relay-Harness/dp/B074FSZWVT/) you'll need 4 total.
* Wire your relays according to lenco diagrams (1 relay per direction/tab) and you'll toggle them with the motor driver in the arduino.
* Wire your actuators with enough power (a single 25A circuit to the back of the boat is fine.)


## Power:
* Since everything except the actuators is very low draw all wiring can be 18-20AWG
* REMOVE 5V REGULATOR JUMPER ON L298N.  This is a small jumper by itself on the board.
* Wire power to the LM2596 "in" solder pads.  Wire this to something that is not always powered or you'll kill your battery.
* Also solder a lead onto the LM2596 "in" solder pads to go directly to the L298N 12V in.
* Connect your LM2596 to a 12V source after turning the gold dial counter-clockwise 15-20 times.  Use a multimeter to measure out pads until you get to 7-8V out.
* Solder wire on the LM2596 "out" solder pads to run to VIN/GND on arduino

## GPS
* Solder or connect 3v3 (+) and GND (-) to arduino pins.
* Connect RX/TX to pin D8/D9 on arduino

## L298N
* Connect 5v and GND to the arduino
* Connect the 4 IN1/IN2/IN3/IN4 to A2/A3/A4/A5
* Connect the OUT1 and OUT2 to the actuator relay at the back of the boat.
* Connect the OUT3 and OUT4 to the actuator relay at the back of the boat.

## Wiring controls:
### Encoder:
* Wire D5 to DT 
* D4 to CLK
* D2 to ROTBUTTON (Might be SWT/SWTCH on yours, its the open pin)
* 5V to the +
* GND shared between led/switch - wire to whichever you prefer

### LED:
* D3 - LED (I used a 12V LED but am feeding it 7v and its fine.)
* GND shared between encoder/switch - wire to whichever you prefer

### SWITCH:
* D10 - LEFT DEPLOY
* D11 - RIGHT DEPLOY
* GND (and GND for encoder/light)

# Install
* Install the arduino IDE and open the .ino sketch in the project.
* PLug in your USB cable to you arduino
* Select your board and port from the menu (nano/uno)
* Install the NeoGPS, EEROM and AltSoftSerial packages if they are not installed (Sketch -> Include library -> manage)
* Upload code to your arduino - there's no required code changes out of box.
* Open serial monitor and you should see it running - it will post a status update every second. If serial isnt working check the baud rate (9600) and the port.

# Usage
To test without speed uncomment the "speedlimit=1" at the end of the loop - this will simulate "always at speed."

* Once on the water, switch surf to your preferred side and accelerate to atleast 8mph (editable at top of code.)
* The tab will deploy for 3.5 seconds by default (on opposite side, if you wired backwards, just fix at acutator wiring or update code.)
* To change the deploy time turn the dial counterclockwise to increase time, clockwise to decrease.
* Once you have found a good deploy time you can press the rotary button at anytime to save that as your new default setting
* If you have issues or a tab stuck deployed hold down the rotary button for 5 seconds and all tabs will retract fully (you'll need to switch back into surf mode probably.)
* If you have an issue and need to reboot hold down the rotary button for 15 seconds and let go, it will restart the arduino loop.

# Notes
* If you used a small project box you can pull your arduino nano to reprogram it easily - or have a spare ready to swap in anytime.
* Make sure you dont feed 12-14V to your arduino or it will most likely die
* Wiring choices are up to you - you can use cat5 without issue and it makes it easy to wire jacks out of the control box.
* I use 4x4x2 electrical boxes with lids from homedepot for my projects - cheap, waterproof,  somewhat tight for all these components - but they do all fit. Everything in box: https://github.com/jonthompson/surfactuator/blob/master/surfactuator_example.JPG

<div>Icons made by <a href="http://www.freepik.com" title="Freepik">Freepik</a> from <a href="https://www.flaticon.com/" title="Flaticon">www.flaticon.com</a> is licensed by <a href="http://creativecommons.org/licenses/by/3.0/" title="Creative Commons BY 3.0" target="_blank">CC 3.0 BY</a></div>
