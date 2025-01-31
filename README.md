![image](https://github.com/EQMOD/EQM_OBDWEB/assets/29789200/ff318b5f-7a61-4340-b203-8979be0f3c4c)# EQM_OBDWEB
A WEB Based or Wifi/BLE (EL327 Compatible) OBDII Dongle Platform using the ESP32 WROVER Module

An OBDII Dongle using the ESP32 Wrover with built-in SPIFFF memory is used as a CAN BUS OBDII reader and the data is presented as web page using a built-in webserver. The Webpage communicates to the dongle  via WiFi and Websockets,  ESP32 is a dual core microcontroller with the first core handling the CAN Bus Comunications part, and the 2nd core handling the websocket part. OBDII data is pushed to the UI ever 60ms to 100ms for critical data such as rpm and  speed and every 1000ms for not so critical data such as temp, voltage, etc.  Using ESP32 RTOS for the  multi core multi tasking component. That's basically a webserver running inside that diy dongle attached to the car's obd port. And literally you can read every car metric data and show it on the infotainment with customizable fancy UI stuff (gauges, graphs, etc.) using standard HTML/JS/CSS/JPG renders.

 Mobile phone apps not required as long as the infotainment/mobilephone/etc can render the UI using a standard webbrowser.

 Once the UI client is connected to the ESP32 via WIFI,  Webserver can be accessed via these urls; 

 OBD HomePage:
 
 http://192.168.0.10/

ESP32 Load Monitoring

http://192.168.0.10/page?var=file&val=/ui/CPULoad/index.html


WEB ASSETS are stored in the ESP32 SPIFFS memory storage which is automatically populated one time  from the data on the SD Card. A SPIFF memory update is triggred by deleting the lock.file on the SD card. Any updates on the WEBSERVER files should be done on the SD card with the "lock.file" deleted.

There are two BLE modules used for this project. The first BLE/Bluetooth Module built in with the ESP32 is used as the Bluetooth connector for the OBDII dongle and can be used to to connect to Mobile OBDII apps such as TORQUE. 

The 2nd Bluetooth/BLE module a JDY-08 contains a user programmable CC2541 BLE Chipset which can be used to receive Car sensor data that are bluetooth based. DEMO CC2541 codes are provided to receive BLE Advertisments from TPMS Sensors such as the Bluetooth based VC601 Tire Pressure Sensors or a Battery Monitoring Sensor (BM2).
The same BLE module can be loaded with a UART-BLE for ELM327 AT command compatible communication.


![image](https://github.com/EQMOD/EQM_OBDWEB/assets/29789200/8c971291-0b14-477d-abf0-11e375a93849)

Here is the Connection diagram from the ESP32 Wrover with SD Card Reader and JDY08 BLE Module

![image](https://github.com/EQMOD/EQM_OBDWEB/assets/29789200/64a7ada1-9e7a-4788-9aba-bed030aca00d)

And here is the suggested development platform (codes included) which provide the user options to burn firmware on the CC2541 by simply dropping a cc2541.bin file on the SD card.

<img width="897" alt="image" src="https://github.com/EQMOD/EQM_OBDWEB/assets/29789200/714c41b0-87a3-4769-ac86-8fdbf50bd103">

![image](https://github.com/EQMOD/EQM_OBDWEB/assets/29789200/5004d103-8bce-4605-83f4-3de82ef758c6)


SAMPLE WEBUI RENDERS;

Homepage;

<img width="883" alt="image" src="https://github.com/EQMOD/EQM_OBDWEB/assets/29789200/c73f5365-5a80-47ea-a897-e879e56ff0a9">

OBDII Screen (Screenshot using data from an OBDII Emulator)


![image](https://github.com/EQMOD/EQM_OBDWEB/assets/29789200/6237eb39-76e0-43a0-86b7-357491b815a1)


TPMS (Tire Pressure Monitoring Screen) 

<img width="912" alt="image" src="https://github.com/EQMOD/EQM_OBDWEB/assets/29789200/b3a094ac-f161-4a8f-b364-854bd627f710">

Battery Monitor via BM2 BLE Broadcasts. Other Battery data is also possible

<img width="969" alt="image" src="https://github.com/EQMOD/EQM_OBDWEB/assets/29789200/c11f6775-d5a7-4e06-84ad-4a189e4e7c38">


ESP32 LOAD Monitoring Screen 

<img width="961" alt="image" src="https://github.com/EQMOD/EQM_OBDWEB/assets/29789200/0481a5cb-47ff-49e9-9991-760a7c0b5ec1">

Sample 3D Printed OBD Dongle (3d files/stl included in the respository)

![image](https://github.com/EQMOD/EQM_OBDWEB/assets/29789200/18fc7b90-b6f0-44de-b6d9-f7ac2d33e340)


How to flash the esp32 itself ;

![image](https://github.com/EQMOD/EQM_OBDWEB/assets/29789200/219494cd-2c7f-46d5-8f14-071f5b2612c8)

Using an "ESP32 Downloader"

![image](https://github.com/EQMOD/EQM_OBDWEB/assets/29789200/8385255c-e1f7-4747-b793-4b1737f40e6e)

CC2541 JDY08 BLE Module Firmwares

![image](https://github.com/EQMOD/EQM_OBDWEB/assets/29789200/e9ee0860-a884-4f26-a952-db3776b59644)


TPMS VC601 Broadcast emulator for testing the cc2541 codes uing a CCDebugger

![image](https://github.com/EQMOD/EQM_OBDWEB/assets/29789200/e762d1d4-6cbb-4614-a0e2-ff4a878afb4c)

Firmware Source ( You need IAR to compile these) 

https://github.com/EQMOD/EQM_OBDWEB/tree/main/CC254x_TPMS_BATMON/Custom%20JDY08-CC2541%20Firmware%20TPMS%20BATMON/SDK/BLE-CC254x-1.4.0/Projects/ble/TPMSBroadcast_Tester

JDY08 Firmware source codes to receive BLE VC601 TPMS Sensor broadcasts and presented to the ESP32 via UART

https://github.com/EQMOD/EQM_OBDWEB/tree/main/CC254x_TPMS_BATMON/Custom%20JDY08-CC2541%20Firmware%20TPMS%20BATMON/SDK/BLE-CC254x-1.4.0/Projects/ble/TPMS_OBD

COMPILING and FLASHING

This version of the program works best with a ESP32-D0WD-V3 (revision 3) 16MB
with the following compile settings;

<img width="960" alt="image" src="https://github.com/EQMOD/EQM_OBDWEB/assets/29789200/d99bd190-b4f2-46fa-9959-13d611277ca3">

Formatting and Flashing the SPIFF Memory is initiated by checking if a detected/attached SD Card is without a "lock.file" inside;

<img width="1920" alt="image" src="https://github.com/EQMOD/EQM_OBDWEB/assets/29789200/af0fd553-99ad-45f9-a32c-b54a19f7b46d">



ON-SITE DEBUGGING

A portable flasher and Serial Console Monitoring port in one as implemented on the EQM_OBDWEB Dongle. The idea here is we use the same 6 pin port to flash new code on the ESP32 inside the obd  dongle OR use it as Serial Console port by plugging in a JDY-16 Bluetooth UART module and connect it to a mobile app BLE Serial Terminal  and monitor the ESP32 activity through a mobile phone;

![image](https://github.com/EQMOD/EQM_OBDWEB/assets/29789200/fd193d7f-0f1a-49eb-bc8a-70d599164461)

JDY-16 Module for Bluetooth UART Console Port Monitoring

![image](https://github.com/EQMOD/EQM_OBDWEB/assets/29789200/828c9ec3-278d-4989-b80c-19fa451150d2)

Connection Diagram

![image](https://github.com/EQMOD/EQM_OBDWEB/assets/29789200/f9dcf423-b83c-4fc4-968b-96162d01d422)

Mobile APP with the Serial Console Data

![image](https://github.com/EQMOD/EQM_OBDWEB/assets/29789200/b5c5d805-cb0c-42b5-a1af-8e539e9dc70a)


Flasher and JDY-16 modules both fit on the same flashing port on the EQM_OBDWEB Dongle

![image](https://github.com/EQMOD/EQM_OBDWEB/assets/29789200/7f59b2c6-b49e-42fd-8880-529d55bf98ad)










 
