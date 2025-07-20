---
title: New Box 
date: 2025-07-20 +/-TTTT
categories: [Home Assistant, Hardware]
tags: [hardware] 
description: A few notes to remember when setting up a new mini pc to run home assistant

comments: true
---
Had to set up a new Lenovo M920Q for HASS, did it the using the simple install method of using a live boot Ubuntu stick.
Things to remember.
1. Turn off secure boot before booting into the live usb and ensure UEFI mode is enabled <u>NOT</u> Auto or Bios/Legacy
2. Always check for BIOS updates first.
3. When in the live boot dont mount the drive you intend to install to, if it is mounted unmount it first
4. Follow the instruction on the Home Assistant website, it will go much smoother.
5. Restoring from backups is easy, download the latest from either a share or a running instance if you have one, make sure you have the rescue kit to decrypt backups.
6. To make life easier after setting up a new instance, ensure you alter the network settings so it has the same IP as the old one, shut down the old one before commiting to saving a config on the new one.
7. release any reserved IP addresses on your router so you can associate it with the new units MAC.
8. The last 2 steps will help with the headache of having to alter the MQTT login info of <U>EVERY</u> device you have that uses MQTT and any other device that calls home rather than being polled.
9. If you are using the same Zigbee coordinator on your new instance you can move it over after shutting down the old one, It DOES NOT need to be in the new machine when you restore, no matter what you read.
10. Be prepared for a few issues with Addons not loading or missing integrations, i had none this time.
11. Last one, if left alone the restore from a backup can take upto 45 mins, dont be impatient leave it to do its thing, if you start refreshing browser windows and rebooting stuff you'll screw it up.
LEAVE IT ALONE.

Have fun.