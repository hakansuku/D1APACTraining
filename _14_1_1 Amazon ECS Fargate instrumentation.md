# 14_1_1 Instrumenting Amazon ECS Fargate workloads

## In this tutorial we will manually instrument Amazon ECS Fargate workloads integrating Dynatrace OneAgent code modules into your Fargate tasks using an initContainer. The initContainer copies the OneAgent artifacts into a shared ephemeral volume, where environment variables then configure and activate OneAgent.
> Amazon ECS Fargate is a serverless compute engine for Amazon ECS that lets you run containers without managing servers or EC2 clusters.
  
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/OTELcollector/.....jpg)
