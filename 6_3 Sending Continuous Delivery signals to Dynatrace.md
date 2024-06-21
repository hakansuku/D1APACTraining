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

## Defining custom JSON data structure 

> You will be editing the existing pipeline and create custom data in JSON format which you will later ingest into Dynatrace via API Biz event format.

- Click on the pipeline you created in workshop 6_2 form the main Jenkins dashboard (eg. example-pipeline)

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/mainpipeline.png?raw=true)

> To edit the pipeline

- Select Configure

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/Configure.png?raw=true)

> Scroll down to Pipeline section

- At the top of the script-box add the line to import JSON library
  
```
import groovy.json.JsonOutput
```

- For each of the stages (Build/Deploy/Test) replace the line [echo "Running XYZ tasks in Build stage!"] with below JSON data definition

```
 script {
          def myJSON = readJSON text: '{}'
          myJSON.Jobname = "${env.JOB_BASE_NAME}" as String
          myJSON.BuildUrl = "${env.BUILD_URL}" as String
          myJSON.Stage = "${env.STAGE_NAME}" as String
          myJSON.'event.type' = "CICD Tool" as String
          myJSON.'event.provider' = "${env.BUILD_TAG}" as String
          myJSON.id = "${env.BUILD_ID}" as String
                    
          def jsonFormat = JsonOutput.toJson(myJSON)
          echo "${jsonFormat}"                  
        }
```
> NOTE: Make sure you do this for all the stages. In between the steps {...}.

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/import.png?raw=true)

- Click Save button

> Execute Build Now and observe in the console , observe data in JSON format in each of the stages

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/jsondata.png?raw=true)

## Creating Dynatrace API TOKEN for Business events API to ingest JSON-format data into Dynatrace via the /bizevents/ingest endpoint

- Open Access Token app from Dynatrace SaaS tenant(3rd Gen).

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/APIToken.png?raw=true)

> - Click to Generate new Token

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/generatetoken.png?raw=true)


- Enter TOKEN Name
- search for Write API
- Tick on Write API tokens to add into the selected scopes

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/writeapi.png?raw=true)

> add further two scopes

- search for Ingest
- tick on Ingest bizevents and Ingest events to add both into the selected scopes
  
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/ingestbizevent.png?raw=true)
