# uroflow
<B>DIY uroflowmetry machine</B></BR>
<img src="https://github.com/rokrodic/uroflow/blob/master/IMAGES/20180118_085800.jpg?raw=true" alt="Uroflowmetry device prototype"></BR>
Uroflowmetry device prototype</BR>
</BR>
<B>FOR ESP32!!! ESP8266 SUPPORT HAS BEEN DROPPED DUE TO LOW RAM AND COMPUTING POWER THEY HAVE!!!</B></BR>
</BR>
<B>WHAT IS UROFLOW MACHINE?</B></BR>
Uroflow is an appliance which measures how good your urinary flow is when emptying your bladder. It objectively shows patients' status to a urologist. It can show many things. The most known is an obstruction either due to benign prostatic enlargement or other reasons.</BR>
</BR>
As I am an urologist by profession and electronics geek and handyman by heart, I was very keen on making one. My purpose here is to populate this device among men. Most of us will have voiding problems at some time in our lives and the device can show us if it really is a problem or just our feeling.</BR>
I offer my firmware for free. As the device is meant for personal usage, it allows 50 measurements before you have to reprogramm the device. Commercial devices cost few thousand euros. See the links below.</BR>
</BR>
<B>VIDEO</B></BR>
I have two videos for my Youtube channel. In the first one I explain what uroflow machine is, how to make the machine and how to use it. In the second video we will see how to calibrate the machine and what does my firmware offer. </BR>
</BR>
<B>PARTS</B></BR>
- ESP32 (or ESP8266)</BR>
- 1Kg load stretch cell with HX711</BR>
- 4 wires</BR>
- optional: LED and a resistor</BR>
</BR>
I used DOIT ESP32 DEVKIT V1 (selection in Arduino IDE). For ESP8266 the code is compiled for NodeMCU V1.0.</BR>
ESP32 brings longer voiding measurement times due to more RAM. Current version supports 5 minutes on ESP32. The ESP8266 has a 60 seconds limit, which is good enough for most people. In my clinical practice I've met only few percent of people voiding longer. These are the ones that really need help.</BR>
</BR>
<B>SCHEMATICS</B></BR>
<img src="https://github.com/rokrodic/uroflow/blob/master/IMAGES/SCH.png?raw=true" alt="uroflowmetry device schematics"></BR>
The schematic is simple. The weighing element has four wires: red, black, white and green. They come from the strain gauges on the load cell. Strain gauges are organized in a wheatstone bridge. That's why there are four wires. They are connected to a HX711 chip. Red goes to E+ and the black one to E-. "E"s represent excitation. Meanwhile white goes to A- and green wire to A+. They are inputs. "A" input can be programmatically defined as gain of 128 or 64, while input "B" has a fixed gain of 32. We will use input "A" with gain 128. Other selectable thing is sample rate. We can choose 10 or 80Hz. I selected 10Hz, as it has lower noise and gives enough precision. Connection to microcontroller has two communication lines: Clock and data line.
The only other thing used in this version of the machine is a red LED which lights when there is an ongoing measurement or calibration procedure. Calibration procedure is also initiated via wifi.</BR>
<B>The picture shows how to connect to ESP8266. On ESP32 connect the VCC and GND from HX711 accordingly, DOUT goes to GPIO17 and CLK to GPIO16. LED connects from GPIO23.</B></BR>
</BR>
<B>HARDWARE DESIGN</B></BR>
Here you can see how a weighing element is mounted. Tray is on the upper side of weighing element. The other side is mounted to the bottom plate. You will need two M3, two M4 screws and some nuts for spacers. You can see the prototype uses breadboard for connections.</BR>
</BR>
<B>PROGRAMMING</B></BR>
First edit config.json according to your likings. Upload the program to your microcontroller. Upload files to SPIFFS too. Files are compiled for any ESP32. For ESP8266 I use NodeMCU.</BR>
</BR>
<B>FILE SYSTEM</B></BR>
We use SPIFFS file system. It contains HTML files, which are editable. Before the first usage you have to upload them on microcontroller (with mkspiffs and flash program). If you do not do it, you can upload them one at a time via http://ip-address/upload. Files are available on my github page.</BR>
Main page is "index.html".</BR>
The info page is "about.html". It contains all other available links (settings, calibration...).</BR>
The file "config.json" contains all the vital information about IP addresses, passwords, calibration factor, NTP server). It is the most important file at startup.</BR>
Default username and password are "admin". </BR>
There is a serial port debugging available for those who want to get more information.</BR>
</BR>
<B>HOW TO USE</B></BR>
First you have to put the appliance on a leveled ground. Put the collecting mug on the tray. If it is heavy, leave it there for few minutes, for the load cell to stretch. If you use the machine for the first time or want to recalibrate it after a certain period of time, you initiate the calibration procedure with a known weight via wifi. The calibration parameters are stored on the machine itself.</BR>
When measuring the urinary flow, you have to use a wide funnel which does not contact the mug or the device. Funnel collects split or sprayed stream and makes just a slight impact on the measurement. The other important thing is not to touch the device in any way while voiding. Touching makes artifacts.</BR>
</BR>
<B>IP ADDRESS</B></BR>
To find your IP address you can use any of the free IP scanners: for windows I recommend Advanced IP scanner, for android Fing. You can also connect the device to a serial port and use 115200 baud - IP address is displayed. If you use DHCP on your router, you can assign a fixed IP address to your device.</BR>
</BR>
<B>WEBSITE</B></BR>
After voiding open device IP address in your browser. A page displays. It contains a table and two graphs. See pictures. You can print the report by pressing CTRL+P. Before the actual print enter patient's name into name input box. The first graph displays the volume of voided urine in time. The second graph shows us flow in time.</BR>
</BR>
<B>VARIABLES ACCESSIBLE THROUGH WEBPAGES</B></BR>
All html files are editable. You can change them if you like. See the UroflowVARS.ino or check the enclosed html files.</BR>
</BR>
<B>Free for personal use. Commercial use is negotiable. Simple to use, high precision, low cost (ca.10€).</B></BR>
</BR>
<B>HOW TO UPLOAD FIRMWARE AND FILES</B></BR>
Watch my video on Youtube how to do the steps below.</BR>
Unpack the UPLOAD.ZIP to your hard drive. It contains all the necessary files. Here are two parts. In the first one I explain how to upload firmware and in the second one how to upload website files.</BR>
PART 1</BR>
======</BR>
1. Copy latest firmware into "Firmware" directory. The file for ESP32 should be named: UroflowESP32.ino_ESP32.bin. The file for ESP8266 should be named UroflowESP32.ino_ESP8266.bin.</BR>
2. Connect your uroflow device via USB cable to your PC.</BR>
3. Find the COM PORT number the device presents itself. </BR>
   Example to find the port number: Click the windows icon at the bottom left of your screen. Type "device manager" and windows should find the program. If this latest step does not work on your computer there are two options: a) press Windows Key + R and run "devmgmt.msc" b) find the program under the menus.</BR>
   Then look under the "Ports (COM & LPT)" for the COM port (something like "Silicon Labs CP210x USB to UART Bridge (COM3)") - this brings us to COM3.</BR>
4. Edit appropriate .bat file UroflowUpload_ESP32.bat (for ESP32) and UroflowUpload_ESP8266.bat (for ESP8266) and CHANGE YOUR COM PORT!</BR>
5. Run the appropriate .bat file.</BR>
</BR>
Alternative commands:</BR>
ESP32:</BR>
esptoolESP32.exe --chip esp32 --port COM3 --baud 921600 --before default_reset --after hard_reset write_flash -z --flash_mode dio --flash_freq 80m --flash_size detect 0xe000 esp32/partitions/boot_app0.bin 0x1000 esp32/sdk/bin/bootloader_dio_80m.bin 0x10000 Firmware/UroflowESP32.ino_ESP32.bin 0x8000 Firmware/UroflowESP32.ino.partitions_ESP32.bin</BR>
</BR>
ESP8266:</BR>
esptoolESP8266.exe -vv -cd nodemcu -cb 115200 -cp COM3 -ca 0x00000 -cf Firmware/UroflowESP32.ino_ESP8266.bin</BR>
</BR>
PART 2</BR>
======</BR>
After finding your IP address (with Fing for android or Advanced IP scanner for windows) enter into browser: "your-ip-address/upload". Mind the /upload! here you can select one-by-one file and upload it to your file system.</BR>
</BR>
---------------------------------------------------------------------------------------------------------------------</BR>
<B>Do you like my work?</B></BR>
1. Hit <B>LIKE</B> on my projects and youtube videos.</BR>
2. Hit <B>SUBSCRIBE</B> on my youtube channel! Did you consider subscribing to my youtube channel and being updated when new videos are published?</BR>
3. <B>COMMENT</B> where you can.</BR>
4. <B>SHARE</B>.</BR>
5. Support my work on <B>Patreon</B>: https://www.patreon.com/GreenEyedExplorer</BR>
6. You can also <B>buy me a coffee</B> directly via: http://paypal.me/rokrodic</BR>
7. Buying through my <B>affiliate links</B> makes you no additional cost, but gives me a small headstart in getting new things for my explorations.</BR>
</BR>
---------------------------------------------------------------------------------------------------------------------</BR>
<B>LINKS:</B>
My homepage: http://www.rodic.si</BR>
My youtube channel: https://www.youtube.com/channel/UCIOIhhPirDJH8LB0azJmd8w</BR>
My Thingiverse designs: https://goo.gl/jdyHbF</BR>
My GitHub page: https://goo.gl/XtjB3h</BR>

<B>MEDIA</B>
- HACKADAY: https://hackaday.com/2018/04/01/assess-your-output-with-a-cheap-diy-urine-flowmeter/
- ELEKTOR MAGAZINE - won 5th place in ESP32 design contest 2018: https://www.elektormagazine.com/labs/contest/esp32-design-contest-2018
- ELEKTOR MAGAZINE: https://www.elektormagazine.com/labs/uroflow-machine-for-every-home
