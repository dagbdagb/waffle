# WAFFLE
Wife Acceptance Factor - Friggin' Lights Edition - A simple panel for Tasmota MQTT devices

## What is this?
This exposes the fruits of your home automation labor to those less interested in or impressed by Tasmota, MQTT and Home Automation. In a somewhat user-friendly way. It is a short and simple HTML file with some CSS and JS included. 

Set the MQTT broker address, and the resulting webpage will show a number of buttons equal to the number of relays on your Online devices as reported by the MQTT broker.

Each button will toggle the power output and reflect the state of the relay.
The button text reflects the topic and (if more than one relay) a number denoting the relay number.

Like this:
![WAFFLE](https://github.com/dagbdagb/waffle/blob/master/waffle.png)


## What is it not?
This does not do anything at all for configuring your devices. 


## How can I use it?
Assuming you start with a working setup with the Mosquitto MQTT broker and one or more Tasmota devices,*and* your MQTT setup matches mine, there are three simple steps to follow:

1. Enable websockets in mosquitto*, by adding these two lines to the mosquitto config file. 
(possibly /etc/mosquitto/mosquitto.conf)

        listener 9001
        protocol websockets

...then restart mosquitto. (sudo service mosquitto restart).
**Note:** Your distribution's build of mosquitto may or may not have support for websockets.

2. Edit the html file to point to your own mosquitto mqtt broker.
Search for 'CHANGE THIS' to find the right line.

3. Load the file in a browser, either from the local filesystem or via a webserver. 


## How are buttons sorted?
Alphabetically. Topics/buttons with a trailing digit are grouped with the topic/button with the same topic *without* a trailing digit.

This reflects my setup, where a wall switch in a room has a topic without a digit, and every device controlled by the same switch has a digit.
All devices have a group topic

Like this:
    wall switch:    livingroom
    lamp1:          livingroom1
    lamp2:          livingroom2


## Are there any concerns with regard to security?
Absolutely.
There are no security considerations in the html/javascript here *at all*.
The instructions for editing mosquitto.conf above opens one more pathway for bad guys to probe and/or break into your system(s).
The html file itself is quite short and can quickly be reviewd by anyone. It does load one external javascript library, though.
If this should give you cause for concern or not is your business. A full discussion about MQTT, websockets and security is out of scope here. Also, if you have enabled authentication in your mosquitto instance, you may have to do the same in this file.


## Are there any known bugs?
No software is complete without 'unexpected features', or features so glaringly missing that it borders on being a bug.

* The JS here will happily create buttons for devices the broker claims is online, even if it isn't.
This is due to the broker keeping retained messages. Google how to kill it. I could probably work around this in JS.

* There is no config file. 
This is distinctly a feature. I want to discover and make everything look pretty, entirely based on information from the broker or devices themselves.

* All buttons have the same color.
IMHO, this looks nice, but from a usability perspective it is less optimal. People with limited sight could certainly benefit from colorcoded buttons.
Tasmota allows for 5 user defined variables (mem1 to mem5). Each variable will only hold 9 characters. I am considering using one of these as an array of indexes for colors and labels.

* I want custom button text.
See above.


## Who wrote this?
Someone whose day job is not writing html or javascript. I rely heavily on w3schools and stackoverflow. You have been warned.


