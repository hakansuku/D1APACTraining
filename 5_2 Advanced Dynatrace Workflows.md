# Advanced Dynatrace Workflows using Javascript code

> The Run Javascript action for Workflows enables you to build a custom task running JavaScript code in a workflow.

#### In this workshop we will replace the HTTP request action with Javascript action and write code to achieve the same goal as in previous section.

- Duplicate the existing workflow and rename (eg. MK_exchange_rate_javascript)
  
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/WORKFLOWS/duplicate.png?raw=true)

- Select first task (get_exchange_rate)
- Click Change action

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/WORKFLOWS/changeaction.png?raw=true)

## Run Javascript action 
- Select Run Javascript action

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/WORKFLOWS/runjavascript.png?raw=true)

- In the input tab , below //your code goes here. copy and paste below:

```
  const response = await fetch('https://cdn.jsdelivr.net/npm/@fawazahmed0/currency-api@latest/v1/currencies/usd.json');
  const result = await response.json();
  return result;
```

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/WORKFLOWS/yourcode.png?raw=true)

- Click Run and validate results tab. 
> Notice the result set is different data structure (JSON is now USD)

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/WORKFLOWS/resultjavascript.png?raw=true)

- Modify the second step (ingest_filtered_logs) to reflect the data structure change by removing ["JSON"] to adjust to the changed structure. 

> Payload should now look like

```
[
  {
    "AUD":{{result("get_exchange_rate")["usd"]["aud"]}},
    "KRW":{{result("get_exchange_rate")["usd"]["krw"]}},
    "USD":{{result("get_exchange_rate")["usd"]["usd"]}},
    "JPY":{{result("get_exchange_rate")["usd"]["jpy"]}}
  }
]
```

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/WORKFLOWS/payloadjava.png?raw=true)

- Run the workflow and validate the input of the ingest_filtered_logs task.

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/WORKFLOWS/inputtabjava.png?raw=true)

- Finally validate in logs and events app

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/WORKFLOWS/javafinal.png?raw=true)

End of document

