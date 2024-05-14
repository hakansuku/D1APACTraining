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

- Choose action type HTTP Requests
  
> Observe that there are other types of actions that we can select.

!["add task"](https://github.com/hakansuku/D1APACTraining/blob/main/images/WORKFLOWS/HTTPRequest1.png?raw=true)

- 1) Rename the taskname  (eg. get_currency)
- 2) Choose GET from the dropdown list
- 3) Copy & Paste exteranl API URL 
```
https://cdn.jsdelivr.net/npm/@fawazahmed0/currency-api@latest/v1/currencies/usd.json
```
- 4) Save the workflow
- 5) Click Run

!["getexchange"](https://github.com/hakansuku/D1APACTraining/blob/main/images/WORKFLOWS/getexchangerate.png?raw=true)

> The above may fail.  Outbound connections from functions are not allowed by default due to security restrictions. Learn how to configure the environment to access external hosts. More information : https://developer.dynatrace.com/develop/functions/allow-outbound-connections/

- Disable outbound connectinos limit in Settings> Preferences > limit outbound connections. 

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/WORKFLOWS/limitoutbound.png?raw=true)

-  Run the workflow again

- When status is success, click on results tab.

> You should be able to confirm result of the API call section contains JSON format exchange rate data.

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/WORKFLOWS/jsonresult.png?raw=true)


