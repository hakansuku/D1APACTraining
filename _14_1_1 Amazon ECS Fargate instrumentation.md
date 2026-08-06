# 14_1_1 Instrumenting Amazon ECS Fargate workloads

## In this tutorial we will manually instrument Amazon ECS Fargate workloads integrating Dynatrace OneAgent code modules into your Fargate tasks using an initContainer. The initContainer copies the OneAgent artifacts into a shared ephemeral volume, where environment variables then configure and activate OneAgent.
> Amazon ECS Fargate is a serverless compute engine for Amazon ECS that lets you run containers without managing servers or EC2 clusters.

## 1) Creating an ECS cluster
- In AWS console , go to Elastic Container Service (ECS Fargate)
- Click Create cluster
![](./images/ECS/ecscreate.jpg)
- name the cluster and click Create 
![](./images/ECS/namecluster.jpg)

## 2) Creating secret to store environment variables used for configuration
- In AWS console , go to Secret Manager service
- Click store a new secret
![](./images/ECS/createsecret.jpg)
