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

---


Update:
sudo apt-get update
sudo apt-get dist-upgrade
sudo apt-get clean

Setup bluetooth keyboard and mouse:
sudo bluetoothctl
agent on
default-agent
scan on
pair xx:xx:xx:xx:xx (device id)
(if asked for a "PIN code" -> enter that "PIN code" on your bluetooth keyboard and press ENTER on the bluetooth keyboard)
trust xx:xx:xx:xx:xx (if not asked for a pin code this may work too)
connect xx:xx:xx:xx:xx

Time:
%r

Overscan: Disable
Change password
Boot: To CLI
Auto login: off

WiFi:
sudo iwlist wlan0 scan
Edit /etc/wpa_supplicant/wpa_supplicant.conf:
Add:
network={
    ssid="The_ESSID_from_earlier"
    psk="Your_wifi_password"
}
ifconfig wlan0


sudo apt-get install weavedconnectd
sudo weavedinstaller
