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
