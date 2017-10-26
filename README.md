#Set up for andriod app using react init :
 
How to build andriod app :
npm install -g react-native-cli

Java Development Kit
and set home varible in bashrc
JAVA_HOME="/usr/lib/jvm/java-1.8.0-openjdk-amd64"

Install Android Studio 

1. Install Android Studio 

Download and install Android Studio. Choose a "Custom" setup when prompted to select an installation type. Make sure the boxes next to all of the following are checked:

Android SDK
Android SDK Platform
Android Virtual Device
Then, click "Next" to install all of these components.

If the checkboxes are grayed out, you will have a chance to install these components later on.
Once setup has finalized and you're presented with the Welcome screen, proceed to the next step.

To run android studio : cd /WorkSpace/android-studio/bin$ sh studio.sh


2. Install the Android SDK 

Android Studio installs the latest Android SDK by default. Building a React Native app with native code, however, requires the Android 6.0 (Marshmallow) SDK in particular. Additional Android SDKs can be installed through the SDK Manager in Android Studio.

The SDK Manager can be accessed from the "Welcome to Android Studio" screen. Click on "Configure", then select "SDK Manager".

The SDK Manager can also be found within the Android Studio "Preferences" dialog, under Appearance & Behavior → System Settings → Android SDK.
Select the "SDK Platforms" tab from within the SDK Manager, then check the box next to "Show Package Details" in the bottom right corner. Look for and expand the Android 6.0 (Marshmallow) entry, then make sure the following items are all checked:

Google APIs
Android SDK Platform 23
Intel x86 Atom_64 System Image
Google APIs Intel x86 Atom_64 System Image
Next, select the "SDK Tools" tab and check the box next to "Show Package Details" here as well. Look for and expand the "Android SDK Build-Tools" entry, then make sure that 23.0.1 is selected.

Finally, click "Apply" to download and install the Android SDK and related build tools.



set home varibale in bashrc
export ANDROID_HOME="/home/shyam/Android/Sdk"
export PATH=$PATH:$ANDROID_HOME/tools
export PATH=$PATH:$ANDROID_HOME/platform-tools

Creating new app
react-native init AwesomeProject

For connecting through Physical device
Plug in your device via USB 
Let's now set up an Android device to run our React Native projects. Go ahead and plug in your device via USB to your development machine.

Next, check the manufacturer code by using lsusb (on mac, you must first install lsusb). lsusb should output something like this:

$ lsusb
Bus 002 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 001 Device 003: ID 22b8:2e76 Motorola PCS
Bus 001 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
These lines represent the USB devices currently connected to your machine.

You want the line that represents your phone. If you're in doubt, try unplugging your phone and running the command again:

$ lsusb
Bus 002 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 001 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
You'll see that after removing the phone, the line which has the phone model ("Motorola PCS" in this case) disappeared from the list. This is the line that we care about.

Bus 001 Device 003: ID 22b8:2e76 Motorola PCS

From the above line, you want to grab the first four digits from the device ID:

22b8:2e76

In this case, it's 22b8. That's the identifier for Motorola.

You'll need to input this into your udev rules in order to get up and running:

echo SUBSYSTEM=="usb", ATTR{idVendor}=="22b8", MODE="0666", GROUP="plugdev" | sudo tee /etc/udev/rules.d/51-android-usb.rules
Make sure that you replace 22b8 with the identifier you get in the above command.

Now check that your device is properly connecting to ADB, the Android Debug Bridge, by running adb devices.

$ adb devices
List of devices attached
emulator-5554 offline   # Google emulator
14ed2fcc device         # Physical device
Seeing device in the right column means the device is connected. You must have only one device connected at a time.

Note : if adb is not showing devices, run sudo apt-get adb


only for Virtual Device (Emulator)
Download Genymotion
download phone settings
run selected phone

Run App:
created local.properties file under android folder in newly created app
paste 
sdk.dir = /home/shyam/Android/Sdk -> Save
adb reverse tcp:8081 tcp:8081
react-native run-android


