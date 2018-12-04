This repo provides an example of gateway provisioning with ansible which can be used on a Raspberry Pi.


## Step 1: Prepare the RPi
* Write the raspbian image to the microSD card
* Enable ssh by creating an empty file called "ssh" in the boot partition
* Put the sd card in the RPi
* Connect the RPi to ethernet and power it up
* Find the IP address of the RPi (if there is a screen connected to it, it is shown)

## Step 2: Use ansible to setup the RPi host name and security
* Set the IP address of the RPi in `inventory_demo.yml` 
* Run `ansible-playbook -i inventory_demo.yml 1-initial-provisioning.yaml`

NOTE: If this is more than a demo, make sure to generate your own key pair in `ansible/private-files`

This ansible script will take care of the basic setup of the RPi: Hostname, change the default password and secure the ssh server to only alllow loging in with a private key.

## Step 3 (Optional): Setup the wifi
* Edit file `2-setup-wifi.yaml` to provide the ssid and password for the WIFI network
* Run `ansible-playbook -i inventory_demo.yml 2-setup-wifi.yaml`

The RPi will reboot and should connect to the wifi. You may then disconnect the ethernet and update the IP address of the RPI in `inventory_demo.yml` to continue over the wifi

## Step 4: Deploy a URL as a "Kiosk"
* Edit file `3-setup-kiosk.yaml` to set the url to display
* Run `ansible-playbook -i inventory_demo.yml 3-setup-kiosk.yaml`

The RPi should reboot and show the given url in a web browser in kiosk mode

## Step 5: Deploy Docker and NodeRED in a container
* Run `ansible-playbook -i inventory_demo.yml 4-setup-nodered.yaml`

This will install docker, deploy a container with nodered and change the kiosk url to show the NodeRed interface.

NOTE: You may need to add a few plugins to your ansible instalation using ansible-galaxy.

NOTE2: The browser may boot up faster than nodered so it may be necessary to reload the page...

## Step 6: Make your own script to deploy your own stuff :-)
