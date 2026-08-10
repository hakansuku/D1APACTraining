# 14_2 Instrumenting sample Nginx application with Oneagent code module for Nginx

## In this tutorial we will define a task definition. The ECS task definition configures an AWS Fargate task that runs an NGINX web server instrumented with Dynatrace OneAgent for application performance monitoring.
> It accomplishes this using the init-container pattern, where a temporary setup container prepares the monitoring files before the main web server starts.  

> When you integrate Dynatrace OneAgent code modules into AWS Fargate tasks using an initContainer (also known as runtime integration), it operates in Application-Only monitoring mode.  Because AWS Fargate is a serverless platform, users do not have administrative access to the underlying virtual machine host or operating system. Consequently, traditional Full-Stack monitoring mode (which requires a root-privileged OneAgent daemon running on the host system to monitor all processes) cannot be utilized

> In this lab we are only showing how to instrument with Oneagent nginx technology module. However (valid technology module values: python, java, dotnet, nodejs, php, go, apache, nginx, all). make sure supported application versions for each technology.

# Creating a task definition 
> Refer https://docs.dynatrace.com/docs/shortlink/aws-fargate#configure-the-task-definition

## 1) Creating a task definition
- In AWS console , go to Elastic Container Service (ECS Fargate) > Task definition 
- Click Create new task definition button and choose Create new task definition with JSON
![](./images/ECS/createtask.jpg)

-  template for the sample application - you will need to modify the below template with your own values

> 1. Rename first line mk-fargate-task with your own task name. 
> 2. Replace all secrets: ARN values with your own ones from your secret manager 

> "valueFrom": "arn:aws:secretsmanager:ap-northeast-2:917226228317:secret:mk-fargate-secret-ZqKPI0:DT_API_URL::"

> "valueFrom": "arn:aws:secretsmanager:ap-northeast-2:917226228317:secret:mk-fargate-secret-ZqKPI0:DT_PAAS_TOKEN::"

> "valueFrom": "arn:aws:secretsmanager:ap-northeast-2:917226228317:secret:mk-fargate-secret-ZqKPI0:DT_TENANT::"

> "valueFrom": "arn:aws:secretsmanager:ap-northeast-2:917226228317:secret:mk-fargate-secret-ZqKPI0:DT_TENANTTOKEN::"

> "valueFrom": "arn:aws:secretsmanager:ap-northeast-2:917226228317:secret:mk-fargate-secret-ZqKPI0:DT_CONNECTION_POINT::"

> 3. Under /ecs/oneagent , Replace "awslogs-region": "ap-northeast-2" with your own Cloudwatch region
> 4. Under /ecs/webcontainer , Replace "awslogs-region": "ap-northeast-2" with your own Cloudwatch region

```
{
    "family": "mk-fargate-task",
    "containerDefinitions": [
        {
            "name": "initoneagent",
            "image": "public.ecr.aws/dynatrace/dynatrace-codemodules:1.329.62.20260107-143121-nginx",
            "cpu": 0,
            "portMappings": [],
            "essential": false,
            "command": [
                "--source=/opt/dynatrace/oneagent",
                "--target=/mnt/dynatrace/oneagent",
                "--technology=nginx"
            ],
            "environment": [
                {
                    "name": "DT_ONEAGENT_OPTIONS",
                    "value": "flavor=default&include=all"
                }
            ],
            "mountPoints": [
                {
                    "sourceVolume": "oneagent",
                    "containerPath": "/mnt",
                    "readOnly": false
                }
            ],
            "volumesFrom": [],
            "secrets": [
                {
                    "name": "DT_API_URL",
                    "valueFrom": "arn:aws:secretsmanager:ap-northeast-2:917226228317:secret:mk-fargate-secret-ZqKPI0:DT_API_URL::"
                },
                {
                    "name": "DT_PAAS_TOKEN",
                    "valueFrom": "arn:aws:secretsmanager:ap-northeast-2:917226228317:secret:mk-fargate-secret-ZqKPI0:DT_PAAS_TOKEN::"
                }
            ],
            "user": "0:0",
            "logConfiguration": {
                "logDriver": "awslogs",
                "options": {
                    "awslogs-group": "/ecs/oneagent",
                    "awslogs-region": "ap-northeast-2",
                    "awslogs-stream-prefix": "ecs"
                }
            },
            "systemControls": []
        },
        {
            "name": "webcontainer",
            "image": "public.ecr.aws/nginx/nginx:1.25.2-alpine-slim",
            "cpu": 0,
            "portMappings": [],
            "essential": true,
            "environment": [
                {
                    "name": "LD_PRELOAD",
                    "value": "/mnt/dynatrace/oneagent/agent/lib64/liboneagentproc.so"
                },
                {
                    "name": "DT_LOGSTREAM",
                    "value": "stdout"
                },
                {
                    "name": "DT_LOGLEVELCON",
                    "value": "INFO"
                }
            ],
            "mountPoints": [
                {
                    "sourceVolume": "oneagent",
                    "containerPath": "/mnt",
                    "readOnly": false
                }
            ],
            "volumesFrom": [],
            "linuxParameters": {
                "initProcessEnabled": true
            },
            "secrets": [
                {
                    "name": "DT_TENANT",
                    "valueFrom": "arn:aws:secretsmanager:ap-northeast-2:917226228317:secret:mk-fargate-secret-ZqKPI0:DT_TENANT::"
                },
                {
                    "name": "DT_TENANTTOKEN",
                    "valueFrom": "arn:aws:secretsmanager:ap-northeast-2:917226228317:secret:mk-fargate-secret-ZqKPI0:DT_TENANTTOKEN::"
                },
                {
                    "name": "DT_CONNECTION_POINT",
                    "valueFrom": "arn:aws:secretsmanager:ap-northeast-2:917226228317:secret:mk-fargate-secret-ZqKPI0:DT_CONNECTION_POINT::"
                }
            ],
            "dependsOn": [
                {
                    "containerName": "initoneagent",
                    "condition": "COMPLETE"
                }
            ],
            "logConfiguration": {
                "logDriver": "awslogs",
                "options": {
                    "awslogs-group": "/ecs/webcontainer",
                    "awslogs-region": "ap-northeast-2",
                    "awslogs-stream-prefix": "ecs"
                }
            },
            "systemControls": []
        }
    ],
    "executionRoleArn": "arn:aws:iam::917226228317:role/ecsTaskExecutionRole",
    "networkMode": "awsvpc",
    "volumes": [
        {
            "name": "oneagent",
            "host": {}
        }
    ],
    "placementConstraints": [],
    "requiresCompatibilities": [
        "FARGATE"
    ],
    "cpu": "256",
    "memory": "512"
}
```
- Save the task definition. 

## 2) Running the task definition in your ECS cluster

- Go to your Clusters and click on your created cluster from previous exercise 14.1
- Click on Tasks tab
- Click on Run new task button

![](./images/ECS/clustertask.jpg)

- Select from the Task definition family dropdown, your task definition created.

![](./images/ECS/runtask.jpg)

> NOTE: revision will be selected to the last revision of your task definition 

> NOTE: Under networking, expand and ensure Public IP is enabled. 

- Finally click Create button at the end of the page. 

- A new task should be visible, click on it to open the information 
> Observe the status and task lifecycle to see progress on deployment. Once deployed it will show as Running (Green)

![](./images/ECS/tasklifecycle.jpg)

- Scroll down and observe the public IP address. 
- Click on open address.  It will open a broser window with the public ip address. 
![](./images/ECS/securitygroup.jpg)

> NOTE the browser page cannot connect, check your security group and allow TCP inbound port 80

- You page should display nginx welcome page (meaning your nginx application is running in ECS. 

![](./images/ECS/nginx.jpg)

## 3) Debug and validate Oneagent instrumentation via logs

> NOTE : we previously added environment variables in the task definition to enable logging, this is not necessary in production and can be removed.  It was added for demonstration purpose in this lab.

> "name": "DT_LOGSTREAM", "value": "stdout" and   "name": "DT_LOGLEVELCON", "value": "INFO" 

- Go to Cloudwatch service
- Under Logs > Log Management section 
![](./images/ECS/loggroups.jpg)
- Click on /ecs/oneagent log group
- Observe the list of log streams generated
- Click to open the latest log stream 
![](./images/ECS/logstream.jpg)

- Similarly open /ecs/webcontainer log group 
- Open the latest log stream 
- Observe the logs generated 

> To validate there is a proper connection to the tenant endpoint look for connection log as below

![](./images/ECS/connected.jpg)

## 4) Validate detected nginx service from Dynatrace tenant

- Go to your Dynatrace tenant
- Run the Services app
- Observe the nginx service being listed on port 80 
- View traces belonging to the nginx service

![](./images/ECS/services.jpg)

- Additionally , Run Infrastructure & Operations app
- Validate that host is visible as the oneagent 


![](./images/ECS/oneagenthost.jpg)

- End of lab Document -

