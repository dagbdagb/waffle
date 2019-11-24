# waffle
Wife Acceptance Factor F*cking Lights Edition - A simple panel for Tasmota MQTT devices

## What is this?
This exposes the fruits of your home automation labor to those less interested in or impressed by Tasmota, MQTT and Home Automation. In a somewhat user-friendly way. It is a short and simple HTML file with some CSS and JS included. 

Set the MQTT broker address, and the resulting webpage will show a number of buttons equal to the number of relays on your Online devices as reported by the MQTT broker.

Each button will toggle the power output and reflect the state of the relay.
The button text reflects the topic and (if more than one relay) a number denoting the relay number.
