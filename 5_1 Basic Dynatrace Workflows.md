# Basic Dynatrace Workflows

#### In this workshop we will create a workflow that is triggered on demand, it will access a public API to get 150+ currency exchange rates, we will filter the results for 4 currencies only and ingest as logs into Dynatrace in JSON format. 

> Workflow is a sequence of steps to perform specific to a goal.

## 1) Triggers and Tasks

> Each action executed in in a workflow is called a step (tasks).


- Open Workflows app
- Create a new workflow

!["workflow"](https://github.com/hakansuku/D1APACTraining/blob/main/images/WORKFLOWS/workflowsapp.png?raw=true)

 - Enter a name to your new workflow 

>  In this section, you will be able to familiarize with basic trigger types.  Notice how workflows can be triggered by 3 main types :
> #### 1) events 2) schedule and 3) on-demand.

 - Select on-demand trigger 

!["entername"](https://github.com/hakansuku/D1APACTraining/blob/main/images/WORKFLOWS/ondemandtrigger.png?raw=true)
> Now this workflow with be only triggered on demand, means it will only run when manually triggered via Run button, or via API call. 

- add a task by pressing the + button

!["add task"](https://github.com/hakansuku/D1APACTraining/blob/main/images/WORKFLOWS/createaction.png?raw=true)

- Choose HTTP
!["add task"]
