---
title: requestPermission.md
date: 2019-04-28 10:42:12
tags: Android
---
##Android 应用申请usb权限的两种方式##

> 1.intent filter

在manifest.xml文件中添加,并建立相关感兴趣地usb设备的vid\pid文件，插入usb设备后app会自动弹出权限申请对话框，选择为默认设置后则再次启动app或插入USB设备都不会再次弹出对话框。
在<application 上方插入语句
```
<uses-feature android:name="android.hardware.usb.host"/>
```
指名安卓设备为主机模式

在main activity中添加
```
<intent-filter>
      <action android:name="android.hardware.usb.action.USB_DEVICE_ATTACHED" />
</intent-filter>
   <meta-data
       android:name="android.hardware.usb.action.USB_DEVICE_ATTACHED"
       android:resource="@xml/device_filter" />
```
>2.广播方式。在检测到usb设备后采用广播的方式调用requestPermission进行权限申请，此种方式只要检测到usb设备便会询问，会多次弹出对话框。
>3.修改安卓源码，重新编译。此方式是针对于方式2的弊端，给应用提供默认权限，对usbPermissionActivity进行修改。
