---
layout: post
title: Android Debugging Utilities
description: Some useful code snippets to use Android Debugging Bridge when developing Android applications, also with Unity3d.
tags: android unity3d debugging bash
---

Here are some useful tips when working with Android, based on [Android Debugging Bridge](https://developer.android.com/studio/command-line/adb.html):

### Add `adb.exe` to Path on Windows
* Edit environment Variables Path
* Add `PATH/TO/ANDROID/SDK/platform-tools` to the list of Path

### View IP address of the Android device
```bash
adb.exe shell ifconfig wlan0
```

### View debugging messages (Unity made)
```bash
adb.exe logcat -s Unity ActivityManager PackageManager dalvikvm DEBUG
```

### Copy Android local files to PC
```bash
adb.exe pull /sdcard/PATH/TO/FILE .
```

### Copy multiple Android local files to PC (Linux)
```shell
for file in `adb shell ls /mnt/sdcard/PATH/ | grep $1`
do
    echo $file
    file=`echo -e $file | tr -d "\r"`;
    adb pull /mnt/sdcard/$file $2/$file;
    # Remove it
    adb shell rm /mnt/sdcard/$file
done
```

Thanks for reading. <i class="em em-lq"></i>

