# Basic Dynatrace Workflows

#### In this workshop we will create a workflow that is triggered on demand, it will access a public API to get 150+ currency exchange rates, we will filter the results for 4 currencies only and ingest as logs into Dynatrace in JSON format. 

> Workflow is a sequence of steps to perform specific to a goal.

## Triggers and Tasks

### 1) Adding a trigger

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

### 2) Adding a task
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

> You should be able to confirm result of the API call section contains JSON format exchange rate data.  We will pass this data to the next task.

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/WORKFLOWS/jsonresult.png?raw=true)

### 3) Adding a second task

- Click + to add a second task of type HTTP request

> In this section we will create a task which will use Dynatrace Environment API to ingest a subset of the exchange rate data (4 currencies only) collected in the previous task.

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/WORKFLOWS/secondtask.png?raw=true)

- [1] Rename the task name
- [2] Choose POST method from the dropdown
  
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/WORKFLOWS/ingest_logs.png?raw=true)

> #### [3] [4] [5] We require the tenant end point information and token. Refer to workshop 3_1 part 3) Ingesting sample log record into Dynatrace via Environment API 2.0 logs/ingest.

- [3]Insert API Request URL and header [4]Authorization and [5]token string as below

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/WORKFLOWS/ingestAPI.png?raw=true)

- [6] In the payload copy and paste

```
[
  {
    "AUD":{{result("get_daily_currency")["json"]["usd"]["aud"]}},
    "KRW":{{result("get_daily_currency")["json"]["usd"]["krw"]}},
    "USD":{{result("get_daily_currency")["json"]["usd"]["usd"]}},
    "JPY":{{result("get_daily_currency")["json"]["usd"]["jpy"]}}
  }
]
```
> Dynatrace Workflows use the Jinja﻿ templating engine to allow for dynamic configurations in workflows. Those expressions provide access to execution parameters, schedule information, event context, and much more.

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/WORKFLOWS/jinja.png?raw=true)

> Note that we have formatted payload in JSON format.  Also defining the fields to 4 currencies AUD , KRW , USD and JPY.  We can retrieve values from the previous task (get_exchange_rate) result (JSON) by using result() from reference expression. Refer to https://docs.dynatrace.com/docs/platform-modules/automations/workflows/reference.  Workflows uses set of powerful Expressions that enable you to reference results from predecessors in a task configuration and define custom conditions.

- Run the workflow.  

> Check both tasks have success labels and validate the input contains the 4 currencies with data from previous task. 

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/WORKFLOWS/success.png?raw=true)

- Go to logs & events app.  
> Observe how 4 fields in the content are automatically recognized and parsed into fields by Dynatrace.

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/WORKFLOWS/logs.png?raw=true)

End of document


