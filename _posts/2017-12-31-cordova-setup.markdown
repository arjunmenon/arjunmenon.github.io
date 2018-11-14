---
layout: post
title:  "Simple guide to setup a cordova environment"
date:   2017-12-31 21:54:38 +0530
categories: cordova
---
A dead simple guide to setup a Cordova enviornment with Android tools in Ubuntu/Elementary os

This setup takes almost 1-2 hour based on your connection speed. 

1. Download java
```bash
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt install oracle-java8-installer
```
2. Install the Full Android SDK from [https://developer.android.com/studio/index.html](https://developer.android.com/studio/index.html)  
This step is time consuming.  
The SDK is almost 800MB. It further downloads almost 1GB of Android platform-tools, build-tools and the latest target SDK. Additional 800MB if you choose to include AVD for emulator, to test directly the app in desktop.
You would, later, have to further download any other target SDK you may want to support for development.


3. Setting environment variables
Save this in a new line in your `~/.bashrc` file *(generally hidden and located in your Home folder)*
```bash
export ANDROID_HOME=$HOME/Android/Sdk
export PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools
```

    Reload your terminal using `source ~/.bash_profile`

4. Install cordova
```bash
sudo npm install -g cordova
```

5. Create a Hello World app
```bash
cordova create hello com.example.hello HelloWorld
```
_cordova create `<folder name> <project id> <app name>`_

6. Add platforms you want to build for  
For this, we will focus on Android
```bash
cd hello # change into the newly created folder
cordova platform add android # or add ios
```
It's a good idea to check if everything is setup correctly so far by doing `cordova requirements` in the terminal.

7. Build app  
```bash
cordova build android # or just build or build ios
```
Now this step is again time consuming, 10-15 minutes. This would download many android binaries required to run your cordova project.   
**Happens only once** and again after you include any cordova plugin.  
After that takes less than two second, whenever you modify code and want to see the changes.

8. Finished  
You can now test the app. If you installed the AVD, you can do this using
```bash
cordova emulate android
```
or connect your android phone to your computer and run
```bash
cordova run android --device
```
Running on device may take few minutes if doing it for the first time. After that, it is quick.  
Make sure developer options is turned on with `install by usb` activated.

### Some troubleshooting
#### Check if android is connected properly to computer.

While connecting make sure you set the USB mode in your phone to "charging".  

Activate developer options in your phone.  

Run `adb devices` in your desktop terminal.  
If it shows `not-verified` adjacent to your device id, turn off and then on the developer options in your phone. Then perform these series of steps  
```
sudo adb kill-server
sudo adb start-server
adb devices
```
This should hopefully show your device id properly.  

If the adb does not show your attached devices, then you need to make sure the computer attached with your phone is verified. For this you generally toggle the developer options, which shows a prompt in your phone asking you permission to verify the RSA fingerprint for the device.


