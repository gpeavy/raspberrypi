# raspberrypi

NOOBS v1.9:
```
Language (l): English (US)
Keyboard (9): us
OSes:
Raspbian
LibreELEC_RPi2
Data Partition
OSMC_Pi2

Install (i)
```

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
3 Boot Options:
B1 Console
5 Internationalisation Options:
I1 Change Locale: en_US.UTF-8 UTF-8
I2 Change Timezone: America Los Angeles
I3 Change Keyboard Layout: Apple English (US)
I4 Change Wifi Country: US United States
9 Advanced Options: 
```

Time:
```
%r
```

WiFi:
```
Add wifi network
Enter password
```

Install Dataplicity:
```
$ curl -s https://www.dataplicity.com/7tnd0aga.sh | sudo sh
```

Install Pagekite:
```
# Add our repository to /etc/apt/sources.list
$ echo deb http://pagekite.net/pk/deb/ pagekite main | sudo tee -a /etc/apt/sources.list

# Add the PageKite packaging key to your key-ring
$ sudo apt-key adv --recv-keys --keyserver keys.gnupg.net AED248B1C7B2CAC3

# Refresh your package sources by issuing
$ sudo apt-get update

# Install pagekite !
$ sudo apt-get install pagekite
```

Configure Pagekite:
```
$ sudo vi /etc/pagekite.d/10_account.rc
# Enter name and secret
$ sudo cp 80_sshd.rc.sample 80_sshd.rc
$ sudo cp 80_httpd.rc.sample 80_httpd.rc
$ sudo vi 80_httpd.rc
# Change kite to hass-gpv
# Change port from 80 to 8123
```

Install nodejs:
```
$ curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
$ sudo apt-get install nodejs
$ sudo npm install npm@latest -g
```

Clone projects:
```
$ mkdir ~/Projects
$ cd ~/Projects
$ git clone ssh://gpv@GarrettsMacBookPro.local:/Users/gpv/git/ifttt-nest-autoaway-trigger.git
$ git clone ssh://gpv@GarrettsMacBookPro.local:/Users/gpv/git/homebridge-config.git
$ git clone ssh://gpv@GarrettsMacBookPro.local:/Users/gpv/git/home-assistant-config.git
```

Install ifttt-nest-autoaway-trigger
```
$ cd ~/Projects/ifttt-nest-autoaway-trigger/
$ sudo useradd --system autoaway
$ sudo cp etc/default/ifttt-nest-autoaway-trigger /etc/default/
$ sudo cp etc/systemd/system/ifttt-nest-autoaway-trigger.service /etc/systemd/system/
$ sudo npm install -g
$ sudo systemctl daemon-reload
$ sudo systemctl enable ifttt-nest-autoaway-trigger
$ sudo systemctl start ifttt-nest-autoaway-trigger
$ sudo systemctl status ifttt-nest-autoaway-trigger
# Verify service is running
```

Reboot:
```
$ sudo systemctl reboot
```
