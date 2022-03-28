Python tkinter app that displays the temperature from zigbee and 433 MHz sensors. The sensor data is sent to mqtt by either zigbee2mqtt for sensors that use zigbee or sent to mqtt by the linux program rtl_433.

For zigbee you need a usb zigbeee dongle as well as the zigbee2mqtt software (available here on github). The zigbee2mqtt web site here on github lists the available usb zigbee dongles. The Electrolama zig-a-zig-ah! (zzh!) is well regarded by the author of zigbee2mqtt. The Conbee II has lots of stars and reviews on Amazon. One disadvantage with the zigbee sensors is that I know of only one that's rated for outdoor use, the Philips Hue outdoor motion sensor, which also has a temperature sensor. The zigbee sensors don't send out readings very often, perhaps because zigbee is strong on low power usage.

For the 433 MHz sensors you need a usb rtl sdr dongle. The one from rtl-sdr.com is a good choice and nooelec also. For interpreting the data from the rtl sdr dongle I use the linux program rtl_433. It's a command line program, with options to send its output to mqtt. There are many 433 MHz temperature sensors available, sold as additional ones for an indoor/outdoor digital thermometer. I have an AccuRite sensor and a ThermoPro sensor. Also an ancient sensor for a Radio Shack indoor/outdoor thermometer. All three work with the rtl_433 software. That software probably works with every known sensor in the world. My rtl sdr dongle is also picking up the readings from some of the neighbors' sensors.

I have both dongles on my Linux Debian PC, and for mqtt I'm using mosquitto. Mosquitto is getting sensor readings for both zigbee sensors as well as 433 MHz sensors. (A Raspberry Pi should work well.)

For the 433 MHz sensors you'll need to edit the file Mqtt_mod.py; near the top is an assignment to self.rtl433_sensor_names. The format is one or more lines of
```
"friendly displayed name" : ( "Model name rtl_433 uses", channel )
```
with a comma between each. To figure out what model name to use I installed MQTT Explorer on my Windows PC. It's very handy for seeing what's being sent to your mqtt service.

For the zigbee sensor names you set them up with zigbee2mqtt. For me that's also running on my Linux PC. I configured it so that it has a web page I can use from my Windows PC (my Linux PC doesn't have a monitor or keyboard).

So to summarize, my Linux PC is running mosquitto, zigbee2mqtt, and rtl_433. It has both a zigbee usb dongle and an rtl sdr dongle plugged into it. My Windows PC runs this python program to display the temperature readings. I start the program with temperature.cmd as one of my Windows startup programs.