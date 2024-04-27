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

> NOTE: Similarly you will need add **import com.dynatrace.android.agent.Dynatrace** at the top of the page.

# 3) Define custom action property key to capture reported value from mobile session
> NOTE action.reportValue sends a key-value pairs (String, Long) format. 

In Dynatrace, choose your application , Under mobile app setting , Session and user action properties Add a new property and give the following parameters.

![mobile app](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/scorekey2.png?raw=true)
> You should now have be below score property

![mobile app](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/customkey.png?raw=true)

# 4) Mobile Session analysis 
> Dynatrace user session analysis enables you to slice, dice, and combine your application's user sessions into meaningful segments based on shared characteristics of individual user sessions—operating system, browser type, location, or user tag.
Below example observe how user tag helps identify the user ID of the session. 

![mobile app](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/usersession.png?raw=true)

CLick on user session to open a specific session to view session details
> Observe the user event and action names during the session. 

Locate action name "send score" at the bottom of the session details page.  Click on "Perform Waterfall Analysis"

> Dynatrace captures user experience and performance data by monitoring individual user actions. Typically a user action begins with a click on an HTML control (for example, a button or link). The browser then loads the requested data, either by navigating to a new page or via an XHR/fetch call. JavaScript callbacks are then executed, the DOM tree is built or changed, and the web application is then once again ready for a new user action. Dynatrace Waterfall analysis view is the perfect tool for analyzing all such user action monitoring data in detail.

![mobile app](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/sendscore.png?raw=true)

> Confirm reported value by "send score" custom action in the session. 

![mobile app](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/reportedvalue.png?raw=true)

### Using Dynatrace User Session Query Language (USQL)
> Dynatrace captures detailed user session data each time a user interacts with your monitored application. This data includes all user actions and high level performance data. Using Dynatrace User Sessions Query Language (USQL), you can easily run powerful queries, segmentations, and aggregations on this captured data.

Type in the following query in the User Session Query box and press Run Query

```
SELECT usersession.userSessionId, usersession.userId, useraction.name, usersession.longProperties.score FROM useraction where usersession.longProperties.score IS NOT NULL AND useraction.name IS 'send score'
```
![mobile app](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/query.png?raw=true)
> Notice that no data matches your query. If you have not generated any sessions after defining custom action property key.  Note that it takes longer for sessions to be available for query USQL queries so be patient. 

- Even if you see no data, don't worry proceed to next step.

### Create User session/action Custom metric 
> With USQL metric events, you can extract business-level KPI metrics from your user session and user action data and store these metrics as time series. 
Note prefix uacm. (User Action Custom Metric) and uscm. (User Session Custom Metric) for metric key names.

Click Create custom metrics button. 

![mobile app](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/uacm.png?raw=true)

### Visualize metrics in Data Explorer
Open Data Explorer from Dynatrace.
> change to advanced mode to write custom query in Data Explorer

Type the following query (replace uacm.score with your metric name if different): 
```
uacm.score:splitBy("usersession.userId"):sum:sort(value(sum,descending))
```
> Change to Table format , change to advanced mode , insert Query inside box and click Run query button
> Note: Returned value is the sum of all scores 

![mobile app](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/dataexplorer.png?raw=true)

> You can automatically create a new dashboard tile from any Dynatrace page that includes a Pin to dashboard button. All you need is edit permission for the dashboard. In this example, we create a new dashboard, so you are guaranteed to have edit permission.

### Pin to dashboard 

From Data Explorer .  click on "Pin to dashboard" and create a dashboard to show the results of the query. 



![mobile app](https://github.com/hakansuku/D1APACTraining/blob/main/images/mobile/dashboard.png?raw=true)

> Observe how the table displays the Total number of clicks for the user
You can adjust the timeframe selector to limit the number of sessions within a particular timeframe. 


#### Congratulations,  you have now completed the mobile workshop

End of Document
