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
