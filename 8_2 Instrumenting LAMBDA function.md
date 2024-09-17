# Instrumenting Serverless - LAMBDA function via environment variables

> - Go to Dynatrace Hub page, search for AWS lambda and click.

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/lambda/hublambda.png?raw=true)

> - Click Setup button

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/lambda/setup.png?raw=true)

> Configure 
- select python
- select traces and logs
- press create token button (generate token)
- select configure with environment variables option
- select region (ap-southeast-2) for Sydney

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/lambda/env1.png?raw=true)
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/lambda/env2.png?raw=true)

> NOTE: you will be using the above generated environment variables to instrument your lambda function.

- go to AWS console and open lambda function.  Select configuration tab

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/lambda/configuration.png?raw=true)

- click Environment variables section and click edit button

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/lambda/edit.png?raw=true)

> - Add environment variables (generated in previous section) and press SAVE button.

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/lambda/lambdaenvvariableSAVE.png?raw=true)
