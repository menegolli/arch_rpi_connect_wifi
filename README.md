# arch_rpi_connect_wifi
Bash script to connect Raspberry Pi running Arch Linux ARM to a wifi network.

```bash
# as root user

# bring the wlan0 interface up
ip link set wlan0 up

# scan for the SSID you like
iw dev wlan0 scan | grep SSID

# store the password for the selected SSID to a certain configuration file
wpa_passphrase <SSID_name> <SSID_passpword> > /etc/wpa_supplicant/<SSID_name>.conf
# If the network is hidden, add config file inside brackets the following line:
#scan_ssid=1

# launch wpa_supplicant daemon using the specified configuration file
wpa_supplicant -B -i wlan0 -c /etc/wpa_supplicant/<SSID_name>.conf

# get an IP for the wlan0 interface
dhcpcd wlan0

# check that you got actually an IP
ifconfig
```
Of course you can create a bash script out of this and use `cron` to launch it at reboot.
