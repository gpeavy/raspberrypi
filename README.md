# raspberrypi

NOOBS v1.9:

Language (l): English (US)
Keyboard (9): us
OSes:
Raspbian
LibreELEC_RPi2
Data Partition
OSMC_Pi2

Install (i)

-
Change password:
```
$ passwd
```

Update:
```
$ sudo apt-get update
$ sudo apt-get dist-upgrade
$ sudo apt-get clean
```

Setup bluetooth keyboard and mouse:
```
$ sudo bluetoothctl
# agent on
# default-agent
# scan on
# pair xx:xx:xx:xx:xx (device id)
(if asked for a "PIN code" -> enter that "PIN code" on your bluetooth keyboard and press ENTER on the bluetooth keyboard)
# trust xx:xx:xx:xx:xx (if not asked for a pin code this may work too)
# connect xx:xx:xx:xx:xx
# quit
```

Configure raspi:
```
$ sudo raspi-config
```
3 Boot Options:
B1 Console
5 Internationalisation Options:
I1 Change Locale: en_US.UTF-8 UTF-8
I2 Change Timezone: America Los Angeles
I3 Change Keyboard Layout: Apple English (US)
I4 Change Wifi Country: US United States
9 Advanced Options: 

```
$ systemctl reboot
```

-
Time:
%r

WiFi:
Add wifi network

Install Dataplicity:
```
$ curl -s https://www.dataplicity.com/7tnd0aga.sh | sudo sh
```

