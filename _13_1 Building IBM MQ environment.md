# 13_1_1 Run a IBM MQ sample environment on an AWS EC2 instance. 

## In this tutorial we will spin a Ubuntu linux AWS::EC2 instance , we run a Docker IBM MQ sample on an AWS EC2 instance. This setup is commonly used for rapid development and testing IBM MQ
- Prepare a development ubuntu VM instance (refer to previous exercise 1_2)
- SSH into the Ubuntu terminal 
  
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/OTELcollector/SSHterminal.jpg)

- Update, Upgrade ubuntu and install Docker
```
sudo su
apt update -y
apt upgrade -y
apt install docker.io -y
```

- Pull the IBM MQ Developer Image
> This is using the latest official image from the IBM Container Registry

```
sudo docker pull icr.io/ibm-messaging/mq:latest
```
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/IBMMQ/dockerpull.jpg)

- Create a Persistent Volume
> This is to ensure your queue manager data survives container restarts

```
sudo docker volume create qm1data
```

- Run the IBM MQ Container
> The following command starts a queue manager named QM1, accepts IBM license, and sets an admin password

> -- env LICENSE=accept	Mandatory license agreement.

> -- env MQ_QMGR_NAME=QM1	Sets the name of the message broker.

> --volume qm1data:/mnt/mqm	Ensures message data isn't lost when the container stops.

> --publish 1414:1414	Opens the channel for application messaging.

> --publish 9443:9443	Opens the web management console.

> --detach	Runs the process in the background.


```
sudo docker run --env LICENSE=accept \
  --env MQ_QMGR_NAME=QM1 \
  --volume qm1data:/mnt/mqm \
  --publish 1414:1414 \
  --publish 9443:9443 \
  --detach \
  icr.io/ibm-messaging/mq:latest
```
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/IBMMQ/dockerrun.jpg)

- Validate IBM MQ container is running and host ports 1414 and 9443 are mapped
> Run ps -ef command
```
ps -ef
```
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/IBMMQ/psef.jpg)

- Open a bah terminal inside the docker container
> Use the docker container id
```
docker exec -u 0 -it <your container id> /bin/bash
```
- Run MQSC within docker container
> runmqsc is a command-line utility in IBM MQ used to administer queue managers by issuing MQSC (Message Queue Scripting Commands) commands
```
runmqsc
```
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/IBMMQ/runmqsc.jpg)

- create a Server-connection channel for QM1
> This command is used to create a Server Connection (SVRCONN) channel. In the world of IBM MQ, this is the most common way for a "Client" (like a Java application, a C# program, or the MQ Explorer) to talk to a "Queue Manager."
```
DEFINE CHANNEL(SVRCONN) CHLTYPE(SVRCONN) TRPTYPE(TCP)
ALTER CHANNEL(SVRCONN) CHLTYPE(SVRCONN) MCAUSER('minkook')
```
> You can validate the created CHANNEL via the DISPLAY command
```
DISPLAY CHANNEL(SVRCONN)
```
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/IBMMQ/svrconn.jpg?raw=true)

- (OPTIONAL) Disable connection password check 
> For simplicity, in this workshop we will will configure No Authentication: When CHCKCLNT is set to NONE, valid credentials supplied by applications are not checked, and invalid ones are ignored
```
ALTER AUTHINFO(SYSTEM.DEFAULT.AUTHINFO.IDPWOS) AUTHTYPE(IDPWOS) CHCKCLNT(NONE)
REFRESH SECURITY TYPE(CONNAUTH)
ALTER QMGR CHLAUTH(DISABLED)
```

- create a linux user eg. minkook
> Create your username
```
sudo adduser <Username>
```

- Give the <username> all access permissions (for simplicity we are granting all) 

> The setmqaut command is an IBM MQ control command used to grant, revoke, or manage authorization permissions for users or groups on MQ objects (like queues, channels, or the queue manager itself)

> replace <Username> with your username created
```
setmqaut -m QM1 -n "**" -t queue -p <Username> +alladm +allmqi
setmqaut -m QM1 -n "**" -t topic -p <Username> +alladm +allmqi
setmqaut -m QM1 -n "**" -t channel -p <Username> +alladm +allmqi
setmqaut -m QM1 -t qmgr -p <Username> +alladm +allmqi +connect
```

![]( https://github.com/hakansuku/D1APACTraining/blob/main/images/IBMMQ/adduser.jpg)

