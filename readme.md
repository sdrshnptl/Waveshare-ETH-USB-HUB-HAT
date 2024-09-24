# setup ETH/USB HUB HAT with raspberry pi zero w

[ETH/USB HUB HAT](https://www.waveshare.com/wiki/ETH/USB_HUB_HAT)



## Setup

#### Edit config.txt by `sudo nano /boot/config.txt`

```bash
[HAT]
# Waveshare
dtoverlay=dwc2,dr_mode=host
```

#### Edit cmdline.txt by `sudo nano /boot/cmdline.txt`

```bash
module-load=dwc2,g_ether
```

### Run `ifconfig`

This should return `eth0` or `enx...`

#### `sudo nano /etc/dhcpcd.conf`

```bash
interface eth0
static ip_address=192.168.1.100/24
static routers=192.168.1.1
# static domain_name_servers=8.8.8.8
```

or

```bash
interface enx00e04c3619ec
static ip_address=192.168.1.100/24
static routers=192.168.1.1
# static domain_name_servers=8.8.8.8
```

### Restart raspberry pi with `sudo reboot`


## Set the Priority for Wi-Fi (wlan0)

`sudo nano /etc/dhcpcd.conf`

```bash
interface enx00e04c3619ec
static ip_address=192.168.1.100/24
static routers=192.168.1.1
static domain_name_servers=8.8.8.8
metric 200


interface wlan0
metric 100
```

restart to take effect `sudo reboot`

