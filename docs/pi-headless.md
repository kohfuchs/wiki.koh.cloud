# Prepare Pi for Headless use

## Aktivate ssh

after flashing the .img to the SD cart, got to the `boot`partition and run

```
touch ssh
```

to create an empty file named ssh.

## Set up WiFi config for your Raspberry Pi

Create a file in this directory (boot) called `wpa_supplicant.conf`

```
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
country=DE
network={
    ssid="WLAN-NAME"
    psk="WLAN-PW"
    key_mgmt=WPA-PSK
}
```