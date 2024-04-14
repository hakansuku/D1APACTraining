# Android mobile app instrumentation

## 1) Getting started with Android studio
> Download latest version of Android studio
https://developer.android.com/studio

![installation guide](https://github.com/hakansuku/D1APACTraining/blob/main/images/managed/installationmail.png?raw=true)

buildscript {
    dependencies {
        classpath("com.dynatrace.tools.android:gradle-plugin:8.+")
    }
}

apply plugin: 'com.dynatrace.instrumentation'
dynatrace {
    configurations {
        sampleConfig {
            autoStart {
                applicationId '73fa53d6-c2f8-4e69-95d8-39d59272ac2a'
                beaconUrl 'https://txm241.managed-dev.dynalabs.io:9999/mbeacon/4bb75d44-6e2e-4280-939f-df8dc14d66d2'
            }
            userOptIn true
            agentBehavior.startupLoadBalancing true
            sessionReplay.enabled true
        }
    }
}

SELECT usersession.userSessionId, usersession.userId, useraction.name, usersession.longProperties.score FROM useraction where usersession.longProperties.score IS NOT NULL AND useraction.name IS 'send score'

Create a mobile application in Dynatrace
Instrument your Android app
Instrument your application via Dynatrace Android Gradle plugin


User action monitoring
Create custom actions
https://docs.dynatrace.com/docs/shortlink/oneagent-sdk-for-android#create-custom-actions

Custom queries, segmentation, and aggregation of session data
How do I get the values that have been reported above within Dynatrace, as well as via your API?
You can create and manage USQL metric events using the Dynatrace web UI.
uacm.cookieclickscore
https://tax37821.dev.dynatracelabs.com/#dashboard;gtf=-6h;gf=all;id=0eba1921-38c0-4eaf-a71c-94c6ac16509f
