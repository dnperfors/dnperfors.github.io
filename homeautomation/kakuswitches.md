In order to automatically turn on and off some of my lights, I needed to be able to control the kaku (klik aan klik uit) switches.
These switches work on 433MHz and can be easily controlled via [pilight](https://pilight.org). This page describes how I found out how to control these switches.

# Hardware
In order to communicate with the kaka switches, you will need a 433MHz sender. Pilight has some recommendation for which to use and a good description on how to [connect the hardware](http://manual.pilight.org/electronics/wiring.html)

Since I had a different sender and receiver I followed some other tutorials on how to connect, making sure the data pins were connected to the same GPIO pins as described by pilight.

# Software
In order to test the communication, I used pilight. Pilight comes with several programs to receive and send data. To install pilight, just follow the [instructions](http://manual.pilight.org/installation.html#linux-debian-based).
Because of a bug with the latest linux kernel, it is actually recommended to use the nightly build.

Some configuration is also needed. I had to set `gpio-platform` to `raspberrypi1b2` and configure the `433gpio` hardware. The `gpio-platform` setting is not yet documented, but will likely be documented when version 8.0 is released.
I have the following configuration file:
```
{
        "devices": {},
        "rules": {},
        "gui": {},
        "settings": {
                "gpio-platform": "raspberrypi1b2",
                "log-level": 6,
                "pid-file": "/var/run/pilight.pid",
                "log-file": "/var/log/pilight.log",
                "webserver-enable": 1,
                "webserver-root": "/usr/local/pilight/webgui",
                "webserver-http-port": 5001,
                "webserver-cache": 1
        },
        "hardware": {
                "433gpio": {
                        "sender": 0,
                        "receiver": 1
                }
        },
        "registry": {}
}
```

# Finding the id of the kaku remote
Since I already have a remote for my kaku switches, I wanted to know the id it is using. For this I used `pilight-receive`.
After running the program you can use the remote and see what is actually received. At first I didn't receive anything,
but by holding the remote directly to the receiver I found the following output (slightly modified):

```
{
        "message": {
                "id": 123456789,
                "unit": 1,
                "state": "off"
        },
        "origin": "receiver",
        "protocol": "arctech_switch",
        "uuid": "0000-00-00-00-000000",
        "repeats": 1
}
{
        "message": {
                "id": 123456789,
                "unit": 1,
                "state": "off"
        },
        "origin": "receiver",
        "protocol": "arctech_switch",
        "uuid": "0000-00-00-00-000000",
        "repeats": 2
}
{
        "message": {
                "id": 123456789,
                "unit": 1,
                "state": "down"
        },
        "origin": "receiver",
        "protocol": "arctech_screen",
        "uuid": "0000-00-00-00-000000",
        "repeats": 1
}
{
        "message": {
                "id": 123456789,
                "unit": 1,
                "state": "off"
        },
        "origin": "receiver",
        "protocol": "arctech_switch",
        "uuid": "0000-00-00-00-000000",
        "repeats": 3
}
{
        "message": {
                "id": 123456789,
                "unit": 1,
                "state": "down"
        },
        "origin": "receiver",
        "protocol": "arctech_screen",
        "uuid": "0000-00-00-00-000000",
        "repeats": 2
}
```

# Controlling the switches
The next step was to test switching the switches using pilight. This can be done by using `pilight-send`. There are several options that can be used:
 - `pilight-send -p kaku_switch -i 123456789 -a -t` to turn on all lights
 - `pilight-send -p kaku_switch -i 123456789 -a -f` to turn off all lights
 - `pilight-send -p kaku_switch -i 123456789 -u 1 -t` to turn on a specific light
 - `pilight-send -p kaku_switch -i 123456789 -u 1 -f` to turn off a specific light
