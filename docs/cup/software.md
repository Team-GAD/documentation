---
layout: default
title: Software
parent: Cup
nav_order: 2
---

# Software

The software that has to be loaded on the ESP32 was written in Arduino 
and can also be found in GitHub. 
Here are the most important things explained. 


## Libraries

For the software to be fully functional, the following libraries must be included.

```
#include <SPIFFS.h>
#include <WiFi.h>
#include <PubSubClient.h>
#include <ArduinoJson.h>
#include <Adafruit_NeoPixel.h>
#include <Arduino.h>
#include <ESPAsyncWebServer.h>
#include <AsyncTCP.h>
```

**SPIFFS.h** SPIFFS stands for (S)erial (P)eripheral (I)nterface (F)lash (F)ile 
(S)ystem and what is meant here is that our ESP can hold a simple file 
system in the SPI program memory, 
which also contains our program code. Here the website for the WifiManager 
is stored as well as the SSID and the password for the access point

**WiFi.h** of course ensures that our ESP32 can establish a WLAN connection.

**PubSubClient.h** provides the MQTT functionalities so that our ESP32 can communicate with the MQTT Broker.

**ArduinoJson.h** allows to convert a string into JSON format so that it can be easily worked with. 

**Adafruit_NeoPixel.h** provides the communication with the LED ring and allows to visualize different annimations.

**Arduino.h** integrates the Arduino core library 

**ESPAsyncWebServer.h** and **AsyncTCP.h** Used to create a web server where an access point can be configured if necessary. 


## Code

The code was written in Arduino and consists of the following files, which are described in more detail below. 

- main.ino
- led.ino
- wifi_manager.ino
- nfc_p2p.ino 
- nfc.cpp
- nfc.h

### Main

First of all, all libraries are included in the main file. Like every Adruino program, it contains a setup and a loop function.
In the setup function, everything is initialized first, such as the LEDs and the NFC module, and the WLAN connection is also established here.
An important step that also happens in this function is the creation of a task. Here a CPU core is assigned a certain task. The ESP32 has 2 CPU cores, in this project one is used for the LED control and the other for the remaining functions. So the functions are never blocked and the LED annimations run smoothly.

In the loop the ESP32 tries to connect to the MQTT broker at the beginning and if it should lose the connection it tries to reestablish it immediately. 

### LED

This file contains all the functions that have to do with the LEDs, 
such as various annimations or parsing the color from the JSON string.

### WIFI Manager

If the ESP is switched on for the first time in a new environment, 
it has no configuration and therefore cannot connect to the gateway. 
That is why there is the WIFI Manager. 
If this scenario occurs, the WIFI Manager creates a web server and an 
access point. Users can connect to this access point and configure the 
cup by entering an SSID and the password from the gateway.  
Once everything is configured the ESP32 will restart and try to connect to the gateway. 
If it still cannot connect, the procedure with the WIFI Manager is repeated.

### Nfc_p2p

This file contains all functions related to the NFC module. 
Here another NFC module is scanned, either in initiator or in target mode. 
Depending on which mode the cup is currently in. 

The remaining two files are needed also for the NFC scan. 