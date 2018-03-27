# uroflow
DIY uroflow machine

FOR ESP8266 AND ESP32 !!! Make your own uroflow machine!!!

WHAT IS UROFLOW MACHINE?
Uroflow is an appliance which measures how good your urinary flow is when emptying your bladder. It objectively shows patients' status to a urologist. It can show many things. The most known is an obstruction either due to benign prostatic enlargement or other reasons.

As I am an urologist by profession and electronics geek and handyman by heart, I was very keen on making one. My purpose here is to populate this device among men. Most of us will have voiding problems at some time in our lives and the device can show us if it really is a problem or just our feeling.
I offer my firmware for free. As the device is meant for personal usage, it allows 50 measurements before you have to reprogramm the device. Commercial devices cost few thousand euros. See the links below.

VIDEO
I have two videos for my Youtube channel. In the first one I explain what uroflow machine is, how to make the machine and how to use it. In the second video we will see how to calibrate the machine and what does my firmware offer. 

PARTS
- ESP32 (or ESP8266)
- 1Kg load stretch cell with HX711
- 4 wires
- optional: LED and a resistor

I used DOIT ESP32 DEVKIT V1 (selection in Arduino IDE). For ESP8266 the code is compiled for NodeMCU V1.0.
ESP32 brings longer voiding measurement times due to more RAM. Current version supports 5 minutes on ESP32. The ESP8266 has a 60 seconds limit, which is good enough for most people. In my clinical practice I've met only few percent of people voiding longer. These are the ones that really need help.

SCHEMATICS
The schematic is simple. The weighing element has four wires: red, black, white and green. They come from the strain gauges on the load cell. Strain gauges are organized in a wheatstone bridge. That's why there are four wires. They are connected to a HX711 chip. Red goes to E+ and the black one to E-. "E"s represent excitation. Meanwhile white goes to A- and green wire to A+. They are inputs. "A" input can be programmatically defined as gain of 128 or 64, while input "B" has a fixed gain of 32. We will use input "A" with gain 128. Other selectable thing is sample rate. We can choose 10 or 80Hz. I selected 10Hz, as it has lower noise and gives enough precision. Connection to microcontroller has two communication lines: Clock and data line.
The only other thing used in this version of the machine is a red LED which lights when there is an ongoing measurement or calibration procedure. Calibration procedure is also initiated via wifi.
The picture shows how to connect to ESP8266. On ESP32 connect the VCC and GND from HX711 accordingly, DOUT goes to GPIO17 and CLK to GPIO16. LED connects from GPIO23.

HARDWARE DESIGN
Here you can see how a weighing element is mounted. Tray is on the upper side of weighing element. The other side is mounted to the bottom plate. You will need two M3, two M4 screws and some nuts for spacers. You can see the prototype uses breadboard for connections.

PROGRAMMING
First edit config.json according to your likings. Upload the program to your microcontroller. Upload files to SPIFFS too. Files are compiled for any ESP32. For ESP8266 I use NodeMCU.

FILE SYSTEM
We use SPIFFS file system. It contains HTML files, which are editable. Before the first usage you have to upload them on microcontroller (with mkspiffs and flash program). If you do not do it, you can upload them one at a time via http://ip-address/upload. Files are available on my github page.
Main page is "index.html".
The info page is "about.html". It contains all other available links (settings, calibration...).
The file "config.json" contains all the vital information about IP addresses, passwords, calibration factor, NTP server). It is the most important file at startup.
Default username and password are "admin". 
There is a serial port debugging available for those who want to get more information.

HOW TO USE
First you have to put the appliance on a leveled ground. Put the collecting mug on the tray. If it is heavy, leave it there for few minutes, for the load cell to stretch. If you use the machine for the first time or want to recalibrate it after a certain period of time, you initiate the calibration procedure with a known weight via wifi. The calibration parameters are stored on the machine itself.
When measuring the urinary flow, you have to use a wide funnel which does not contact the mug or the device. Funnel collects split or sprayed stream and makes just a slight impact on the measurement. The other important thing is not to touch the device in any way while voiding. Touching makes artifacts.

IP ADDRESS
To find your IP address you can use any of the free IP scanners: for windows I recommend Advanced IP scanner, for android Fing. You can also connect the device to a serial port and use 115200 baud - IP address is displayed. If you use DHCP on your router, you can assign a fixed IP address to your device.

WEBSITE
After voiding open device IP address in your browser. A page displays. It contains a table and two graphs. See pictures. You can print the report by pressing CTRL+P. Before the actual print enter patient's name into name input box. The first graph displays the volume of voided urine in time. The second graph shows us flow in time.

VARIABLES ACCESSIBLE THROUGH WEBPAGES
All html files are editable. You can change them if you like. See the UroflowVARS.ino or check the enclosed html files.

Free for personal use. Commercial use is negotiable. Simple to use, high precision, low cost (ca.10€).

---------------------------------------------------------------------------------------------------------------------
Do you like my work?
1. Hit LIKE on my projects and youtube videos.
2. Hit SUBSCRIBE on my youtube channel! Did you consider subscribing to my youtube channel and being updated when new videos are published?
3. COMMENT where you can.
4. SHARE.
5. Support my work on Patreon: https://www.patreon.com/GreenEyedExplorer
6. You can also donate directly to me via: http://paypal.me/rokrodic
7. Buying through my affiliate links makes you no additional cost, but gives me a small headstart in getting new things for my explorations.

---------------------------------------------------------------------------------------------------------------------
LINKS:
My homepage: http://www.rodic.si
My youtube channel: https://www.youtube.com/channel/UCIOIhhPirDJH8LB0azJmd8w
My Thingiverse designs: https://goo.gl/jdyHbF
My GitHub page: https://goo.gl/XtjB3h 
