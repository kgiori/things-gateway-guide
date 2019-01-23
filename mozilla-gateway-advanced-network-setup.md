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
`sudo vi /etc/wpa_supplicant/wpa_supplicant.conf`

You might edit it to look something like the following (you can add multiple networks):

```
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=US

network={
        ssid="TechConference"
        Key_mgmt=NONE
}

network={
        ssid="mozilla-things"
        psk="some-password”
}
```

### Ways to connect to the RPi:

Wired serial connection between RPi and Laptop USB.
1. Connect a special USB to TTL serial cable to three GPIO pins to gain direct console access. From your 
   laptop terminal window use the screen command. 
   `screen /dev/cu.SLAB_USBtoUART 115200`
2. After the RPi boots, you will see a `login:` prompt. Enter `pi` as the user. The 
   default password is `raspberry`. Be sure to change it with the `passwd` command right away.
   
Connect over an IP network using ssh.
1. Enable ssh by dropping a blank file named "ssh" onto the uSD card.
2. Connect the Ethernet port to a local network and connect your laptop to that same network, then 
   look up its IP address or try "ping gateway.local" (Linux/MacOS) or "ping -4 gateway.local" (MS Windows 10).
3. Using ssh, log in as the pi user. For example: `ssh pi@192.168.1.xyz`.
4. If obtaining an IP address over Ethernet is not available, connect your laptop to the RPi directly 
   as an access point (to "Mozilla IoT Gateway") then `ssh pi@192.168.220.1`
5. Same default `raspberry` password and warning to change it immediately as noted above.



