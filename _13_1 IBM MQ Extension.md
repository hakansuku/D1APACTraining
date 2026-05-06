# 13_1_1 Run a Docker IBM MQ sample on an AWS EC2 instance. 

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
