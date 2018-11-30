# Smart Home Gateway v0.6 User Guide
![Project Things by Mozilla](/images/ThingsGateway-Mozilla.png)

## I. Introduction

Congratulations on choosing to set up your own private Smart Home Gateway. This guide provides an overview of
what is currently referred to as the “Things Gateway” by Mozilla. It is an alpha prototype, v0.6. Hereafter we will
usually just refer to it as the "gateway". 
The gateway lets you directly monitor and control your home over the web, even though all your smart home data stays 
in your home, on the gateway. The gateway often bypasses the need to 
purchase separate hubs or to download apps for each different manufacturer.

This guide will explain how to set up your gateway, connect smart home devices, create rules to automate 
your home, plus a few additional tips.

### Things Gateway Running on Raspberry Pi

The Things Gateway software can be installed onto an 8GB or larger microSD card which is inserted into a 
Raspberry Pi. We recommend the latest model, such as the RPi 3 B+. You can optionally attach Zigbee and 
Z-wave radios that connect to the RPi over USB.

images to upload:
[uSD image] + [Things Gateway w/case] + [USB power supply] + (optional) [Zigbee, Z-Wave USB dongles]

### Flashing the microSD Card

First download the Things Gateway image from [here](https://iot.mozilla.org/gateway/). We recommend using 
the [etcher.io](https://www.balena.io/etcher/) program to flash the 
image onto the microSD card (8GB or larger) that is inserted into your computer. Alternatively, some 
[distributors](https://docs.iot-bus.com/en/latest/getting-started/iot-bus-getting-started-with-mozilla.html) 
sell the Raspberry Pi with a microSD card that has been pre-flashed with the Mozilla Things 
Gateway image. Once flashed, insert the microSD card into the Raspberry Pi.

## II. First Time Setup

In order for your Things Gateway to communicate with your home network, a one-time connection setup process must be completed.

### Power Up

Make sure the microSD card is plugged into the Raspberry Pi, and optionally plug USB dongles, such as 
Zigbee and Z-wave, into one of the four USB ports. The additional USB dongles allow the gateway to communicate 
with devices that don’t use Wi-Fi, Bluetooth, or other IP networking protocols.

Plug the gateway into a power outlet using the provided USB power supply. Wait 2-3 minutes for it to power 
up before proceeding to the next step.

### Connect to Wi-Fi

Using your laptop, connect to the Wi-Fi network called `Mozilla IoT Gateway`. 

(Note that it takes several minutes after first power on before the network name will appear in the scanned 
list of Wi-Fi networks.)

Upon connecting to `Mozilla IoT Gateway`, a welcome screen will pop up automatically, showing a list of other 
nearby Wi-Fi networks. Select your home Wi-Fi network from the list, and enter your Wi-Fi password. If successful, 
this step will connect your gateway as a Wi-Fi client of your home network. Alternatively, you can directly connect 
the gateway using an ethernet cable to your local area network (LAN), for example by plugging into a LAN port of 
your home Wi-Fi router. 

**TIP**: If you don’t see the welcome screen after cnnnecting to `Mozilla IoT Gateway`, you can try typing http://192.168.220.1 
into your web browser’s address bar to navigate to the page.

### Choose Your Own Unique Web Address

Your Mozilla Things Gateway should now be connected to your home network. The next step is to give your gateway its 
own unique domain name and to create a user account to secure access to it. Your smart home data are stored locally 
on your gateway, not in the cloud. Only you can access your gateway to control your smart home devices safely and 
and securely, whether at home or remote.

Type `http://gateway.local` into your web browser’s address bar to find your gateway on your home network. If a 
web page does not load, you can type the IP address of the gateway instead. You can determine the gateway IP address 
by pinging the hostname gateway.local from the command line terminal of your computer.

For example: `$ ping gateway.local` or if using Windows 10: `$ ping -4 gateway.local`

**TIP**: If `http://gateway.local` or `http://<IP_address>` can’t be found, check to make sure your laptop is connected to 
the same home Wi-Fi network that you selected in the previous section. To make sure the gateway is connected, you can log 
into your home Wi-Fi router to look up the gateway IP address. Look at the router's DHCP client list and search for 
the name `gateway` or look for a MAC address starting with `b8:27:eb...`.

At this step you need to think of a unique web address name that will hereafter be used to securely access your 
Things Gateway over the Internet. Type your chosen name, enter your preferred email, and select “Create.”

If you previously set up a Things Gateway subdomain, you can reclaim it by entering the same name and email.

### Create Your Own Unique User Account
Finally, create an account which you will thereafter use to log in to your gateway. Now you can securely access your gateway 
and manage its devices from any web browser. (Additional user accounts can be added later. See `Settings => Users`, and 
follow a similar account creation process.)

### Success!

_Congratulations if you made it through the setup process!_ 
Keep in mind that each time you want to control and monitor the devices connected to your Things Gateway, you will need to 
navigate to the web address you just created, which will be of the form `[your_subdomain].mozilla-iot.org`. 

We recommend that you **bookmark** the web address on all devices that you have access to from home. 
It is also handy to save your Things Gateway as a **web application on the home screen** of your phones and tablets.

On Android phones/tablets: 
* In Firefox: Select the “add to home” icon in the address bar (circled in red) to add an app icon to your home screen. 
* In Chrome: Select “Add Things to Home screen”. 

On iPhones and iPads:  
* In Safari: Select the Share icon, and then “Add to Home Screen”. 
* (iOS does not currently support an "add to home screen" function for Firefox or Chrome browsers.)

## III. Adding and Managing Smart Home Devices

### Scan For and Add Smart Devices

Pick a device to add and prepare it for pairing. Typical preparation steps for Zigbee and Z-Wave devices are as follows:
* Smart bulb: screw into a light fixture that it is turned on (bulb should be lit when ready for pairing)
* Smart plug: plug into an outlet
* Other powered devices: plug in and turn on
* Bettery-operated devices such as door/window sensors, motion detectors, pushbuttons, dimmer switches, leak detectors, 
temperature sensors, and more: remove tab from battery, or plug in battery, to power on

**TIP**: Some devices come pre-paired with controllers or IoT hubs. First follow the manufacturers instructions to do 
a factory reset on those devices before attempting to pair them with your Mozilla gateway.

When you are ready to add devices to your Things Gateway, we recommend that you provision devices one at a time. 
First load your secure web address (format [your_subdomain].mozilla-iot.org) and log in to your account.

From the main “Things” page, select the (+) button at the bottom right corner. The gateway will begin scanning 
to discover unprovisioned and unconfigured devices that are nearby.

When a new device is found, it will appear on the Things scan page. Rename the device, then select 
‘Save’ to add it, and ‘Done’ when you are finished.

**TIP**: When naming your smart devices, we recommend using a name that helps you remember where they are 
located in your home. For example, “Bedroom Light”.

Repeat these discovery steps for each device. Powering them up and scanning for them one at a time helps you 
identify each device. 

### Control Your Things

First learn how to monitor and control each device by checking out its capabilities. Then in the next section 
you can learn to create rules to automate interactions between devices.

Devices are displayed on the Things screen and the Floorplan screen. You can toggle light bulb and smart plugs 
on and off by directly clicking on the device icon. You can also see the current state of devices such as 
door sensors and motion detectors, from the main screens. 

To view and control additional details, click the tiny (*) toward the top-right of a device icon. A new page 
should open. To edit a device’s name or remove it altogether, select the (:) icon in the bottom right-hand corner.

## IV. Rules: Automate Your Home

Now that your Mozilla Things Gateway is set up and your smart things are connected, you can start automating 
your home for your convenience by creating ‘Rules’. Practice creating a rule by following the next few steps. 

### Create a Rule

Navigate to “Rules” on the Things menu.

1. Start in the top left hand corner. To the left of the paintbrush, create a name for your rule. As an example, 
create the rule: “At 10pm, turn off bedroom light”. 
Don’t worry about the “If” statement below the Rule name, this will populate as you add your devices to the Rule space.

2. In Rule creation, the basic logic is: if (A), then (B). Optionally, you can change “if” to “while” and combine 
multiple inputs for (A), and multiple outputs for (B). 
Let’s start by grabbing our input: time. Drag the ‘clock’ from the bottom of the screen to the left side of the Rule space. 
Since we want something to occur at 10pm, set the time to ‘10pm’.

3. Next we select our output: a smart bulb named "Bedroom Light". Drag the light you want to turn off at 10pm to the right 
side of the Rule space.

4. To complete the rule, select the desired property of the smart light that you want to set at 10pm. 
In this example, we want the bedroom light to turn “Off” at 10pm. Go to the light's drop down menu and select ‘Off’. 
The clock and light bulb rectangles should now be connected by a black line, and the “If” statement under 
your Rule name should be updated to reflect the logic of this rule.

5. Click on the back-arrow button in the upper left-hand corner of the Rule space (next to the name), 
to save the rule and return to the main Rule overview page.

### View/Edit, Disable/Enable, or Remove a Rule

From the main Rules view, each rule is represented by a rectangle. 
* View/Edit. You can view or change a rule by hovering over the middle of the rectangle and selecting the "Edit" button. 
* Disable/Enable. You can disable a rule by toggling the "switch" element to the left, which will turn the circle color 
to grey. You can re-enable the rule by toggling the switch element back to the right, turning the circle back to white.
* Remove. To remove (permanently delete) a rule, hover over the rule rectangle and click on the (x) in the upper 
right-hand corner.

## V. Floorplan: Map the Location of Your Devices

The Floorplan allows you to view your devices as they are positioned within your home. It shows all your devices, 
consistent with what you would see on the Things page, but it lets you see their states mapped over the layput of 
your home. You can still click an icon to change its state, the same as you would on the Things page. However, 
one interaction difference is that you need to click-and-hold on an icon to open the thing's detailed view. 

### Create a Floorplan

First sketch a floorplan of your home, and save it as a digital image. You can draw one by hand and take a picture of it, 
or use an illustrator tool. (If you take a picture of the floorplan using your smartphone, you can upload the image 
directly to your gateway from the phone's browser.)

**TIP**: Save your digital drawing as an SVG file with white lines and a transparent background, using a tool like Inkscape or Sketch, for a minimalist look.

### Upload Floorplan

Next click on the pencil icon in the lower right corner of the floorplan page to enter edit mode. An "upload file" 
button will appear -- click on it to select the floorplan image to be uploaded. 

After the floorplan image is uploaded, make sure you are still in edit mode, and then drag the thing icons from the top 
of the page onto the floorplan. Click the check mark in the lower right corner when done.

## VI. Add-Ons: Extend your Gateway’s Capabilities

The gateway has an add-ons system so that you can extend its capabilities. A few add-ons are installed by default (Web Thing, Zigbee, and Z-Wave) so that your gateway will work with a large number of commercial devices right out of the box. However, you can boost support for additional devices if they are supported by an Add-on. You'll find the Add-on page under Settings.

### Locate and Install More Add-Ons As Needed

From the Settings menu, select Add-Ons. To enable more Add-Ons, click the (+) button to browse the add-on list, then select ` + Add` to enable any additional add-ona. For example, if you have TP-Link or HomeKit compatible devices at home, you can install their add-ons, then discover and pair the devices so that they can be managed by your Mozilla gateway. 

New add-ons will continue to be developed to enable control of newly supported devices, so check back periodically at 
the Add-ons list. You can submit requests for additional device support in the issues tab of the 
[gateway software development site](https://github.com/mozilla-iot/gateway/issues).

## VII. Experiments

Try out experimental new features like the Smart Assistant in Experiments.

### Enable Smart Assistant

From the Settings menu, select Experiments, and then check the box to enable the Smart Assistant. 

### Using the Smart Assistant

Once enabled, the smart assistant page can be selected from the main navigation menu. It lets you use voice and 
messaging commands to control the things in your home. The same commands are possible whether using voice or typing text input. 

The web interface shows both typed and spoken commands that were made recently, as well as the result of the command. If a portion of a command that you spoke was misinterpreted, or just missing, try again. Remember to speak load and clear near your PC's microphone.

You can give it commands like “Turn the kitchen light on” and it will respond to you to confirm the action. So far it can understand a basic set of commands to turn devices on and off, set levels, set color and set color temperatures.

The first time you click on the microphone icon, your browser will ask for permission to use your computer’s microphone. From the popup dialog, click the “Remember this decision” checkbox, then select “Allow”.

## VIII. Additional Settings

Browse the other pages listed under the Settings menu in order to find additional configuration and capabilities of the Things Gateway. 

## IX. Support

For support, please sign up to our IoT Discourse forum (https://discourse.mozilla.org/c/iot) or email iot@mozilla.com or post issues on [github](https://github.com/mozilla-iot/gateway/issues). 

## Appendix: More on Pairing and Unpairing Smart Devices

💡💡💡💡💡💡💡💡💡💡💡💡

