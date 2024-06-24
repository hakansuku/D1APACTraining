# Synchronous monitoring of Continuous Deployment Pipelines using Dynatrace Workflows

#### In this workshop, we will be using Dynatrace Workflows to schedule periodic connection every (60 minutes) to Jenkins using Jenkins API and query data (PULL) to obtain information of all pipelines being executed. You will then ingest (PUSH) the data into Dynatrace as Biz events.

- You will create a token in Jenkins.
- You will create a workflow and trigger a run every 60 minutes. 
- You will create a Javascript code to PULL data using Jenkins API endpoint to retrieve pipeline execution informaiton (pipeline run status, ID , Duration for each stage (Build/Deploy/Test) etc. Then will PUSH (ingest) the information as bizevents into Dynatrace.
- You will validate the information using Notebooks app and DQL to observe the bizevents ingested.
- You will create a dashboard to visualize the events ingested

## Create a token in Jenkins for use in Jenkins API
> - Login to Jenkins

 - Click Manage Jenkins to access Jenkins management page
 - Select Users

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/credentials.png?raw=true)

- Click on configuration icon for admin user
  
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/useradmin.png?raw=true)

> Now generate a new token.  This new token heredits the access permissions of the admin user.

- Click Add new Token button
- Enter any name for the token
- Click Generate button

> NOTE: Please copy and save the generated token as you will be using later for authorizing Jenkins API calls.

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/jenkinsnewtoken.png?raw=true)

## Create PULL and PUSH workflow in Dynatrace Workflows app

- Open Dynatrace Workflows APP
- Click  + Workflows  button
- Name the workflow "Pull & Push Bizevents"

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/workflowpushandpull.png?raw=true)

## Create a time interval trigger 
> trigger workflow to run every 60 minutes

- Select Time Interval trigger
- Enter 60
- Click Save

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/runevery60save.png?raw=true)

## Create New task - type Run Javascript
> Add a new task under the trigger and define the type as Javascript. You don't need to know this code as it is specific to Jenkins API.  Customers may be using Ansible or Azure DevOps etc... Just remenber that Dynatrace Workflows can use Javascript code to query CI/CD tools to obtain pipeline related information for monitoring and triggering actions based on the events.

- Click + icon under schedule box
- select Run Javascript

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/NewtaskJS.png?raw=true)

> Next we will add the Javascript code to this task

- Name the task as "pull_jenkins_data_n_push_bizevents"
- Delete existing default code.  Copy and paste the en Javascript code below
- Click SAVE button

> #### NOTE :  MODIFY JenkinsBaseUrl value to your Jenkins Url IP  and MODIFY JENKINS_API_TOKEN with your Jenkins token generated previously

```
/*
* This function will run in the DYNATRACE JavaScript runtime.
* For information visit https://dt-url.net/functions-help
*/
import { execution } from '@dynatrace-sdk/automation-utils';
import { businessEventsClient } from '@dynatrace-sdk/client-classic-environment-v2';
import { credentialVaultClient } from "@dynatrace-sdk/client-classic-environment-v2";



/*Function to pull build data from CICD tool - in this case, Jenkins*/
export default async function ( {execution_id} ) {
  let jenkinsBaseUrl = "http:// < YOUR JENKINS IP > :8080/";
  const JENKINS_USER = 'admin';
  const JENKINS_API_TOKEN='< YOUR TOKEN STRING >'
  
  // Fetch Jenkins crumb
  const crumbResponse = await fetch(`${jenkinsBaseUrl}/crumbIssuer/api/xml`, {
    headers: {
      'Authorization': `Basic ${btoa(JENKINS_USER + ':' + JENKINS_API_TOKEN)}`,
    },
  });
  if (!crumbResponse.ok) {
    const crumbResponseText = await crumbResponse.text();
    throw new Error(`Failed to fetch Jenkins crumb. Response status: ${crumbResponse.status}. Response text: ${crumbResponseText}`);
  }
  const crumbXml = await crumbResponse.text();
  const crumb = (crumbXml.match(/<crumb>(.*?)<\/crumb>/) || [])[1];

  const apiPullJobNames = `${jenkinsBaseUrl}/api/json?tree=jobs[name]`;
  console.log(apiPullJobNames);
  const jobsResponse = await fetch(apiPullJobNames, {
    method: 'GET',
    headers: {
      'Authorization': `Basic ${btoa(JENKINS_USER + ':' + JENKINS_API_TOKEN)}`,
      'Jenkins-Crumb': crumb,
    },
  });
  if (!jobsResponse.ok) {
    const jobsResponseText = await jobsResponse.text();
    throw new Error(`Failed to fetch Jenkins build. Response status: ${jobsResponse.status}. Response text: ${jobsResponseText}`);
  }
  const responseData = await jobsResponse.json();
  const jobNames=[];
  for (const jobname of responseData.jobs) {
    jobNames.push(jobname.name);
  }
  console.log(jobNames);
  for (const jobName of jobNames) {
    const apiUrl = `${jenkinsBaseUrl}/job/${jobName}/api/json?tree=builds[number,url,timestamp,building,duration,result,actions[causes[*]]]{0,500}`;
  
    // Fetch builds within the timeframe
    const buildsResponse = await fetch(apiUrl, {
      method: 'POST',
      headers: {
        'Authorization': `Basic ${btoa(JENKINS_USER + ':' + JENKINS_API_TOKEN)}`,
        'Jenkins-Crumb': crumb,
      },
    });
  
    if (!buildsResponse.ok) {
      const buildsResponseText = await buildsResponse.text();
      throw new Error(`Failed to fetch Jenkins builds. Response status: ${buildsResponse.status}. Response text: ${buildsResponseText}`);
    }
    const buildsData = await buildsResponse.json();
    console.log(jobName);
    bizevents(buildsData, jenkinsBaseUrl, JENKINS_USER, JENKINS_API_TOKEN, jobName, crumb);
  }
}

/*Function to send the build details as bizevents*/
async function bizevents ( buildsData, jenkinsBaseUrl, JENKINS_USER, JENKINS_API_TOKEN, jobName, crumb ) {
    
  const startTimeEpoch = Date.now() - 60 * 60 * 1000; //60 is the minutes
  const endTimeEpoch = Date.now();

  const builds=[];
  // Process each build
  if (buildsData && buildsData.builds) {
    for (const build of buildsData.builds) {
      let buildTimestampEpoch = build.timestamp;
      if (build.result && (buildTimestampEpoch >= startTimeEpoch && buildTimestampEpoch <= endTimeEpoch)) {
        builds.push(build.number);
        const buildNumber = build.number;
        const buildUrl = build.url;
        const buildTimestamp = build.timestamp;
        const buildStatus = build.building ? 'Building' : (build.result === 'SUCCESS' ? 'Success' : 'Failure');
        const buildDuration = build.duration;
        const result = build.result;
        
        let buildUserId = 'Unknown';
        let buildUserName = 'NoName';
        const eventType = 'buildevents';
        const buildCausesAction = build.actions && build.actions.find((action) => action && action._class === 'hudson.model.CauseAction');
        const buildCauses = buildCausesAction ? buildCausesAction.causes : [];
  
        for (const cause of buildCauses) {
          if (cause._class === 'hudson.model.Cause$UserIdCause') {
            buildUserId = cause.userId;
            buildUserName = cause.userName;
            break;
          }
        }
        console.log(builds);
        //Populate bizevents object from buildsData
        const buildDetail = {
               "job-name": jobName,
               "buildNumber": buildNumber,
               "buildTimestamp": buildTimestamp,
               "status": buildStatus,
               "buildDuration": buildDuration,
               "buildUserId": buildUserId,
               "buildUserName": buildUserName,
               "buildResult":result,
               "event.type":eventType
        };
        businessEventsClient
        .ingest({
        body: buildDetail,
        type: 'application/json',
     })
     .then(() => console.log('Event ingested'))
     .catch((e) => console.error('Failed to ingest event: ' + e));

      }
    }
    identifyStageDetailAndPushAsBizevents(builds, jenkinsBaseUrl, JENKINS_USER, JENKINS_API_TOKEN, jobName, crumb);
  }
}

async function identifyStageDetailAndPushAsBizevents(builds, jenkinsBaseUrl, JENKINS_USER, JENKINS_API_TOKEN, jobName, crumb) {
  console.log("in identifyStageDetail");
  
  // Get details of the various stages of the build
  for (const build of builds) {
    const apiUrl = `${jenkinsBaseUrl}/job/${jobName}/${build}/wfapi/describe`;
    console.log(apiUrl);
    // Fetch builds within the timeframe
    const buildsResponse = await fetch(apiUrl, {
      method: 'POST',
      headers: {
        'Authorization': `Basic ${btoa(JENKINS_USER + ':' + JENKINS_API_TOKEN)}`,
        'Jenkins-Crumb': crumb,
      },
    });

    if (!buildsResponse.ok) {
      const buildsResponseText = await buildsResponse.text();
      throw new Error(`Failed to fetch Jenkins build details. Response status: ${buildsResponse.status}. Response text: ${buildsResponseText}`);
    }
    const stagesData = await buildsResponse.json();
    
    for (let j = 0; j < stagesData["stages"].length; j++) {
      const stageDetail = {
                 "jobname": jobName,
                 "buildnumber": stagesData["id"],
                 "stagename": stagesData["stages"][j]["name"],
                 "status": stagesData["stages"][j]["status"],
                 "stageDuration": stagesData["stages"][j]["durationMillis"],
                 "pauseInQueueDuration":stagesData["stages"][j]["pauseDurationMillis"],
                 "event.type":"stageType"
        };
        console.log("STAGESDATA");
        console.log(stageDetail);
        businessEventsClient.ingest({
            body: stageDetail,
            type: 'application/json',
      })
      .then(() => console.log('Event ingested'))
      .catch((e) => console.error('Failed to ingest event: ' + e));
    }
   }
  }
```
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/javascriptcode.png?raw=true)

