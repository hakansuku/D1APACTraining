# 13_3_1 Debug and troubleshoot IBM MQ extension connection issues. 

## In this tutorial we will show how to debug and troubleshoot IBM Extension connection issues.  

- From section 13_2 we encountered a warning error log 
  
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/IBMMQ/warning.jpg)

Log message:

> Endpoints OK: 0 WARNING: 0 ERROR: 1 Unhealthy endpoints: QM1 - GENERIC_ERROR DEC:15C ERROR: Unable to connect to queue manager QM1. Could not connect to Queue Manager: Code: MQCC_FAILED, Reason: MQRC_NOT_AUTHORIZED. Message: MQJE001: Completion Code '2', Reason '2035'.

- Checking MQ Queue manager Logs
> Open a terminal to the MQ server docker instance (using your docker id)

> You can find Queue manager error logs in this folder (/var/mqm/qmgrs/QM1/errors)

> Use cat command to display the logs.
```
docker exec -u 0 -it 7c69ebbde043e56f3b278a57fcbe81371f44331afe9954a23090cd33bb3e07a0 /bin/bash
cd /var/mqm/qmgrs/QM1/errors
ls
cat AMQERR01.LOG
```
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/IBMMQ/qmerrors.jpg)

- Observe the Queue Manager log explanation

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/IBMMQ/explanation.jpg)

- Fix
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/IBMMQ/FIX.jpg)
