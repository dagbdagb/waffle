# WAFFLE
Wife Acceptance Factor - Friggin' Lights Edition - A simple panel for Tasmota MQTT devices

## What is this?
This exposes the fruits of your home automation labor to those less interested in or impressed by Tasmota, MQTT and Home Automation. In a somewhat user-friendly way. It is a short and simple HTML file with some CSS and JS included. 

Set the MQTT broker address, and the resulting webpage will show a number of buttons equal to the number of relays on your Online devices as reported by the MQTT broker.

Each button will toggle the power output and reflect the state of the relay.
The button text reflects the topic and (if more than one relay) a number denoting the relay number.

Like this:
![WAFFLE](https://github.com/dagbdagb/waffle/blob/master/waffle.png)

## How can I use it?
Assuming you start with a working setup with the mosquitto MQTT broker and one or more tasmota devices, there are three simple steps to follow:

1. Enable websockets in mosquitto*, by adding these two lines to the mosquitto config file. 
(possibly /etc/mosquitto/mosquitto.conf)

    listener 9001
    protocol websockets

...then restart mosquitto. (sudo service mosquitto restart).
**Note:** Your distribution's build of mosquitto may or may not have support for websockets.

2. Edit the html file to point to your own mosquitto mqtt broker.
Search for 'CHANGE THIS' to find the right line.

3. Load the file in a browser, either from the local filesystem or via a webserver. 

