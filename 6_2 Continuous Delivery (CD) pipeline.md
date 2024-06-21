# Creating a simple Continuous Delivery (CD) pipeline

#### In this workshop you will create a continuous delivery pipeline in Jenkins.  A continuous delivery pipeline automates the entire software release process. 
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/pipeline.png?raw=true)

- You will be defining 3 stages:  Build -> Deploy -> Test.
- You will schedule it to run every 15 minutes.
- For each stage we will use Business events API to ingest JSON-format data into Dynatrace via the /bizevents/ingest endpoint.
- You will be able to access records stored in Grail by making DQL queries (fetch bizevents) using Notebooks application.

## Create a new pipeline
- Click New item from the Jekins Main page
  
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/newitem.png?raw=true)
  
- Enter item name (eg. example-pipeline)
- Select pipeline
- click OK
  
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/examplepipelineok.png?raw=true)

Scroll down to Build Triggers section.

- Click on Build periodically
- Enter frequency under Schedule box (eg. # Every fifteen minutes)

```
H/15 * * * *
```

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/schedule15.png?raw=true)

> Note: you can click on (?) icon next to Schedule to find out more about the frequency format expression.

## Defining stages in the pipeline

Scroll further down to Pipiline section.

- paste the following script code to define 3 stages

```
pipeline {
    agent any 
    stages {
        stage('Build') {
            steps {
                echo "Running XYZ tasks in Build stage!"
            }
        }
        stage('Deploy') {
            steps {
                echo "Running XYZ tasks in Deploy stage!"
            }
        }
        stage('Test') {
            steps {
                echo "Running XYZ tasks in Test stage!"
            }
        }
    }
}
```

- Click Save button
  
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/stages.png?raw=true)

## Test the pipeline

> Although the pipeline is scheduled for every 15 minutes, You can immediately manually trigger the pipeline at anytime by Clicking on Build Now.  Observe under Build history, a new build run ID gets added and executed.

- Click on Build now. 

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/buildnow.png?raw=true)

> You can also visualize the different stages of the pipeline and drill down to the console output to debug the results of the pipeline run.  

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/SRE/consoleoutput.png?raw=true)

Now you have a Continuous Deployment pipeline which will automatically trigger a run every 15 minutes.

End of Document

 
