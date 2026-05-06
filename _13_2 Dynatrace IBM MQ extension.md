# 13_1_1 Connect Dynatrace IBM MQ extension to the sample environment. 

## In this tutorial we will use the Dynatrace IBM Extension to monitor the performance of your IBM MQ queue manager objects and collect performance metrics from queue managers remotely using an Activegate.
- Launch Extensions app from dynatrace UI
  
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/IBMMQ/extensionapp.jpg)

- Select Add configuration
  
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/IBMMQ/addconfig.jpg)

- Select Activegate to run your extension
  
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/IBMMQ/activegate.jpg)

- Choose Activegate group
  
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/IBMMQ/defaultag.jpg)

- You'll need the public ip of your IBM MQ server
> Get the public ip of your EC2 instance

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/IBMMQ/publicip.jpg)

> Make sure you allow inbount rules for TCP traffic on ports 1414 and 9443 (optional) via the EC2 instance Security tab > security group > inbount rules

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/IBMMQ/securityinbound.jpg)

- Queue Manager connection configuration 
> type public ip : port

> type Queue manager name (QM1)

> type Server-connection Channel (eg. SVRCONN)

> type user (eg. minkook)

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/IBMMQ/QMConn.jpg)

- Choose recommended metrics and Save the configuration
> At the top, type a configuration name eg. MQ_workshop
> for simplicity we are going to leave all recommneded metrics

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/IBMMQ/qmsave.jpg)

- Validate that the configuration is enabled 
> If status is Pending, it means it is deploying the configuration into the Activate.  Click on the Pending (status column) to drill-down for more information.

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/IBMMQ/pending.jpg)

- Select timeframe to grab logs for last 30 minutes

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/IBMMQ/logs.jpg)

- NOTICE There is a warning log - this is intended. 
> Endpoints OK: 0 WARNING: 0 ERROR: 1 Unhealthy endpoints: QM1 - GENERIC_ERROR DEC:15C ERROR: Unable to connect to queue manager QM1. Could not connect to Queue Manager: Code: MQCC_FAILED, Reason: MQRC_NOT_AUTHORIZED. Message: MQJE001: Completion Code '2', Reason '2035'.

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/IBMMQ/warning.jpg)

We will address - How to debug and troubleshoot connection Errors in the next section 13_3

-end of document-


