# Mozilla Things Gateway First Time Setup Networking Tricks
![Project Things by Mozilla](/images/ThingsGateway-Mozilla.png)

## Introduction

Main user guide link: 
[“Things Gateway” by Mozilla](https://github.com/kgiori/things-gateway-guide/blob/master/mozilla-gateway-guide.md)

This document provides some tips for bringing up a gateway on a cnference network or other advanced workarounds 
when you run into a captive portal network or some other local network problem.

## Boot the Raspberry Pi and Connect to Local Wi-Fi Network

Insert the uSD card that has been flashed with the [Things Gateway](https://iot.mozilla.org/gateway/) image. 
*Wait several minutes*. Eventually you'll see the RPi's own Wi-Fi network (SSID) called "Mozilla IoT Gateway". 

<img src="/images/image8.png" alt="Mozilla IoT Gateway SSID" width="300">

Upon connecting to `Mozilla IoT Gateway`, a welcome screen will pop up automatically, showing a list of other 
nearby Wi-Fi networks. Select the desired network name from the list, and enter the password. If the list does not pop 
up, try loading http://192.168.220.1 into your browser.

You can change the Wi-Fi network that the gateway is connected to by powering it up in a new location, where the 
previous network is not accessbile. It will revert to broadcasting the `Mozilla IoT Gateway` network name, and you 
can repeat the above steps. You can provision the gateway for as many different Wi-Fi networks as you want.

## Edit Wi-Fi Configuration File Directly

You can alternatively edit the Wi-Fi configuration file directly. For example:
`sudo vi /etc/wpa_sppulicant/wpa_supplicant.conf`

### Ways to connect to the RPi:

1. Connect a special USB to TTL serial cable to three GPIO pins to gain direct console access.
2. Enable ssh by dropping a blank file named "ssh" onto the uSD card.
  1. Connect the Ethernet port to a local network and connect your laptop to that same network, then 
     look up its IP address or try "ping gateway.local" (Linux/MacOS) or "ping -4 gateway.local" (MS Windows 10).
  2. Connect to the RPi as an access point at "Mozilla IoT Gateway"
3. Using serial, you will be prompted at the login "pi:" after the boor process completes. 
   Default password is `raspberry`. Be sure to change it with the `passwd` command right away.
4. Using ssh, login as the pi user. For example: `ssh pi@192.168.1.xyz`. Same password and warning to change as above.


