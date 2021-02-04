# Ender 3 v2

## [Octoprint](https://octoprint.org/)
Ocotoprint can be run on a raspberry pi to provide a web-interface and direct printing over LAN for your not-networked 3D printer. Once setup the printer can be accessed directly from a slicer such as Ultimaker Cura.

### When turning off the printer but keeping Octopi running the printers display stays on
The raspberry pi is delivering 5V of power through the USB cable which keeps the printer partly powered. A quick & easy hack to prevent this is to cover the 5V pin on the USB-A port with electrical tape as seen in [this thread](https://community.octoprint.org/t/led-panel-stays-lit-when-i-turn-off-printer/5707/8).