# 14_1_1 Instrumenting Amazon ECS Fargate applications

## In this tutorial we will instrument Amazon ECS Fargate application. 
> Amazon ECS Fargate is a serverless compute engine for Amazon ECS that lets you run containers without managing servers or EC2 clusters.
  
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/OTELcollector/SSHterminal.jpg)

- Get root access
```
sudo su
```
- Update, Upgrade ubuntu and install Docker

```
apt update -y
apt upgrade -y
apt install docker.io -y
```

- Pull the IBM MQ Developer Image
> This is using the latest official image from the IBM Container Registry

```
