# tools

## adb

```text
# lock for devices
adb devices


# use the device over wireless
adb tcpip 3690


# connect via wireless over LAN
adb connect 192.168.1.X:3690

# 
adb disconnect

# send files
adb push nethunter-hammerhead-marshmallow-kalifs-full-2020.1.zip  /sdcard/nethunter-hammerhead-marshmallow-kalifs-full-2020.1.zip 
```

## fastboot + factory reset android

```text
# get the iso from here:
https://developers.google.com/android/images#hammerhead

sudo $(which fastboot) devices


sudo fastboot devices
sudo fastboot oem device-info

fastboot oem unlock
fastboot flash unlock


sudo fastboot flash bootloader bootloader-hammerhead-hhz20h.img
sudo fastboot reboot-bootloader

sudo fastboot flash radio radio-hammerhead-m8974a-2.0.50.2.30.img
sudo fastboot reboot-bootloader

sudo fastboot flash system image-hammerhead-m4b30z/system.img
sudo fastboot flash userdata image-hammerhead-m4b30z/userdata.img

sudo fastboot flash boot image-hammerhead-m4b30z/boot.img
sudo fastboot flash recovery image-hammerhead-m4b30z/recovery.img
sudo fastboot erase cache
sudo fastboot flash cache image-hammerhead-m4b30z/cache.img

```

