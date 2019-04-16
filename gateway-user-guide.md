# Smart Home Gateway v0.6 User Guide
![Project Things by Mozilla](/images/ThingsGateway-Mozilla.png)

## I. Introduction

Congratulations on choosing to set up your own private Smart Home Gateway. This guide provides an overview of
what is currently referred to as the “Things Gateway” by Mozilla. It is an alpha prototype, v0.6. Hereafter we will
usually just refer to it as the "gateway". 

The gateway lets you directly monitor and control your home over the web. Unlike many smart home hubs and connected 
IoT devices on the market, your data is not stored or processed in the cloud. It stays in your home on the gateway. 
The gateway can often bypass the need for you to purchase an IoT hub for each brand. And instead of downloading a 
different app for each brand, you can manage everything from one place, using any web browser.

This guide will explain how to set up your gateway, connect smart home devices, create rules to automate 
your home, experiment with voice and text-based commands, and a few additional tips.

### Things Gateway Running on Raspberry Pi

The Things Gateway software can be installed onto an 8GB or larger microSD card which is inserted into a 
Raspberry Pi. We recommend the latest model, such as the RPi 3 B+. You can optionally attach Zigbee and 
Z-wave radios that connect to the RPi over USB. To run the gateway software on other devices, refer to the 
"Supported Hardware" section of the project [wiki](https://github.com/mozilla-iot/wiki/wiki). Other than some 
changes in installation and initial setup, most of this guide is agnostic to the actual gateway hardware. 

The following image shows a typical collection of smart home devices, the top row shows the Raspberry Pi, power supply 
and a Zigbee USB dongle. The bottom row shows a door sensor, smart plugs, smart bulb, and motion sensor.

<img src="/images/image53.png" alt="smart home devices" width="400">

### Flashing the microSD Card

First download the Things Gateway image from [here](https://iot.mozilla.org/gateway/). We recommend using 
the [etcher.io](https://www.balena.io/etcher/) program to flash the 
image onto a microSD card (8GB or larger) that is inserted into your computer. Alternatively, some 
[distributors](https://docs.iot-bus.com/en/latest/getting-started/iot-bus-getting-started-with-mozilla.html) 
sell the Raspberry Pi with a microSD card that has been pre-flashed with the Mozilla Things 
Gateway image. Once flashed, insert the microSD card into the Raspberry Pi.

<img src="/images/image54.png" alt="uSD card" width="160">

## II. First Time Setup

In order for your Things Gateway to communicate with your home network, a one-time connection setup process must be completed.

### Power Up

Make sure the microSD card is plugged into the Raspberry Pi, and optionally plug USB dongles, such as 
Zigbee and Z-wave, into one of the four USB ports. The additional USB dongles allow the gateway to communicate 
with devices that don’t use Wi-Fi, Bluetooth, or other IP networking protocols.

<img src="/images/image1.png" alt="power on gateway">

Plug the gateway into a power outlet using at least a 2A USB power supply. (Cell phone charging USB power adapters 
will not provide sufficient power to run a Raspberry Pi gateway.) After applying power, you will need to wait 2-3 minutes 
for compressed software images to be unpacked, and for various install scripts to run, before proceeding to the next step.

### Connect to Wi-Fi

Using your laptop, connect to the Wi-Fi network called `Mozilla IoT Gateway`. 

<img src="/images/image8.png" alt="Mozilla IoT Gateway SSID" width="300">

(Note that it takes several minutes after first time power on before the network name will appear in the scanned 
list of Wi-Fi networks.)

Upon connecting to `Mozilla IoT Gateway`, a welcome screen will pop up automatically, showing a list of other 
nearby Wi-Fi networks. Select your home Wi-Fi network from the list, and enter your Wi-Fi password. If successful, 
this step will connect your gateway as a Wi-Fi client of your home network. Alternatively, you can directly connect 
the gateway using an ethernet cable to your local area network (LAN), for example by plugging into a LAN port of 
your home Wi-Fi router. 

<img src="/images/image19.png" alt="SSID list" width="800">

You can change the Wi-Fi network that the gateway is connected to by powering it up in a new location, where the 
previous network is not accessbile. It will revert to broadcasting the `Mozilla IoT Gateway` network name, and you 
can repeat the above steps. You can provision the gateway for as many different Wi-Fi networks as you want.

**TIP**: If you are cnnnected to `Mozilla IoT Gateway` but you don’t see the welcome screen, you can try 
typing http://192.168.220.1 into your web browser’s address bar to manually navigate to the page. If the page 
still does not load, then you are not connected to the gateway. Check your Wi-Fi network and try again.

### Choose Your Own Unique Web Address

Your Mozilla Things Gateway should now be connected to your home network. To proceed, your computer will need 
to be connected to the same network. 

The next step is to give your gateway its own unique domain name and to create a user account to secure access 
to it. Your smart home data are stored locally on your gateway, not in the cloud. Only you can access your 
gateway to control your smart home devices safely and securely, whether at home or remote.

Type `http://gateway.local` into your web browser’s address bar to find your gateway on your home network. 

<img src="/images/image9.png" alt="gateway.local" width="600">

If a web page does not load, you can type the IP address of the gateway instead. 

<img src="/images/image25.png" alt="gateway IP address" width="600">

You can determine the gateway IP address by pinging the hostname gateway.local from the command line terminal 
of your computer. To open a terminal window using Microsoft Windows, type `cmd` into the search bar.

<img src="/images/image38.png" alt="windows cmd" width="600">

To open a terminal window using MacOS, type `terminal` into the search bar.

<img src="/images/image39.png" alt="macos terminal" width="300">

From the command line terminal, type: `ping gateway.local` and look for the IP address in the response.

If using Windows 10, type: `ping -4 gateway.local`

**TIP**: If `http://gateway.local` or `http://<IP_address>` can’t be loaded in your browser, check to make sure 
your laptop is connected to the same home Wi-Fi network that you selected in the previous section. To make sure 
the gateway is connected, you can log into your home Wi-Fi router to look up the gateway IP address. Look at the 
router's DHCP client list and search for the name `gateway` or look for a MAC address starting with `b8:27:eb...`.

<img src="/images/image55.png" alt="router DHCP client list" width="600">

Once you have successfully connected to the gateway in your browser, a Welcome page will load.

<img src="/images/image22.png" alt="create subdomain" width="800">

At this step you need to think of a unique web address name that will hereafter be used to securely access your 
Things Gateway over the Internet. Type your chosen name, enter your preferred email, and select “Create.”

If you previously set up a Things Gateway subdomain, you can reclaim it by entering the same name and email. After this
step successfully completes, you will receive an email asking you to confirm your address. Doing so will allow you 
to "own" and continually renew this subdomain (automatically registered for you with LetsEncrypt), for as long as you want.

### Create Your Own Unique User Account

Finally, create an account which you will thereafter use to log in to your gateway. Now you can securely access your gateway 
and manage its devices from any web browser, anywhere in the world. (Additional user accounts can be added later. 
See `Settings => Users`, and follow a similar account creation process.)

<img src="/images/image5.png" alt="create user account" width="800">

### Bookmark Your Success!

Congratulations if you made it through the setup process! 
Keep in mind that each time you want to control and monitor the devices connected to your Things Gateway, you will need to 
navigate to the web address you just created, which will be of the form `[your_subdomain].mozilla-iot.org`. 

We recommend that you **bookmark** the web address on all devices that you have access to from home. 
It is also handy to save your Things Gateway as a **web application on the home screen** of your phones and tablets.

On Android phones/tablets: 
* In Firefox: Select the “add to home” icon in the address bar (circled in red) to add an app icon to your home screen. 
* In Chrome: Select “Add Things to Home screen”. 

<img src="/images/image3.png" alt="firefox add to home" width="300"><img src="/images/image23.png" alt="firefox as web app" width="300">

On iPhones and iPads: 
* In Safari: Select the Share icon, and then “Add to Home Screen”. 
* (Note that iOS does not currently support an "add to home screen" function for Firefox or Chrome browsers.)

<img src="/images/image35.png" alt="safari share" width="300"><img src="/images/image37.png" alt="safari add to home" width="300">

## III. Adding and Managing Smart Home Devices

### Scan For and Add Smart Devices

Pick a device to add and prepare it for pairing. Typical preparation steps for Zigbee and Z-Wave devices are as follows:
* Smart bulb: screw into a light fixture that it is turned on (bulb should be lit when ready for pairing)
* Smart plug: plug into an outlet
* Other powered devices: plug in and turn on
* Battery-operated devices such as door/window sensors, motion detectors, pushbuttons, dimmer switches, leak detectors, 
temperature sensors, and more: remove tab from battery, or plug in battery, to power on

<img src="/images/image6.jpg" alt="sensor battery tab" width="250">

**TIP**: Some devices come pre-paired with controllers or IoT hubs. First follow the manufacturers instructions to do 
a **factory reset** on those devices before attempting to pair them with your Mozilla gateway. See the Appendix 
for more tips on pairing new devices.

When you are ready to add devices to your Things Gateway, we recommend that you provision devices one at a time. 
First load your secure web address (format [your_subdomain].mozilla-iot.org) and log in to your account.

From the main “Things” page, select the <img src="/images/image10.png" alt="plus" width="20">
button at the bottom right corner. 
The gateway will begin scanning to discover unprovisioned and unconfigured devices that are nearby.

<img src="/images/image33.png" alt="scan things" width="800">

When a new device is found, it will appear on the Things scan page. Rename the device, then select 
‘Save’ to add it, and ‘Done’ when you are finished.

<img src="/images/image2.png" alt="save things" width="800">

**TIP**: When naming your smart devices, we recommend using a name that helps you remember where they are 
located in your home. For example, “Bedroom Light”. Choose simple names that will be easy to remember and use if 
you want to command and control your home using voice commands.

Repeat these discovery steps for each device. Powering them up and scanning for them one at a time helps you 
identify each device. 

### Control Your Things

First learn how to monitor and control each device by checking out its capabilities. Then in the next section 
you can learn to create rules to automate interactions between devices.

Devices are displayed on the Things screen and the Floorplan screen. You can toggle light bulb and smart plugs 
on and off by directly clicking on the device icon. You can also see the current state of devices such as 
door sensors and motion detectors, from these screens. 

<img src="/images/image17.png" alt="things screen" width="800">

To view and control additional details, click the <img src="/images/image18.png" alt="bubble" width="20"> icon 
toward the top-right of a device icon. A detailed thing page should open. 

<img src="/images/image32.png" alt="detailed things screen" width="800">

To edit a device’s name or remove it altogether, select 
the <img src="/images/image34.png" alt="edit" width="20"> icon in the bottom right-hand corner.

<img src="/images/image26.png" alt="edit menu" width="200">

## IV. Rules: Automate Your Home

Now that your Mozilla Things Gateway is set up and your smart things are connected, you can start automating 
your home for your convenience by creating ‘Rules’. Practice creating a rule by following the next few steps. 

### Create a Rule

Navigate to the “Rules” page from the main menu. Click the <img src="/images/image10.png" alt="plus" width="20"> icon 
in the lower right corner to create a new rule. In Rule creation, the basic logic is: if (A), then (B). Optionally, 
you can change “if” to “while” and combine multiple inputs for (A), and take action against multiple outputs for (B). 

<img src="/images/image29.png" alt="new rule" width="800">

Let’s start by grabbing our input: time. Drag the ‘clock’ from the bottom of the screen to the left side of the Rule space. 
Since we want something to occur at 10pm, set the time to ‘10pm’.

<img src="/images/image21.png" alt="clock as input" width="800">

Next we select our output: a smart bulb named "Bedroom Light". Drag the light you want to turn off at 10pm to the right 
side of the Rule space.

<img src="/images/image27.png" alt="light action" width="800">

To complete the rule, select the desired property of the smart light that you want to set at 10pm. 
In this example, we want the bedroom light to turn “Off” at 10pm. Go to the light's drop down menu and select ‘Off’. 
The clock and light bulb rectangles should now be connected by a black line, and the “If” statement under 
your Rule name should be updated to reflect the logic of this rule.

<img src="/images/image20.png" alt="completed rule" width="800">

In the top left hand corner, click the tiny pencil near "Rule Name" to edit the name of your rule. For example, 
you can name this rule “At 10pm, turn off bedroom light”. 
For clock-based rules, the “If” statement below the name is appropriate logic. For other situations, such as 
turning on a light only when a door is open, you can change it to "While" instead. When you have more than 
one input parameter, you can select "And" or "Or" as the logical condition to tie together the input parameters.

Click on the back-arrow button in the upper left-hand corner of the Rule space (next to the name), 
to save the rule and return to the main Rule overview page.

### View/Edit, Disable/Enable, or Remove a Rule

From the main Rules view, each rule is represented by a rectangle. 
* View/Edit. You can view or change a rule by hovering over the middle of the rectangle and selecting the "Edit" button. 

<img src="/images/image40.png" alt="rule mouse over" width="600">

* Disable/Enable. You can disable a rule by toggling the "switch" element to the left, which will turn the circle color 
to grey. You can re-enable the rule by toggling the switch element back to the right, turning the circle back to white.

<img src="/images/image13.png" alt="enable or disable rule" width="300">

* Remove. To remove (permanently delete) a rule, hover over the rule rectangle and click on the "(x)" in the upper 
right-hand corner.

<img src="/images/image41.png" alt="remove rule" width="800">

## V. Floorplan: Map the Location of Your Devices

The Floorplan allows you to view your devices as they are positioned within your home. It shows all your devices, 
consistent with what you would see on the Things page, but it lets you see their states mapped over the layput of 
your home. You can still click an icon to change its state, the same as you would on the Things page. However, 
one interaction difference is that you need to click-and-hold on an icon to open the thing's detailed view. 

### Create a Floorplan

First sketch a floorplan of your home, and save it as a digital image. You can draw one by hand and take a picture of it, 
or use an illustrator tool. (If you take a picture of the floorplan using your smartphone, you can upload the image 
directly to your gateway from the phone's browser.)

<img src="/images/image36.jpg" alt="sketched floorplan" width="600">

**TIP**: Save your digital drawing as an SVG file with white lines and a transparent background, using a tool like Inkscape or Sketch, for a minimalist look.

<img src="/images/image14.png" alt="svg floorplan" width="800">

### Upload Floorplan

Click on the pencil icon <img src="/images/image11.png" alt="pencil" width="20"> in the lower right corner of the floorplan 
page to enter edit mode. An "upload file" button will appear -- click on it to select the floorplan image to be uploaded. 

<img src="/images/image7.png" alt="upload floorplan" width="800">

After the floorplan image is uploaded, make sure you are still in edit mode, and then drag the thing icons from the top 
of the page onto the floorplan. Click the check mark <img src="/images/image28.png" alt="checkmark" width="20"> 
in the lower right corner when done.

<img src="/images/image30.png" alt="position things on floorplan" width="800">

## VI. Add-Ons: Extend your Gateway’s Capabilities

The gateway has an add-ons system so that you can extend its capabilities. A few add-ons are installed by default 
(Web Thing, Zigbee, and Z-Wave) so that your gateway will work with a large number of commercial devices right 
out of the box. However, you can boost support for additional devices if they are supported by an Add-on. You'll 
find the Add-on page under Settings.

### Locate and Install More Add-Ons As Needed

From the Settings menu, select Add-Ons. 

<img src="/images/image12.png" alt="addons" width="800">

To enable more Add-Ons, click the "(+)" button in the lower right to browse the add-on list, 
then select ` + Add` to enable any additional add-ons. For example, if you have TP-Link or HomeKit compatible 
devices at home, you can install their add-ons, then discover and pair the devices so that they can be managed 
by your Mozilla gateway. 

<img src="/images/image24.png" alt="select addon" width="600">

New add-ons will continue to be developed to enable control of newly supported devices, so check back periodically 
to scan new Add-ons in the list. You can submit requests for additional device support in the issues tab of the 
[gateway software development site](https://github.com/mozilla-iot/gateway/issues).

## VII. Experiments

You can try out experimental new features, like the Smart Assistant, by enabling them in Experiments.

### Enable Smart Assistant

From the Settings menu, select Experiments, and then check the box to enable the Smart Assistant. 

<img src="/images/image31.png" alt="enable experiments" width="800">

### Using the Smart Assistant

Once enabled, the smart assistant page can be selected from the main navigation menu. It lets you use voice and 
messaging commands to control the things in your home. The same commands are possible whether using voice or 
typing text input. 

<img src="/images/image4.png" alt="smart assistant" width="800">

The web interface shows both typed and spoken commands that were made recently, as well as the result of the command. 
If a portion of a command that you spoke was misinterpreted, or just missing, try again. Remember to speak loud and 
clear near your PC's microphone.

You can give it commands like “Turn the kitchen light on” and it will respond to you to confirm the action. So far it 
can understand a basic set of commands to turn devices on and off, set levels, set color and set color temperatures.

The first time you click on the microphone icon, your browser will ask for permission to use your computer’s microphone. 
From the popup dialog, click the “Remember this decision” checkbox, then select “Allow”.

Note that in the 0.6 gateway release, voice commands are currently processed using Google's voice assistant API, 
so the audio strings are processed in the cloud. The speech-to-text result is passed back to your gateway. If you instead 
type a command into the text field of the smart assistant screen, those commands are processed locally and do not 
require a connection to the Internet.

## VIII. Additional Settings

Browse the other pages listed under the Settings menu in order to find additional configuration and capabilities 
of the Things Gateway. 

<img src="/images/image43.png" alt="settings menu" width="800">

### Domain

The default localhost name is gateway.local, but you can change it to match your subdomain or choose a different name.

<img src="/images/image42.png" alt="localhost name" width="800">

### Users

You can add as many user accounts as you like, so that everyone has their own unique login. Although all users have the 
same access and control privileges in gateway v0.6, a future feature will be to allow lesser privileges to some users, 
such as children or guests.

<img src="/images/image45.png" alt="user accounts" width="800">

Click the "(+)" icon to provision more user accounts.

<img src="/images/image46.png" alt="add user" width="800">

### Adapters

The adapters page shows which of the Add-ons are currently installed and active. Go to the Add-ons page to add or remove 
adapters that are shown on this page.

<img src="/images/image44.png" alt="adapters" width="800">

### Updates

Assuming your gateway is connected to the Internet, system updates will be applied automatically when a new 
stable release is ready. As of the v0.6 release, new versions are being released approximately quarterly.

<img src="/images/image47.png" alt="updates" width="800">

### Authorizations

Authorizations are enabled in "Settings" by selecting "Developer => Create local authorization". This page shows 
whether or not an authorization has been enabled.

<img src="/images/image48.png" alt="authorizations" width="800">

### Developer

On the "Developer" page you can enable ssh, for connecting directly to the Raspberry Pi console. The default 
username is "pi", and the default password is "raspberry". If you decide to enable ssh, we recommend that you 
immediately ssh into the RPi to change the default password. Type the command `$ passwd` and follow the prompts 
to change the pi user's password.

<img src="/images/image49.png" alt="developer menu" width="800">

Click "View Logs" to see raw logs displayed in your browser.

<img src="/images/image50.png" alt="view logs" width="200">

Click "Create local authorization" to establish a secure web token that can be exchanged with 3rd party 
applications and services that you may want to enable, or simply for accessing the data using your own 
development tools.

<img src="/images/image51.png" alt="create auth" width="800">

## IX. Support

For support, please sign up to our IoT Discourse forum (https://discourse.mozilla.org/c/iot) or email iot@mozilla.com or post issues on [github](https://github.com/mozilla-iot/gateway/issues). 

## Appendix: More on Pairing and Unpairing Smart Devices

💡💡💡💡💡💡💡💡💡💡💡💡

