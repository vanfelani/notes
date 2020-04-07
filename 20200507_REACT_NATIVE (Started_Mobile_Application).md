---
id: environment-setup Android Project
title: Setting up the development environment Android Project
---
# Mobile Project development for Android

### this is for the linux developer os, if your other os can read the full documentation of the Mobile Setup project at: [Setting up the development environment](https://reactnative.dev/docs/environment-setup) and select the developer os and target os.
#

## Installing dependencies
You will need Node, the React Native command line interface, a JDK, and Android Studio.

While you can use any editor of your choice to develop your app, you will need to install Android Studio in order to set up the necessary tooling to build your React Native app for Android.

### Node
Follow the installation instructions for your Linux distribution to install Node 8.3 or newer.

### Java Development Kit
React Native requires version 8 of the Java SE Development Kit (JDK). You may download and install OpenJDK from AdoptOpenJDK or your system packager. You may also Download and install Oracle JDK 8 if desired.

### Android development environment
Setting up your development environment can be somewhat tedious if you're new to Android development. If you're already familiar with Android development, there are a few things you may need to configure. In either case, please make sure to carefully follow the next few steps.

### 1.Install Android Studio
Download and install Android Studio. Choose a "Custom" setup when prompted to select an installation type. Make sure the boxes next to all of the following are checked:

Android SDK
Android SDK Platform
Android Virtual Device
Then, click "Next" to install all of these components.

If the checkboxes are grayed out, you will have a chance to install these components later on.

Once setup has finalized and you're presented with the Welcome screen, proceed to the next step.

### 2.Install the Android SDK
Android Studio installs the latest Android SDK by default. Building a React Native app with native code, however, requires the Android 9 (Pie) SDK in particular. Additional Android SDKs can be installed through the SDK Manager in Android Studio.

The SDK Manager can be accessed from the "Welcome to Android Studio" screen. Click on "Configure", then select "SDK Manager".

The SDK Manager can also be found within the Android Studio "Preferences" dialog, under Appearance & Behavior → System Settings → Android SDK.

Select the "SDK Platforms" tab from within the SDK Manager, then check the box next to "Show Package Details" in the bottom right corner. Look for and expand the Android 9 (Pie) entry, then make sure the following items are checked:

Android SDK Platform 28
Intel x86 Atom_64 System Image or Google APIs Intel x86 Atom System Image
Next, select the "SDK Tools" tab and check the box next to "Show Package Details" here as well. Look for and expand the "Android SDK Build-Tools" entry, then make sure that 28.0.3 is selected.

Finally, click "Apply" to download and install the Android SDK and related build tools.

### 3.Configure the ANDROID_HOME environment variable
The React Native tools require some environment variables to be set up in order to build apps with native code.

Add the following lines to your $HOME/.bash_profile or $HOME/.bashrc config file:
```
export ANDROID_HOME=$HOME/Android/Sdk
export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/tools
export PATH=$PATH:$ANDROID_HOME/tools/bin
export PATH=$PATH:$ANDROID_HOME/platform-tools
```

.bash_profile is specific to bash. If you're using another shell, you will need to edit the appropriate shell-specific config file.

Type source $HOME/.bash_profile to load the config into your current shell. Verify that ANDROID_HOME has been added to your path by running echo $PATH.

Please make sure you use the correct Android SDK path. You can find the actual location of the SDK in the Android Studio "Preferences" dialog, under Appearance & Behavior → System Settings → Android SDK.



## Creating a new application
If you previously installed a global react-native-cli package, please remove it as it may cause unexpected issues.

React Native has a built-in command line interface, which you can use to generate a new project. You can access it without installing anything globally using npx, which ships with Node.js. Let's create a new React Native project called "AwesomeProject":

npx react-native init AwesomeProject
This is not necessary if you are integrating React Native into an existing application, if you "ejected" from Expo, or if you're adding Android support to an existing React Native project (see Platform Specific Code). You can also use a third-party CLI to init your React Native app, such as Ignite CLI.

[Optional] Using a specific version or template
If you want to start a new project with a specific React Native version, you can use the --version argument:

```
npx react-native init AwesomeProject --version X.XX.X
```

You can also start a project with a custom React Native template, like TypeScript, with --template argument:

```
npx react-native init AwesomeTSProject --template react-native-template-typescript
```


## Running your React Native application
Run react-native start inside your React Native project folder:

```
cd AwesomeProject
npx react-native start
```

If you use the Yarn package manager, you can use yarn instead of npx when running React Native commands inside an existing project.

On another terminal, run npx react-native run-android:
```
cd AwesomeProject
npx react-native start
```
react-native start starts Metro Bundler, which you can read more about here.

Run react-native run-android inside your React Native project folder:
```
npx react-native run-android
```
If everything is set up correctly, you should see your new app running in your Android emulator shortly.

npx react-native run-android is one way to run your app - you can also run it directly from within Android Studio.

If you can't get this to work, see the Troubleshooting page



