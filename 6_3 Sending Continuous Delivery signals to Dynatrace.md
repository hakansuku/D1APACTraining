# Sending Continuous Delivery (CD) pipeline signals to Dynatrace

#### In this workshop, during each stage (Build/Deploy/Test) you will add Dynatrace API call to send custom information when the pipeline executes.

- You will create a custom JSON data structure with the pipeline stage information.
- You will create a Dynatrace token to ingest / write data through Dynatrace API via the /bizevents/ingest endpoint
- You will be adding API call script task within the pipeline for each of 3 stages:  Build -> Deploy -> Test.
- You will be using notebooks to write DQL query to Grail and validate the events information of the pipeline executions.

## Add plugin for manipulating JSON data structure

- Click on Manage Jenkins option

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/maangejenkins.png?raw=true)

- Click Plugins
  
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/plugins.png?raw=true)

> Jenkins has numerous plugins that extends its automation capabilities.

- Select Availabe plugins
- type in steps
- Select and install "Pipeline Utility Steps" Plugin

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/steps.png?raw=true)


