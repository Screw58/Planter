# Project Planter

## General
Planter is my project for monitoring plants growth parameters e.g. humidity, soil moisture, illuminance and temperature.The idea is to collect all measurements from each plant and visualize it in the graph on pc or mobile phone via home network.
Project contains minimum 2 devices: **slave** and **master**.


## Details

**Slave**\
Each plant is controlled by it's own one device based on ESP32 microcontroller. The device is supplied by one 18650 battery via buck-boost controller. In the most of the time, the device is in the deep sleep mode. It wakes up on the time set by user (e.g. 8.00 a.m and 7.00 p.m) or "on demand" by pressing the user button. After this, all the measurements are read from the sensors connected to the ESP32 and send to the *host* via MQTT. At the end of the cycle, device checks time using SNTP and calculates the time needed to the next wake up event.

**Host**\
The role of the host is played by the RaspberryPi 5. It receives readings from Slaves via mosquitto broker and pass it to the InfluxDB database. Then Grafana reads the values and visualize it in the graphs.

## Other 

Tools used in the project:
* Git - gitflow strategy (master branch for releases and dev as a main development branch)
* KiCad for creating schematics and design PCB 
* esp-idf-v5.3 framework 