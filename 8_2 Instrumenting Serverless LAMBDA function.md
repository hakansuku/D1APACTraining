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

> - Click on Layer in the function diagram

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/lambda/layer.png?raw=true)

> - Click on add layer button

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/lambda/addlayer.png?raw=true)

> refer to previous generated Amazon Resources Name (note how it contains region ap-southeast-2 (Sydney))

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/lambda/arnawslambda.png?raw=true)

> - select Specify ARN option, and copy and paste from the generated ARN.
- Click Add

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/lambda/addarn.png?raw=true)

> - To test your service, use the API entry point link to generate traffic

> - You are now able to observe lambda service monitored under Services page

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/lambda/services.png?raw=true)

> - check information getting gathered 

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/lambda/lambdainfo.png?raw=true)

> - Go to logs and observe how logs have been captured for analysis

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/lambda/logs.png?raw=true)

> end of document
