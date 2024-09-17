# 8_1_1 Creating sample lambda function

> Go to AWS console choose region to sydney

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/lambda/lambdaregionsydney.png?raw=true)

> Search and open Lambda page

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/lambda/clicklambda.png?raw=true)

> Click on Create lambda function

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/lambda/createfunction.png?raw=true)

> Add the following configuration to create a lambda function
- choose create from scratch option
- Give a function name
- select python 3.12 as runtime
- select architecture x86_64
- Click create function

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/lambda/mklambda1.png?raw=true)
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/lambda/mklambda2.png?raw=true)

> - Click add trigger

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/lambda/addtrigger.png?raw=true)

> - Select API Gateway and create new API endpoint
> - Select open for security and click Add button

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/lambda/addtrigger2.png?raw=true)

> Refer a trigger API endpoint has been generated.
- Click on the link and test the API trigger.

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/lambda/triggerlink.png?raw=true)

> - Observe your lambda function response in the browser

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/lambda/triggertest.png?raw=true)

> End of Document
