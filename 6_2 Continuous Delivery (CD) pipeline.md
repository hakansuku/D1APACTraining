# Creating a simple continuous delivery pipeline

#### In this workshop we will create a continuous delivery pipeline in Jenkins.  A continuous delivery pipeline automates the entire software release process. 

- You will be defining 3 stages:  Build -> Deploy -> Test.
- You will schedule it to run every 15 minutes.
- During each stage we will use Business events API to ingest JSON-format data into Dynatrace via the /bizevents/ingest endpoint.
- You will be able to access records stored in Grail by making DQL queries (fetch bizevents) 

## 
