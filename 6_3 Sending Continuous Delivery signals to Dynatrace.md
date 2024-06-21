# Sending Continuous Delivery (CD) pipeline run signals to Dynatrace for each stage

#### In this workshop, during each stage (Build/Deploy/Test) you will add Dynatrace API call to send custom information (from Jenkins to Dynatrace) for each stage during pipeline execution .

- You will create a custom JSON data structure with the pipeline stage information.
- You will create a Dynatrace token to ingest / write data through Dynatrace API via the /bizevents/ingest endpoint
- You will be adding API call script task within the pipeline for each of 3 stages:  Build -> Deploy -> Test.
- You will be using notebooks to write DQL query to Grail and validate the events information of the pipeline executions.
