# 2_1 Mobile Development Environment preparation

## 1) Getting started with Android studio
> Download latest version of Android studio
https://developer.android.com/studio

![installation guide](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/install.png?raw=true)
> Download the installer file and run through the default installation until complete.
> Launch Android studio.

## 2) Create a new project
> A project in Android Studio contains everything that defines your workspace for an app, from source code and assets to test code and build configurations.

![installation guide](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/newproject.png?raw=true)

> Select the Empty View activity template and click Next
 - Empty Activity and Empty Views Activity are not the same. Using Empty Activity results in creating a project with Compose, while Empty Views Activity is a project with XML. Compose and XML are both ways to build user interfaces in Android.
> We are using XML as we can view UI design layouts and is graphically intuitive and simple which saves us development time.

![installation guide](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/Prjemptyview.png?raw=true)

> Give the application name CookieClicker, 
We will be using Kotlin language for the workshop Set the configuration as below and click Finish.
- Kotlin is a programming language that makes coding concise, cross-platform, and fun. It is Google's preferred language for Android app development.

![installation guide](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/Prjfinish.png?raw=true)

> Android Studio will download and generate the files required for the project.  Let it run till the generation is complete.  You should be able to see a project folder structure created at the left panel of the Android Studio Integrated Development Environment (IDE).

## 2) Project folder view
> You should see the project folder structure view as below

![project folder view](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/androidappview.png?raw=true)

> If the project folder structure view is different to above.  Change the project folder tructure view from the dropdown as below.

![project folder view select](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/folderview.png?raw=true)

## 3) Configure Android Gradle plugin version

> The Android Studio build system is based on Gradle, and the Android Gradle plugin (AGP) adds several features that are specific to building Android apps. 

> Open the AGP Upgrade Assistant to update Gradle version

![project folder view select](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/agpupgrade.png?raw=true)
> Select and upgrade the version of Gradle to 8.3.2 using the dropdown. 

![project folder view select](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/gradleversion.png?raw=true)

## 4) Configure Android SDK and Tools used by the IDE
> The SDK manager is a tool that allows you to view, install, update, and uninstall packages for the Android SDK.
Click on SDK Manager under Tools tab

![project folder view select](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/SDKmanager.png?raw=true)

> Under SDK Platforms tab , select SDK Platform version 34 if not already installed.

![project folder view select](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/android14.png?raw=true)

> Click to move to the SDK tools tab and select SDK Build tool 34.00 if not already installed.

> Do not worry if below screen is not available or different in your environment move to next step.

![project folder view select](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/androidtools.png?raw=true)

## 5) Configure Android Plugins used by the IDE (OPTIONAL)
> Android Studio Plugins are additional features and customizations that are added to make development easy and fast. 

(OPTIONAL) We will be using Rainbow Bracket Lite , Kotlin language.
Using the Search box, Search for Rainbow Brakets Lite and Kotlin plugin and install.  
- NOTE: Ensure Kotlin plugin version is 232-1.9.0 release.  

![project folder view select](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/kotlinplugin.png?raw=true)

## 6) Configure Android Virtual Devices 
> The Device Manager is a tool you can launch from Android Studio that helps you create and manage Android Virtual Devices (AVD). 

To open the Device Manager click on the mobile icon.  

![Device Manager](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/devicemanager.png?raw=true)

> Click on + button to add a new Virtual Android Device (virtual phone)

Select Pixel 8 phone and click Next

![Add Device](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/pixel8.png?raw=true)

> You can now select the virtual Phone's Android system flavour 

Download Tiramisu click on the down arrow next to Tiramisu. 
Select Tiramisu and click Next

![Add Device](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/tiramisu.png?raw=true)

Click finish

![Add Device](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/AVDfinish.png?raw=true)

> Notice that the created Virtual Device should now be visible in the selection dropdown as below

Click on the Play button to start running the Virtual phone device in the background

![Add Device](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/selectAVD.png?raw=true)

> For enhanced viewing, Right click on the Running Devices section tab and change the View Mode to Undock

![Add Device](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/undockAVD.png?raw=true)

> To control the operation of the phone, you can use the icons on the top bar.

![Add Device](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/runningdevice.png?raw=true)

> Now your environment is ready for application development!

End of Document
