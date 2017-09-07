# Setting up your device
##W4118 Fall 2017

Here are the instructions to get your Huawei Honor 5X device ready to write kernel and userspace code for homework 3 and beyond.

##Caution: If you ignore any of these instructions, or do not go in order you will likely brick your device.  You are responsible for your actions here.  If you are worried about accidentally bricking the device come see us during office hours.

#Upgrading your device to Android 6
This is a very easy step.  After you have started up your device, go into Settings -> Updater and install the update.

#Get the fastboot unlock code
Your Huawei device has the bootloader locked by Huawei.  Unlocking the bootloader is required to change the kernel on the device and make other modifications.  This voids the warranty.  The unlocker code can be found [here](https://emui.huawei.com/en/plugin/unlock/index).  You will have to sign up for Huawei Club, after you have signed up for Huawei Club and are logged in you will be able to unlock the bootloader.  The following information is needed: Product Model, Serial Number, IMEI (I had to use IMEI2 to unlock instead of IMEI1), and Product ID.  Instructions on getting the above data is neatly presented on the Huawei website.  Once you have the fastboot unlock code, save it for later.

#Enable developer mode on your device.
For your device to take commands from ADB, we need to enable developer mode.  This is done by going to Settings->About Phone.  In this menu, find the "Build Number" and tap it 7 times to enable developer mode.  Your phone should inform you that You are now a developer!  Congratulations. Enable USB debugging to have adb connection.

#Setup udev permission on your VM
Power on your VM,
```
wget https://raw.githubusercontent.com/W4118/common/master/51-android.rules
sudo cp 51-android.rules /etc/udev/rules.d/
```
Reboot the VM

#Getting into Fastboot
Connect your device to your physical machine.  After this is done, you have to let VMWare know to connect this device to the VM.  

[VMWare Workstation] With the class VM started, go to VM -> Removable Devices and connect the device to the VM (Disconnect from Host).

[VmWare Fusion] With the class VM started, connect your device.  A dialog should pop up asking you if you want to connect this device to the VM.

If you get stuck on this step KB Articles on the above can be found for [Fusion](https://pubs.vmware.com/fusion-4/index.jsp?topic=%2Fcom.vmware.fusion.help.doc%2FGUID-F081AFAF-7DBB-44FA-BC5B-C41928CFBAE1.html) and [Workstation](https://www.vmware.com/support/ws55/doc/ws_devices_usb_connect.html).

#Flash images to the device
In Settings->Developer Options, enable OEM unlock. Goto fastboot by either

+ Poweroff your device. Hold the Volume DOWN button and Power button at the same time until the boot logo shows up. OR
+ ```adb reboot bootloader```

Your device will now reboot and boot into a special menu.  This is fastboot mode.  This allows us to modify system components such as placing a new kernel, or changing the system image.

Now that you are in fastboot, you need to unlock the bootloader to make modifications.  This is done by executing:
```
sudo fastboot oem unlock <your unlock code>
```
Fill in your unlock code that you noted down earlier. It'll do a factory reset of the device. You'll have to tap the "build number" 7 times again to go to developer mode, and enable Settings->Developer Options->OEM unlock. Also please enable USB debugging to have adb connection.

We have provided images to flash onto your device that make developing and debugging easy.  Once you are in the fastboot mode flash the following images located [here](https://drive.google.com/drive/folders/0B8gV4-XkkODsVHoxei1YWkNnMTA?usp=sharing)
```
fastboot flash recovery recovery.img
fastboot reboot
```
Once installed you'll be able to boot to TWRP recovery by either

+ Power off your device, hold both the Volume UP & DOWN key and hold the power button until the boot logo shows up, release the power button and release the Volume buttons.
+ ```adb reboot recovery```

#Install SuperSU
Download the BETA-SuperSU-v2.74-2-20160519174328.zip file from the aforementioned google drive link. Boot normally and connect your device to computer. Once connected, pull down the android notification bar at the top of the screen, and select "files" in the USB connected section. You should be able to copy the zip to "Internal Storage/Download/". Boot to TWRP by powering off the device fist and holding the keys as described above.

```
INSTALL -> Select Storage [Internel Storage] -> Download -> BETA-SuperSU...zip -> Zip signature verification -> Swipe to confirm Flash -> WAIT For a Few Seconds -> Reboot System
```

#Take backups
Boot to TWRP using either way described above. Go into the backup menu and take a backup of the Boot and System partition.  This is done by selecting the "Boot" and "System" option in the checkbox dialog and using the slidebar to take a backup.  After the backup is complete reboot your device to the home screen.

You're all set!
