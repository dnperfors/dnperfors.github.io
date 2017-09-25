As brain for my homeaustomation I have chosen [Home Assistant](https://home-assistant.io). My main reason for chosing Home Assistant is that it is super easy to install on a Raspberry pi. There are basically four options:

1. hass.io - the docker image variant
1. hassbian - the preinstalled raspbian installation
1. Raspberry Pi All-In-One - the all in one installation script to get started quickly
1. Manual - manual install everything

After trying all options, I finally went for the manual installation. Mainly because I had problems getting the [`fritz` component](https://home-assistant.io/components/device_tracker.fritz/) working in the other options.

# My Setup
This section describes which components I use, what problems I had with them and how I solved them. My configuration is not yet available, but I intend to put it on GitHub.

## Pi Light
In order to control my lights, I use PiLight and KaKu switches. Setting this up is straightforward using the [component documentation](https://home-assistant.io/components/switch.pilight/).
The only problem I still have is that when PiLight is configured with a port, it is no longer possible to use `pilight-send` and `pilight-receive`.

## Fritz!Box
Fritz!Box is the router I use for my internet. Home Assistent has support for device tracking via the [`fritz` component](https://home-assistant.io/components/device_tracker.fritz/). In order to get this component working, some dependencies.
I had several problems installing lxml in the python virtual environment:
* "Error when installing lxml because of dist_wheel" - Not sure what the problem was, but I had this problem in all standard installation options, except the manual installation.
* "Not enough memory" when installing lxml - Fixed by assigning less memory to the gpu as described [here](https://raspberrypi.stackexchange.com/a/15299).
