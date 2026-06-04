| # D1APACTraining |
| --- |
 ## This repository is for training internal Dynatrace One Product Specialists on empowering individual technical knowledge via hand-on workshops 

## 📚 Workshop Chapters
## Workshop 1 : Managed Cluster environment

:blue_book: Learning value : 
 - Gain confidence in Linux commands 
 - Gain proficiency using cloud environment. 
 - Improve knowledge supporting on-premise customers 

### [Chapter 1.1: Obtain Dynatrace License](./1_1%20Obtain%20Dynatrace%20License.md)
**Goal:** Generate a Dynatrace cluster license via Development Mission Control for internal testing.
* **Concepts covered:** Account creation, license configuration, allocating unlimited Host Units (HU) and DEM units, and retrieving the installation token.
* **Outcome:** Participants receive a valid Dynatrace Cluster license key and installation instructions via email.

### [Chapter 1.2: Cloud Environment Preparation](./1_2%20Cloud%20environment%20preparation.md)
**Goal:** Provision an AWS EC2 instance to serve as the host server for the Dynatrace Managed Cluster.
* **Concepts covered:** AWS console navigation, configuring Spot Instances, selecting Ubuntu 22.04 LTS AMIs, creating SSH key pairs, storage allocation (300 GiB), hardware sizing (t3.2xlarge), and configuring Security Group inbound rules (Ports 80, 22, 443).
* **Outcome:** A running, correctly sized AWS EC2 instance ready for secure remote connection.

### [Chapter 1.3: Learning the Linux Environment and Preparation](./1_3%20Learning%20the%20linux%20envrionment%20and%20preparation.md)
**Goal:** Establish a secure connection to the newly provisioned host and prepare the operating system.
* **Concepts covered:** SSH connections via MobaXterm using private `.pem` keys, gaining Linux root access (`sudo su`), updating OS packages (`apt update/upgrade`), and monitoring system resources (`htop`, `df -h`). *Includes an appendix on manually partitioning and mounting additional EBS volumes (`lsblk`, `mkfs`, `mount`).*
* **Outcome:** An updated and fully prepared Linux environment ready for the Dynatrace installation.

### [Chapter 1.4: Dynatrace Managed Cluster Installation & Maintenance](./1_4%20Cluster_Installation_maintenance.md)
**Goal:** Install the Dynatrace Managed Cluster software and configure the initial administrative settings.
* **Concepts covered:** Downloading the installer via `wget`, executing the shell installation script with the provided license token, verifying server status via the launcher directory, first-time CMC (Cluster Management Console) setup, enabling Log Monitoring/RUM, and configuring data retention and overload prevention.
* **Outcome:** A fully functional Dynatrace Managed Cluster accessible via a web browser.

## Chapter 2: Mobile Application Development & Dynatrace Monitoring

**Overall Value:** Native mobile application development requires a properly configured IDE and emulator environment. This chapter covers the end-to-end process of building a native Android application from scratch and integrating it with Dynatrace for deep user session monitoring. You will learn to set up Android Studio, build a functional "CookieClicker" UI using XML and Kotlin, and apply Dynatrace auto-instrumentation to capture user interactions, custom metrics, and session data.

### Chapter 2.1: Mobile Development Environment Preparation
**Goal:** Configure Android Studio and set up an Android Virtual Device (AVD) for local testing.
* Android Studio installation and project initialization (Empty Views Activity)
* Android Gradle Plugin (AGP) and SDK configuration (Android 14 / API 34)
* Provisioning an Android Virtual Device (Pixel 8 with Tiramisu)
* **Exercise:** Install the IDE, configure the required Kotlin/Gradle plugins, and successfully boot up a virtual Pixel 8 device in your environment.

### Chapter 2.2: Build Your Native Android Application (CookieClicker)
**Goal:** Develop a functional, interactive Android application using Kotlin and XML layouts.
* Android manifest configuration for network permissions
* XML Layout Editor design (TextView and Buttons)
* Kotlin `MainActivity` logic (button listeners, click counters)
* **Exercise:** Design the CookieClicker UI, wire up the Kotlin logic to increment the counter on click, and test the live application using the Logcat debugger in your emulator.

### Chapter 2.3: Monitoring with Dynatrace
**Goal:** Instrument your native Android app with Dynatrace to monitor user sessions, interactions, and custom metrics.
* Dynatrace Android Gradle plugin configuration and privacy settings
* Implementing User Tags and Custom Actions via the Dynatrace API
* User Session Query Language (USQL) and Data Explorer visualizations
* **Exercise:** Instrument the app using the Dynatrace wizard, capture custom "send score" actions, and build a Dynatrace dashboard tracking total cookie clicks using USQL and custom metric queries.

---

## Chapter 3: Log Management & Dynatrace Pattern Language (DPL)

**Overall Value:** Processing and parsing log data is essential for extracting actionable business and operational intelligence. This chapter explores Dynatrace's log management capabilities, focusing on the Dynatrace Pattern Language (DPL) and the Dynatrace Query Language (DQL). You will learn how to ingest logs via the Dynatrace API and use DPL Architect to structure both unstructured text and nested JSON payloads, turning raw log data into queryable, metric-ready attributes.

### Chapter 3.1: Log Management Environment Preparation
**Goal:** Authenticate and interact with the Dynatrace Environment API to manually ingest log records.
* Dynatrace API access token generation with log ingest scopes
* Swagger UI configuration for REST API interaction
* Sending HTTP POST requests to the `/logs/ingest` endpoint
* **Exercise:** Generate an ingest token, authenticate via Swagger UI, push a sample order-fallout log payload to the API, and validate its arrival in the Dynatrace Logs & Events app.

### Chapter 3.2: Parse Unstructured Text Log Data using DPL
**Goal:** Use DPL Architect to extract specific data fields from raw, unstructured log text.
* Understanding DPL matchers (`DATA`) and pointer traversal
* Extracting variables and defining data types (`JSONTIMESTAMP`, `INT`)
* Creating and testing Dynatrace log processing rules
* **Exercise:** Open DPL Architect in Notebooks, write a pattern expression to extract the `orderId` and timestamps from the raw text, and save it as a permanent log processing rule.

### Chapter 3.3: Parse and Extract Structured JSON Data
**Goal:** Efficiently extract nested attributes from structured JSON log payloads.
* JSON visualization and payload decoding
* Utilizing the Line Data (`LD`) matcher and `VARIANT OBJECT` JSON auto-discovery
* Mapping nested JSON paths using the `FIELDS_ADD` command
* **Exercise:** Parse a complex JSON order event using the `JSON:parsedJson` matcher, map specific nested attributes (like `orderInfo.externalKey`) to log fields, and validate the fully structured log record in Dynatrace.

## Workshop 4 : Practice Dynatrace Query Language (DQL)

:blue_book: Learning value : 
 - Gain confidence with Dynatrace Query Language 
 - Learn DQL through hands-on experience with interactive tutorials.
 - Explore, query, combine and process ALL of your observability data stored in Grail.
 - Davis Analyzer / Davis Predictive AI
 - Familiarize with Notebooks
 - Examine use cases

### [4_1 - Practice Dynatrace Query language (DQL) :link: ](https://github.com/hakansuku/D1APACTraining/blob/main/4_1%20Practice%20Dynatrace%20Query%20Language%20DQL.md)
 > - Basic commands and tutorials.
 > - fetch, filter, fieldsAdd & fieldsRemove , parse (DPL), sort , makeTimeseries and summarize commands.

### [4_2 - Davis® forecast analysis :link: ](https://github.com/hakansuku/D1APACTraining/blob/main/4_2%20Davis%C2%AE%20forecast%20analysis.md)
 > - Visualize future trend with help of Davis predictive AI.
 > - Timeseries, understand intervals and granularity
 > - Predictive AI use case and its benefits

### [4_3 - Joining DQL queries via lookup command :link: ](https://github.com/hakansuku/D1APACTraining/blob/main/4_3%20Joining%20DQL%20queries%20via%20lookup%20command.md)
 > - Joining DQL queries for analysis
 > - Use case comparing disk % usage week-over-week 
 > - Thresholds/Indicators to display trends/status

## Workshop 5 : Automation services with Workflows 
:blue_book: Learning value : 
- Gain confidence and understand Dynatrace Workflows
- Familiarize with Workflows app
- Examine usecases
- Learn by building a workflow define triggers and apply programming language to define filters and logic
- Explore query data, transform, filter results and further ingest into Dynatrace for analysis, notification and alerting


### [5_1 Basic Workflows :link: ](https://github.com/hakansuku/D1APACTraining/blob/main/5_1%20Basic%20Dynatrace%20Workflows.md)
 > - Basic Settings / Task Types / Trigger types
 > - Create a workflow that is triggered on demand

### [5_2 Advanced Workflows :link: ](https://github.com/hakansuku/D1APACTraining/blob/main/5_2%20Advanced%20Dynatrace%20Workflows.md)
 > - JavaScript / Dynatrace SDK
 > - Loops and characteristics

## Workshop 6 : Site Reliability Engineering with Dynatrace
:blue_book: Learning value : 

- Understand how Dynatrace Software Intelligence Platform empowers SRE
- Build your own Continuous Deployment pipeline
- Examine and learn how Dynatrace helps automate, optimize CI/CD operations and reduce cost 
- Experience coding Synchronous and Asynchronous communication between CI/CD tool.
- Be able to articulate competitive value and unique proposition of Dynatrace for SRE and demonstrate live.

### [6_1 Environment preparation :link: ](https://github.com/hakansuku/D1APACTraining/blob/main/6_1%20Environment%20preparation.md)
> - Prepare Ubuntu and update libraries
>   Install JDK 17
> - Install Jenkins 
> - Activate Jenkins admin password / install Plugins

### [6_2 Continuous Delivery (CD) pipeline :link: ](https://github.com/hakansuku/D1APACTraining/blob/main/6_2%20Continuous%20Delivery%20(CD)%20pipeline.md)
> - Create a new pipeline
> - Build triggers
> - Define stages in the pipeline
> - Test the pipeline

### [6_3 Asynchronous - Sending Continuous Delivery signals to Dynatrace :link: ](https://github.com/hakansuku/D1APACTraining/blob/main/6_3%20Sending%20Continuous%20Delivery%20signals%20to%20Dynatrace.md)
> - You will create a custom JSON data structure with the pipeline stage information.
> - You will create a Dynatrace token to ingest / write data through Dynatrace API via the /bizevents/ingest endpoint
> - You will be adding API call script task within the pipeline for each of 3 stages: Build -> Deploy -> Test.
> - You will be using notebooks app to write DQL query to Grail and validate the events information of the pipeline executions.

### [6_4 Synchronous monitoring of Continuous Deployment Pipeline :link: ](https://github.com/hakansuku/D1APACTraining/blob/main/6_4%20Synchronous%20CD%20monitoring%20of%20Continuous%20Deployment%20Pipelines.md)
> - You will create a token in Jenkins.
> - You will create a workflow and trigger a run every 60 minutes.
> - You will create a Javascript code to PULL data using Jenkins API endpoint to retrieve pipeline execution informaiton (pipeline run status, ID , Duration for each stage (Build/Deploy/Test) etc. Then will PUSH (ingest) the information as bizevents into Dynatrace.
> - You will validate the information using Notebooks app and DQL to observe the Bizevents ingested.
> - You will create a dashboard to visualize the events ingested near real-time

## Chapter 7: Local OpenShift Development & Cluster Management

**Overall Value:** Developing and testing containerized applications requires a robust, isolated environment that mirrors production without the overhead of cloud infrastructure. This chapter provides the foundation for working with Red Hat OpenShift, a leading enterprise Kubernetes platform. You will learn how to provision a fully functional, localized OpenShift cluster directly on your machine and navigate its web-based management console. By the end of this module, you will have the administrative skills to deploy a local cluster, manage authentication, and isolate resources using OpenShift Projects—setting the stage for secure, hands-on application deployment.

### Chapter 7.1: Install Red Hat OpenShift Local
**Goal:** Create a minimal OpenShift cluster on your local machine for development and testing.
* Hardware prerequisites and Red Hat SSO
* OpenShift Local Installer deployment
* Command-line cluster initialization (`crc setup` and `crc start`)
* **Exercise:** Download the installer, configure your local environment, and successfully spin up a local OpenShift cluster.

### Chapter 7.2: Managing OpenShift Cluster from Web Console
**Goal:** Access and navigate the OpenShift web console to manage your cluster environment.
* Web console authentication via `kubeadmin`
* Understanding OpenShift Projects vs. Kubernetes namespaces
* **Exercise:** Log into the cluster management console and provision a new OpenShift Project.

## Chapter 8: Serverless Architecture & Observability

**Overall Value:** Serverless computing abstracts away the underlying infrastructure, making deployment easier but creating "blind spots" for monitoring and troubleshooting. This chapter bridges that gap. You will learn not only how to build and trigger AWS Lambda functions, but also how to implement robust observability using Dynatrace. By the end of this module, you will be able to deploy serverless code, manage local development tools like the AWS SAM CLI, and gain immediate, deep visibility into your application's performance, traces, and logs.

### Chapter 8.1: Creating a Sample AWS Lambda Function
**Goal:** Build a serverless AWS Lambda function from scratch and expose it via an API endpoint.
* AWS Lambda configuration (Python 3.12 runtime, x86_64 architecture)
* API Gateway trigger setup and security configuration
* **Exercise:** Create a new Lambda function, attach an open API Gateway trigger, and test the live endpoint directly in your browser.

### Chapter 8.2: Instrumenting Serverless - Lambda via Environment Variables
**Goal:** Connect your AWS Lambda function to Dynatrace to monitor performance, traces, and logs.
* Dynatrace Hub setup for AWS Lambda (Python)
* Configuring AWS Lambda environment variables for instrumentation
* Applying AWS Layers using a specified Amazon Resource Name (ARN)
* **Exercise:** Generate connection tokens in Dynatrace, update your Lambda function's configuration, generate test traffic, and observe the resulting traces and logs in the Dynatrace console.

### Chapter 8.3: Prerequisites and AWS SAM CLI Installation
**Goal:** Set up your local development environment with Python and the AWS Serverless Application Model (SAM) CLI.
* AWS console privilege requirements (Private Full Access)
* Python 3.12 installation 
* AWS SAM CLI downloading and configuration
* **Exercise:** Install the required software on your local machine and verify the installation via the command line using `sam --version`.

## Chapter 9: Application Instrumentation with OpenTelemetry

**Overall Value:** In modern cloud environments, relying on proprietary monitoring agents isn't always feasible or desired. This chapter teaches you how to leverage OpenTelemetry (OTel)—the open-source industry standard for observability—to instrument your code directly. You will start by provisioning a cost-effective development environment in AWS, then move hands-on into configuring OTel SDKs for both PHP and Python applications. By the end of this module, you will be able to programmatically capture traces, custom metrics, and logs, and route them securely into Dynatrace for analysis.

### Chapter 9.1: Prepare Coding Environment
**Goal:** Provision a cost-effective Ubuntu development environment on AWS and install a web-based code editor.
* AWS EC2 Spot Instance creation (Ubuntu 24.04, `t2.medium`)
* Configuring EC2 inbound port rules (Ports 8000 & 8080)
* Installing and configuring Visual Studio Code-Server for browser-based development
* **Exercise:** Launch a Spot Instance, connect via SSH, update system packages, install VS Code-Server, and access your cloud IDE via the browser.

### Chapter 9.2: Manually Instrument your PHP Application with OpenTelemetry
**Goal:** Configure a PHP environment with OpenTelemetry and write a script to ingest logs and metrics into Dynatrace.
* PHP and Composer installation
* OpenTelemetry dependencies and VS Code PHP Debug extension setup
* Configuring `otel.php` with Dynatrace API credentials
* **Exercise:** Create a PHP console application that utilizes the OpenTelemetry SDK to generate custom logs and metric counters, then verify their ingestion via the Dynatrace Logs and Notebooks apps.

### Chapter 9.3: Manually Instrument your Python Application with OpenTelemetry
**Goal:** Configure a Python virtual environment with OpenTelemetry and write a script to gather system metrics and logs.
* Python virtual environment (`venv`) and PIP configuration
* Installing the OpenTelemetry SDK and `psutil` library
* Configuring `otel.py` with Dynatrace API credentials
* **Exercise:** Build a Python console application that generates logs and uses callback functions to monitor CPU and RAM usage, then query the ingested data within Dynatrace using DQL.

## Chapter 10: Kubernetes Monitoring with Dynatrace ClassicFullStack

**Overall Value:** Containerized orchestrators like Kubernetes introduce complex layers of abstraction that can obscure infrastructure health and application performance. This chapter guides you through establishing full-stack visibility within a Kubernetes cluster. You will deploy a local single-node cluster using MicroK8s, install the Dynatrace Operator using the ClassicFullStack deployment model, and launch a multi-service microservice application (EasyTrade). By the end of this module, you will understand how containerized workloads interact with host resources and how to seamlessly monitor Kubernetes nodes, namespaces, pods, and services within Dynatrace.

### Chapter 10.1: Environment Preparation
**Goal:** Provision a dedicated Kubernetes environment using MicroK8s on an enterprise-grade cloud instance.
* AWS EC2 Spot Instance configuration (`m5.xlarge` with 4 vCPU, 16 GB RAM) (use ubuntu 22.x)
* MicroK8s installation via Snap package manager (`--classic`)
* Configuring shell quality-of-life enhancements via `kubectl` alias mapping (`k`)
* **Exercise:** Spin up the Ubuntu host, install MicroK8s, verify cluster status, and create a permanent command alias for local cluster management.

### Chapter 10.2: Install Dynatrace Operator - ClassicFullStack Deployment Mode
**Goal:** Deploy the Dynatrace Operator onto your cluster to automatically monitor nodes and cluster infrastructure.
* Dynatrace API token generation tailored for Kubernetes workloads
* Dedicated Kubernetes namespace creation and secure token secret handling
* Deploying the Dynatrace Operator manifests and tailoring a `DynaKube` Custom Resource (CR) file
* **Exercise:** Create the `dynatrace` namespace, apply the operator YAML manifests, substitute your environment tenant details into the `classicFullStack.yaml` template, and confirm cluster recognition in the Dynatrace console.

### Chapter 10.3: Deploy EasyTrade Demo Application
**Goal:** Deploy a multi-tier microservice application, expose its frontend, and validate end-to-end service monitoring.
* Cloning the open-source EasyTrade multi-service repository
* Declaring a targeted application namespace and deploying release manifests
* Exposing containerized workloads through local Kubernetes NodePort services
* **Exercise:** Clone and apply the EasyTrade manifests inside the cluster, configure AWS security group inbound rules to expose the frontend NodePort, generate live traffic in your browser, and track the detected application services in Dynatrace.

## Chapter 11: Deploying Environment ActiveGate in Kubernetes

**Overall Value:** To securely bridge the gap between your Kubernetes cluster and the Dynatrace platform, an ActiveGate is essential for routing traffic and executing API calls. This chapter walks through deploying an Environment ActiveGate directly within a Kubernetes container. You will learn to navigate the Dynatrace API to dynamically generate authentication tokens and connection information, injecting them as Kubernetes secrets for a secure, declarative deployment.

### Chapter 11.1: Deploying ActiveGate in a Kubernetes Container
**Goal:** Securely deploy an Environment ActiveGate within a dedicated Kubernetes namespace using API-generated credentials.
* Dynatrace API operations via `curl` (generating tokens and fetching tenant endpoints)
* Kubernetes namespace and Secret creation (`dynatrace-tokens`)
* YAML manifest deployment for ActiveGate containerization
* **Exercise:** Generate ActiveGate and tenant tokens via the Dynatrace API, create a `dynatrace` namespace and secret, deploy the ActiveGate via a custom YAML file, and validate its running status in both the CLI and the Dynatrace UI.

---

## Chapter 12: OpenTelemetry (OTel) Collector & Python Instrumentation

**Overall Value:** OpenTelemetry provides a vendor-agnostic framework for observability, but managing that data requires a robust collector. This chapter covers end-to-end OTel implementation. You will start by instrumenting a custom Python Flask application with zero-code OTel libraries, pushing data to the console. Then, you will deploy a Dynatrace OpenTelemetry Collector via Docker, reroute your application's telemetry to the collector, and validate the flow of traces, metrics, and logs in Dynatrace.

### Chapter 12.1: Building and Instrumenting a Python Application with OpenTelemetry
**Goal:** Create a Python Flask web application and implement zero-code OpenTelemetry instrumentation.
* Python virtual environments (`venv`) and Flask HTTP server creation
* OpenTelemetry zero-code instrumentation (`opentelemetry-distro`)
* Exporting telemetry data to the local terminal console
* **Exercise:** Deploy a Dice Roll Python application, configure OTel to track metrics (roll counter) and distributed traces, and test the app to view the telemetry output locally in your SSH console.

### Chapter 12.2: Deploying the Dynatrace OTel Collector and Ingesting Data
**Goal:** Route OpenTelemetry data from your application to Dynatrace using a dedicated OTel Collector.
* Docker-based Dynatrace OTel Collector deployment
* Collector YAML configuration (receivers, processors, exporters)
* OTLP data routing and Dynatrace OpenPipelines
* **Exercise:** Launch the Dynatrace OTel Collector in Docker, update the Flask application to use OTLP exporters instead of the console, generate web traffic, and analyze the resulting distributed traces, logs, and metrics within custom Dynatrace dashboards.

## Chapter 13: IBM MQ Monitoring and Troubleshooting

**Overall Value:** Message queues are critical middleware for enterprise applications, making their performance and health essential to monitor. This chapter provides hands-on experience with IBM MQ and the Dynatrace IBM MQ Extension. You will deploy a containerized IBM MQ environment, configure server-connection channels, and integrate it with Dynatrace via an ActiveGate. Finally, you will learn real-world troubleshooting skills by identifying and resolving MQ authentication errors.

### Chapter 13.1: Run an IBM MQ Sample Environment on AWS EC2
**Goal:** Provision a functional IBM MQ message broker environment using Docker.
* Docker volume persistence and IBM MQ container initialization
* MQSC CLI administration (`runmqsc`)
* Channel configuration (`SVRCONN`) and MQ authorization (`setmqaut`)
* **Exercise:** Pull and run the IBM MQ image, access the container's shell, define a server-connection channel, create a local Linux user, and assign the necessary message queue access permissions.

### Chapter 13.2: Connect Dynatrace IBM MQ Extension
**Goal:** Configure the Dynatrace platform to monitor your IBM MQ server remotely via an ActiveGate.
* Dynatrace Extensions hub configuration
* ActiveGate routing for extension workloads
* Remote queue manager connection parameters
* **Exercise:** Add an IBM MQ configuration in the Dynatrace Extensions app, link it to your ActiveGate, input your AWS EC2 public IP and MQ credentials, and review the initial connection logs.

### Chapter 13.3: Debug and Troubleshoot IBM MQ Connection Issues
**Goal:** Identify, debug, and resolve standard MQ connection and authorization errors.
* Docker container troubleshooting and bash execution
* Reading and interpreting MQ `AMQERR01.LOG` files
* Diagnosing `MQRC_NOT_AUTHORIZED` (2035) errors
* **Exercise:** Analyze a failed connection attempt via Dynatrace logs, trace the error back to the IBM MQ server error logs within the container, apply the required configuration fix, and validate successful metric ingestion in a pre-built Dynatrace MQ dashboard.







