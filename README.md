# Setting up your device
##W4118 Fall 2016

Here are the instructions to get your Huawei Honor 5X device ready to write kernel and userspace code for homework 3 and beyond.

##Caution: If you ignore any of these instructions, or do not go in order you will likely brick your device.  You are responsible for your actions here.

#Upgrading your device to Android 6
This is a very easy step.  After you have started up your device, go into Settings -> Updater and install the update.

#Get the fastboot unlock code
Your Huawei device has the bootloader locked by Huawei.  Unlocking the bootloader is required to change the kernel on the device and make other modifications.  This voids the warranty.  The unlocker code can be found [here](https://emui.huawei.com/en/plugin/unlock/index).  You will have to sign up for Huawei Club, after you have signed up for Huawei Club and are logged in you will be able to unlock the bootloader.  The following information is needed: Product Model, Serial Number, IMEI (I had to use IMEI2 to unlock instead of IMEI1), and Product ID.  Instructions on getting the above data is neatly presented on the Huawei website.  Once you have the fastboot unlock code, save it for later.

#Enable developer mode on your device.
For your device to take commands from ADB, we need to enable developer mode.  This is done by going to Settings->About Phone.  In this menu, find the "Build Number" and tap it 7 times to enable developer mode.  Your phone should inform you that You are now a developer!  Congratulations.

#Getting into Fastboot
Connect your device to your physical machine.  After this is done, you have to let VMWare know to connect this device to the VM.  

[VMWare Workstation] With the class VM started, go to VM -> Removable Devices and connect the device to the VM (Disconnect from Host).
[VmWare Fusion] With the class VM started, connect your device.  A dialog should pop up asking you if you want to connect this device to the VM.

If you get stuck on this step KB Articles on the above can be found for [Fusion](https://pubs.vmware.com/fusion-4/index.jsp?topic=%2Fcom.vmware.fusion.help.doc%2FGUID-F081AFAF-7DBB-44FA-BC5B-C41928CFBAE1.html) and [Workstation](https://www.vmware.com/support/ws55/doc/ws_devices_usb_connect.html).

Now you will have to approve this new machine as trusted by your phone so you can issue commands through adb.  You should get a notification in the notification menu of your device (scroll down from the top with the device on the home screen).  Approve this machine as trusted.

In a terminal execute:
adb reboot bootloader

Your device will now reboot and boot into a special menu.  This is fastboot mode.  This allows us to modify system components such as placing a new kernel, or changing the system image.

#Flash images to the device
We have provided images to flash onto your device that make developing and debugging easy.  Once you are in the fastboot mode flash the following images:
fastboot flash recovery recovery.img
fastboot flash boot boot.img
fastboot flash system system.img

#Boot into Recovery and take backups
This is EXTREMELY important.  First reboot your system as normal until you are on the home screen.  With the device connected to the VM, execute
adb reboot recovery

You should enter TWRP (Team Win Recovery Project).  This recovery tool allows us to take backups and restore as needed.  Go into the backup menu and take a backup of the Boot and System partition.  This is done by selecting the "Boot" and "System" option in the checkbox dialog and using the slidebar to take a backup.  After the backup is complete reboot your device to the home screen.

You're all set!
