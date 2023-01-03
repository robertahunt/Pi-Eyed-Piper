# Pi-Eyed-Piper
Prototype code for pinned insect digitization station at Natural History Museum of Denmark. General setup somewhat based on ALICE (https://www.doi.org/10.17605/OSF.IO/UVWRN)


# Steps for setup
1. Write raspberry pi os to sd card - release 2022-09-22, with settings hostname: PiEyeNE, ssh key, username and password and locale settings
2. Enable device to be run in usb device mode:
    1. with the sd card still in your computer, edit the following in the 'boot' partition of the sd card
        1. config.txt - comment out the line "otg_mode=1" and add "dtoverlay=dwc2" to the bottom of the file
        2. ssh - add an empty file called "ssh" to the boot partition
        3. cmdline.txt - insert "modules-load=dwc2,g_ether g_ether.host_addr=00:22:82:ff:ff:20 g_ether.dev_addr=00:22:82:ff:ff:22" after rootwait. ensure there is one single space on either side of the command, and ensure the mac addresses are different for the different pis. - specifying the mac addresses because by default the mac address changes on reboot, and then the network settings are reset which is annoying
3. Put the sd card into the zero, plug it into power and one cable to your computer. Your computer should now be able to connect via usb-ethernet to the raspberry pi zero. Ensure in your network settings that ipv4 and ipv6 are set to 'shared to other computers'
4. Once it says connected, you should be able to ssh into the pi - ssh pi@pieyene.local (note, must be lowercase)
5. Set the pi to have a static ip address - should stop it from needing to modify the connection every time the pi restarts
5. Set up the pieye service . Run the following:
    1. sudo nano /etc/systemd/system/pieye.service
    2. paste the contents of pieye.service into the file
6. 

TODO
1. Make a service to update the git on the pi automatically
2. Make our own images for each pi? can easily be flashed onto the devices?