# raspberrypi

NOOBS v1.9:
```
Language (l): English (US)
Keyboard (9): us
OSes:
Raspbian

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
$ sudo apt-get install screen
```

Load ssh public key:
```
$ cat ~/.ssh/id_rsa.pub | ssh pi@raspberrypi.local 'cat >> .ssh/authorized_keys'
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
```

Time:
```
%r
```

Setup WiFi:
```
$ sudo vi /etc/wpa_supplicant/wpa_supplicant.conf
# Add
network={
    ssid="SSID"
    psk="Password"
    key_mgmt=WPA-PSK
}
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
$ cd /etc/pagekite.d/
$ sudo cp 80_sshd.rc.sample 80_sshd.rc
$ sudo cp 80_httpd.rc.sample 80_httpd.rc
$ sudo vi 80_httpd.rc
# Change kite to hass-gpv
# Change port from 80 to 8123
```

Install VNC:
```
$ sudo apt-get install tightvncserver
```
Create ~/vnc.sh:
```
#!/bin/sh
vncserver :1 -geometry 1920x1080 -depth 24 -dpi 96
```
Create ~/stopvnc.sh:
```
#!/bin/sh
vncserver -kill :1
```
```
$ chmod +x vnc.sh
$ chmod +x stopvnc.sh
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

Install ifttt-nest-autoaway-trigger:
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

Install homebridge:
```
$ cd ~/Projects/homebridge-config/
$ sudo apt-get install libavahi-compat-libdnssd-dev
$ sudo useradd --system homebridge
$ sudo mkdir /var/homebridge
$ sudo chown homebridge /var/homebridge
$ sudo cp var/homebridge/config.json /var/homebridge/
$ sudo cp etc/default/homebridge /etc/default/
$ sudo cp etc/systemd/system/homebridge.service /etc/systemd/system/
$ sudo npm install -g homebridge
$ sudo npm install -g homebridge-nest
$ sudo npm install -g homebridge-harmonyhub
$ sudo systemctl daemon-reload
$ sudo systemctl enable homebridge
$ sudo systemctl start homebridge
$ sudo systemctl status homebridge
# Verify service is running
```

Install home-assistant:
```
$ sudo apt-get install python3 python3-venv python3-pip
$ sudo useradd -rm homeassistant
$ cd /srv
$ sudo mkdir homeassistant
$ sudo chown homeassistant:homeassistant homeassistant
$ sudo su -s /bin/bash homeassistant 
$ cd /srv/homeassistant
$ python3 -m venv homeassistant_venv
$ source /srv/homeassistant/homeassistant_venv/bin/activate
$ pip3 install homeassistant
$ hass
# Check http://raspberrypi.local:8123
# Ctrl-c
$ exit
$ sudo apt-get install bluetooth libbluetooth-dev
$ cd ~/Projects/home-assistant-config/
$ sudo cp etc/systemd/system/home-assistant.service /etc/systemd/system/
$ sudo systemctl --system daemon-reload
$ sudo systemctl enable home-assistant
$ sudo systemctl start home-assistant
$ sudo systemctl status home-assistant
# Verify service is running
```
Install no-ip
```
$ sudo -s
$ cd /usr/local/src/
$ wget http://www.no-ip.com/client/linux/noip-duc-linux.tar.gz
$ tar xf noip-duc-linux.tar.gz
$ cd noip-2.1.9-1/
$ make install
$ /usr/local/bin/noip2 -C
$ /usr/local/bin/noip2
$ useradd --system noip
$ chown noip:noip /usr/local/etc/no-ip2.conf
$ exit
$ sudo -u noip noip2
```
Install PiVPN
```
$ sudo useradd -rm pivpn
$ curl -L https://install.pivpn.io | bash
```


Cleanup and Reboot:
```
$ sudo apt-get clean
$ sudo apt-get autoremove
$ sudo systemctl reboot
```

Install Cockpit:
```
$ sudo apt-get install autoconf intltool libglib2.0-dev libsystemd-journal-dev libjson-glib-dev libpolkit-agent-1-dev libkrb5-dev libssh-dev libpam-dev libkeyutils-dev glib-networking
$ cd ~/Projects/
$ git clone https://github.com/cockpit-project/cockpit.git
$ cd cockpit
$ mkdir build
$ cd build
$ ../autogen.sh --disable-pcp --disable-doc
$ make
$ sudo make install
$ sudo cp ../src/bridge/cockpit.pam.insecure /etc/pam.d/cockpit
$ sudo sh -c "cat ../src/bridge/sshd-reauthorize.pam >> /etc/pam.d/sshd"
$ sudo systemctl start cockpit.socket
$ sudo systemctl enable cockpit.socket
```
