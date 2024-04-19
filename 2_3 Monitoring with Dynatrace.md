# 2_3 Monitoring with Dynatrace


## 1) Configure Dynatrace Android Gradle plugin

> Android Studio uses Gradle, an advanced build toolset, to automate and manage the compilation process while allowing you to define flexible, custom build configurations. 

From your Dynatrace environment under Digital Experience open Mobile page.
Click on create mobile application
![mobile app](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/mobileappcreate.png?raw=true)

Type in name of the mobile application and press 'Create mobile app' button.

![mobile name](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/monitor.png?raw=true)

Click 'Instrumentation wizard' and select Android platform

![instrumentation wizard](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/mobileappsettings.png?raw=true)

> Dynatrace generates instrumentation code for each different platform making it simple to instrument various mobile technologies. 

Select Kotlin (build gradle.kts) tab and click to copy the classpath generated

![classpathe](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/dependencies.png?raw=true)

In android studio, open the top-level 'build.gradle.kts' file under Gradle Scripts folder
- Insert classpath wrapped within buildscript and dependencies {} as shown below. 


![gradle](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/buildgradlekts.png?raw=true)

- Similarly copy plugin configuration (below) and insert at the botoom of 'build.gradle.kts' file as above.

![manifest](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/applyplugin.png?raw=true)

> Notice configuration code contains the applicationId, beacon URL and privacy settings. 

In our example we will turn off user opt-in flag and disable sessionReplay.
Change the privacy setting and session replay entries as below:
- userOptIn(false)
- sessionReplay.enabled(false)

![iactivity_main](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/privacy.png?raw=true)

To apply changes, press the below icon to Sync changes in gradle file.

![sync gradle](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/synchgradle.png?raw=true)

> Sync ensures that Dynatrace plugin is enabled and libraries can be imported for use during build time.  Dynatrace Auto-instrumentation is now complete.

# 2) Add User Tag and custom action 
Open MainActivity.kt and insert below user tag:
```kotlin
Dynatrace.identifyUser("Minkook Kang"); //tag user name
```
> With user tags, you can analyze a specific user's behavior and experience via user session analysis.
```
val action = Dynatrace.enterAction("send score") //initialize custom action
action.reportValue("score",counter.toLong()) //report score value in Long format
action.leaveAction() // close custom action
Dynatrace.endVisit() // terminate session
```

![mobile app](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/usertagging.png?raw=true)
