# Creating a simple Continuous Delivery (CD) pipeline

#### In this workshop you will create a continuous delivery pipeline in Jenkins.  A continuous delivery pipeline automates the entire software release process. 
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/pipeline.png?raw=true)

- You will be defining 3 stages:  Build -> Deploy -> Test.
- You will schedule it to run every 15 minutes.
- During each stage we will use Business events API to ingest JSON-format data into Dynatrace via the /bizevents/ingest endpoint.
- You will be able to access records stored in Grail by making DQL queries (fetch bizevents) using Notebooks application.

## Create a new pipeline
- Click New item from the Jekins Main page
  
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/newitem.png?raw=true)
  
- Enter item name (eg. example-pipeline)
- Select pipeline
- click OK
  
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/examplepipelineok.png?raw=true)
