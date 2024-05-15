# Advanced Dynatrace Workflows

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
