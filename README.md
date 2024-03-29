# WAFFLE
Wife Acceptance Factor - Friggin' Lights Edition  (A simple panel for controlling Tasmota MQTT devices)


## What is this?
This exposes the fruits of your home automation labor to those who are less interested in (or flat out annoyed by) your obsession with Tasmota, MQTT and Home Automation. In a somewhat user-friendly way. It is a short and simple HTML file with some CSS and JS included. 

Set the MQTT broker address, and the resulting webpage will show a number of buttons equal to the number of relays on your Online devices as reported by the MQTT broker.

Each button will toggle the power output and reflect the state of the relay.
The button text reflects the topic and (if more than one relay) a number denoting the relay number.

Like this:
![WAFFLE](https://github.com/dagbdagb/waffle/blob/master/waffle.png)


## What is it not?
This does not do anything at all for configuring your devices. For that, have a look at [Tasmota Device Manager](https://github.com/jziolkowski/tdm).


## How to use it?
Assuming you start with a working setup with the Mosquitto MQTT broker and one or more Tasmota devices, *and* your MQTT setup matches mine, there are three simple steps to follow:

1. Enable websockets in mosquitto, by adding these two lines to the mosquitto config file. 
(possibly /etc/mosquitto/mosquitto.conf)

        listener 9001
        protocol websockets

...then restart mosquitto. (_sudo service mosquitto restart_).

2. Download and edit the HTML [file](https://github.com/dagbdagb/waffle/raw/master/lights.html) to point to your own mosquitto MQTT broker. Search for 'CHANGE THIS' to find the right line.

3. Load the file in a browser, either from the local filesystem or via a webserver. No installation required.

**Note 1:** Your distribution's build of mosquitto may or may not have support for websockets.

**Note 2:** My devices use the format {tele|stat|cmnd}/topic/{POWER|RESULT} format for MQTT. If your setup is different, I presume you need to change the JS a bit. Sorry, not sorry.


## How are buttons sorted?
Alphabetically. Topics/buttons with a trailing digit are grouped with the topic/button with the same topic *without* a trailing digit.

This reflects my setup, where a wall switch in a room has a topic without a digit, and every device controlled by the same switch has the same topic with a terminating digit. All devices have a group topic, and I use rules to toggle groups of devices from my wall switch.

Devices with more than one relay get a button text with a dash and a trailing digit for each relay.


## Are there any concerns with regard to security?
Absolutely.
There are no security considerations in the HTML/JS here *at all*.
The instructions for editing mosquitto.conf above opens one more pathway for someone to probe and/or break into your system(s).

The HTML file itself is quite short and can quickly be reviewed by anyone. It does load one external JS library, though.
If this should give you cause for concern or not is your business. 

A full discussion about MQTT, websockets and security is out of scope here. Also, if you have enabled authentication in your mosquitto instance, you will have to modify this file.


## Are there any known bugs?
No software is complete without 'unexpected features', or features so glaringly missing that it borders on being a bug.

* There are buttons for non-existing devices.
    The JS here will happily create buttons for a device the broker claims is online, even if it isn't. This is due to the broker keeping retained messages. Google how to kill it. I could probably work around this in JS.

* There is no config file. 
    
    This is distinctly a feature. I want to discover and make everything look pretty, entirely based on information from the broker or devices themselves.

* All buttons have the same color.
    
    IMHO, this looks nice, but from a usability perspective it is less optimal. People with limited sight could certainly benefit from colorcoded buttons.
    Tasmota allows for 5 user defined variables (mem1 to mem5). Each variable will only hold 9 characters. I am considering using one of these as an array of indexes for colors and labels.

* I want custom button text.
    
    See above.
    
* What about dimmers?

    I don't have any. HTML5 does allow for sliders, so it is most likely doable for someone with exactly the right itch.
 
 * Sensors?
    
    Would be cool to have each button appear as a tiny LCD display, with signal strength, sensor readings and what not. Let me know when you have forked this and implemented something like it.
    
* The page drops contact with the MQTT broker.

    I have noticed. I should probably do something to automatically reload the page periodically and/or when connection is dropped.

* The logic in the function for drawing buttons is wrong.

    Yeah. When a new device is coming online after the page has been loaded, it will likely end up somewhere odd. Haven't tested this yet.
    
* I found something else/I have a fix for something.

    Cool. I hang in the Tasmota Discord channel.


## This is crap. Who TF wrote this thing?
Someone whose day job is not writing HTML or JS. I rely heavily on w3schools and stackoverflow. You have been warned.


