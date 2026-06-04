| # D1APACTraining |
| --- |
 ## This repository is for training internal Dynatrace One Platform Specialist Engineers on empowering individual technical knowledge via hands-on workshops 

# D1 APAC Training Workshop

Welcome to the D1 APAC Training repository! This workshop is designed to provide hands-on experience with modern cloud infrastructure, serverless application observability, application instrumentation using OpenTelemetry, and container orchestration monitoring using Dynatrace.  NOTE : This content is for informational purposes only and is not official. We assume no responsibility or liability for any errors, omissions, or outcomes.

## 📚 Workshop Chapters

Below is an overview of the modules covered in this training. Each chapter directory contains its own set of detailed instructions, code snippets, and hands-on exercises.

---

## Chapter 1: Dynatrace Managed Cluster Deployment & Administration

**Overall Value:** Deploying a self-managed observability platform requires foundational knowledge in cloud infrastructure, Linux system administration, and software provisioning. This chapter walks you through the complete lifecycle of deploying a Dynatrace Managed Cluster. 

### [Chapter 1.1: Obtain Dynatrace License](./1_1%20Obtain%20Dynatrace%20License.md)
**Goal:** Generate a Dynatrace Managed Cluster license with unlimited quota for development and testing.

**Concepts Covered:**
* Development Mission Control account creation
* Assigning unlimited Host Units (HU) and Digital Experience Monitoring (DEM) units

**Exercise:** Create a new internal account, generate a "Never Expires" license with unlimited quotas, and retrieve your installation token via email.

**Outcome:** You will possess a valid, unlimited internal Dynatrace license key and token required for a managed cluster installation.

### [Chapter 1.2: Cloud Environment Preparation](./1_2%20Cloud%20environment%20preparation.md)
**Goal:** Provision a dedicated AWS EC2 instance tailored for a Dynatrace Managed deployment.

**Concepts Covered:**
* AWS Spot Instance requests (Ubuntu 22.04 LTS, `t3.2xlarge`)
* SSH Key Pair generation and 300 GiB root storage allocation
* Configuring AWS Security Group inbound rules (Ports 22, 80, 443)

**Exercise:** Launch an optimized Ubuntu spot instance, secure it with a new key pair, expand the root volume to meet installation requirements, and open the necessary network ports.

**Outcome:** A secured, properly resourced AWS Ubuntu instance running in the cloud, accessible via SSH and ready for enterprise software installation.

### [Chapter 1.3: Linux Environment Fundamentals](./1_3%20Learning%20the%20linux%20envrionment%20and%20preparation.md)
**Goal:** Establish an SSH connection to your instance and perform essential Linux system administration tasks.

**Concepts Covered:**
* SSH client configuration (MobaXterm) and root access (`sudo su`)
* OS package management (`apt update`, `apt upgrade`)
* Monitoring system resources (`df -h`, `htop`)
* *(Optional)* Additional AWS EBS volume mounting (`lsblk`, `mkfs`, `mount`)

**Exercise:** Connect to your AWS instance via SSH, update the core Ubuntu packages, verify available CPU/RAM resources using `htop`, and check the available disk space to ensure readiness for Dynatrace.

**Outcome:** Competency in basic Linux command-line navigation, system updates, and resource validation.

### [Chapter 1.4: Dynatrace Managed Cluster Installation & Maintenance](./1_4%20Cluster_Installation_maintenance.md)
**Goal:** Install the Dynatrace Managed software and perform initial cluster configuration.

**Concepts Covered:**
* Downloading the Dynatrace installer via `wget` using your license token
* Executing the installation script (`dynatrace-managed.sh`)
* Verifying cluster status (`server.sh status`)
* Cluster Management Console (CMC) setup (storage retention, Log Monitoring, overload prevention)

**Exercise:** Run the automated Dynatrace installer, verify the server processes, log into the web interface using your public IP, and configure initial data retention and capability settings in the CMC.

**Outcome:** A fully functional, self-hosted Dynatrace Managed Cluster ready to monitor your applications and infrastructure.

---

## Chapter 2: Mobile Application Development & Dynatrace Monitoring

**Overall Value:** Native mobile application development requires a properly configured IDE and emulator environment. This chapter covers the end-to-end process of building a native Android application from scratch and integrating it with Dynatrace for deep user session monitoring.

### [Chapter 2.1: Mobile Development Environment Preparation](./2_1%20Mobile%20Development%20Environment%20preparatio.md)
**Goal:** Configure Android Studio and set up an Android Virtual Device (AVD) for local testing.

**Concepts Covered:**
* Android Studio installation and project initialization (Empty Views Activity)
* Android Gradle Plugin (AGP) and SDK configuration (Android 14 / API 34)
* Provisioning an Android Virtual Device (Pixel 8 with Tiramisu)

**Exercise:** Install the IDE, configure the required Kotlin/Gradle plugins, and successfully boot up a virtual Pixel 8 device in your environment.

**Outcome:** A fully configured mobile development environment capable of compiling code and running a virtual Android device.

### [Chapter 2.2: Build Your Native Android Application (CookieClicker)](./2_2%20Build%20your%20native%20Android%20application.md)
**Goal:** Develop a functional, interactive Android application using Kotlin and XML layouts.

**Concepts Covered:**
* Android manifest configuration for network permissions
* XML Layout Editor design (TextView and Buttons)
* Kotlin `MainActivity` logic (button listeners, click counters) 

**Exercise:** Design the CookieClicker UI, wire up the Kotlin logic to increment the counter on click, and test the live application using the Logcat debugger in your emulator.

**Outcome:** A working native Android application with interactive UI elements and functioning backend logic.

### [Chapter 2.3: Monitoring with Dynatrace](./2_3%20Monitoring%20with%20Dynatrace.md)
**Goal:** Instrument your native Android app with Dynatrace to monitor user sessions, interactions, and custom metrics.

**Concepts Covered:**
* Dynatrace Android Gradle plugin configuration and privacy settings
* Implementing User Tags and Custom Actions via the Dynatrace API
* User Session Query Language (USQL) and Data Explorer visualizations

**Exercise:** Instrument the app using the Dynatrace wizard, capture custom "send score" actions, and build a Dynatrace dashboard tracking total cookie clicks using USQL and custom metric queries.

**Outcome:** The ability to trace mobile user sessions, capture custom application events, and visualize user behavior data in Dynatrace.

---

## Chapter 3: Log Management & Dynatrace Pattern Language (DPL)

**Overall Value:** Processing and parsing log data is essential for extracting actionable business and operational intelligence. This chapter explores Dynatrace's log management capabilities, focusing on the Dynatrace Pattern Language (DPL) and the Dynatrace Query Language (DQL).

### [Chapter 3.1: Log Management Environment Preparation](./3_1%20Log%20management%20environment%20preparation.md)
**Goal:** Authenticate and interact with the Dynatrace Environment API to manually ingest log records.

**Concepts Covered:**
* Dynatrace API access token generation with log ingest scopes
* Swagger UI configuration for REST API interaction
* Sending HTTP POST requests to the `/logs/ingest` endpoint

**Exercise:** Generate an ingest token, authenticate via Swagger UI, push a sample order-fallout log payload to the API, and validate its arrival in the Dynatrace Logs & Events app.

**Outcome:** The technical capability to programmatically push custom log data into Dynatrace using REST APIs.

### [Chapter 3.2: Parse Unstructured Text Log Data using DPL](./3_2%20Combine%20DQL%20query%20with%20DPL%20to%20parse%20unstructured%20text%20log%20data.md)
**Goal:** Use DPL Architect to extract specific data fields from raw, unstructured log text.

**Concepts Covered:**
* Understanding DPL matchers (`DATA`) and pointer traversal
* Extracting variables and defining data types (`JSONTIMESTAMP`, `INT`)
* Creating and testing Dynatrace log processing rules

**Exercise:** Open DPL Architect in Notebooks, write a pattern expression to extract the `orderId` and timestamps from the raw text, and save it as a permanent log processing rule.

**Outcome:** The ability to transform messy, unstructured log strings into clean, queryable key-value attributes.

### [Chapter 3.3: Parse and Extract Structured JSON Data](./3_3%20Parse%20and%20extract%20elegantly%20using%20structured%20JSON%20data%20.md)
**Goal:** Efficiently extract nested attributes from structured JSON log payloads.

**Concepts Covered:**
* JSON visualization and payload decoding
* Utilizing the Line Data (`LD`) matcher and `VARIANT OBJECT` JSON auto-discovery
* Mapping nested JSON paths using the `FIELDS_ADD` command

**Exercise:** Parse a complex JSON order event using the `JSON:parsedJson` matcher, map specific nested attributes (like `orderInfo.externalKey`) to log fields, and validate the fully structured log record in Dynatrace.

**Outcome:** Mastery over parsing complex JSON payloads and mapping them to standardized log metrics.

---

## Chapter 4: Dynatrace Query Language (DQL) & Davis AI

**Overall Value:** Navigating and analyzing vast amounts of observability data requires a powerful query language. This chapter introduces you to the Dynatrace Query Language (DQL) and Davis Predictive AI.

### [Chapter 4.1: Practice Dynatrace Query Language](./4_1%20Practice%20Dynatrace%20Query%20Language%20DQL.md)
**Goal:** Familiarize yourself with basic DQL commands using interactive tutorials.

**Concepts Covered:**
* Dynatrace interactive Dojo application
* Fundamental DQL query structuring (`fetch`, `filter`, `fieldsAdd`, `parse`, `summarize`)

**Exercise:** Install the Dojo app within Dynatrace and complete the 8-step Beginner's tutorial.

**Outcome:** A foundational understanding of DQL syntax and the ability to retrieve and filter data in Grail.

### [Chapter 4.2: Davis® Forecast Analysis](./4_2%20Davis®%20forecast%20analysis.md)
**Goal:** Use Davis Predictive AI to project future infrastructure capacity based on historical timeseries data.

**Concepts Covered:**
* Timeseries data queries and aggregation (`avg`, `dt.host.memory.usage`)
* Chaining commands via pipeline operators (`|`)
* Activating the Davis Analyzer for trend projection

**Exercise:** Query the 30-day average memory usage of a specific VMware host group, visualize it as a line chart, and enable Davis AI to forecast future memory demands.

**Outcome:** The ability to leverage AI-driven forecasting to predict infrastructure bottlenecks before they occur.

### [Chapter 4.3: Joining DQL Queries via the Lookup Command](./4_3%20Joining%20DQL%20queries%20via%20lookup%20command.md)
**Goal:** Join data from multiple independent queries to perform comparative analysis.
**Concepts Covered:**
* DQL `lookup` command syntax and execution
* Mapping `sourceField` to `lookupField` to join tables
* Advanced array math and conditional UI indicators (e.g., 🔴 🟠 🟢)

**Exercise:** Write a complex query using `lookup` to compare week-over-week disk usage across hosts, calculating the difference and automatically assigning visual status indicators based on threshold logic.

**Outcome:** Advanced querying skills allowing you to merge disparate datasets and build highly customized analytical dashboards.

---

## Chapter 5: Automation with Dynatrace Workflows

**Overall Value:** Modern operations require automation to bridge the gap between monitoring and action. This chapter explores Dynatrace Workflows, teaching you how to build automated sequences using APIs and custom code.

### [Chapter 5.1: Basic Dynatrace Workflows](./5_1%20Basic%20Dynatrace%20Workflows.md)
**Goal:** Create a workflow that pulls external data via an HTTP GET request and ingests a filtered subset into Dynatrace.

**Concepts Covered:**
* Workflow triggers (On-demand, Scheduled, Event-based)
* HTTP request tasks (GET/POST) and outbound connection preferences
* Jinja templating for dynamic payload generation

**Exercise:** Build a workflow that calls a public currency exchange API, uses a Jinja template to isolate four specific currencies (AUD, KRW, USD, JPY), and POSTs the formatted JSON as a log event into Dynatrace.

**Outcome:** A working automated workflow capable of communicating with external APIs and ingesting formatted data.

### [Chapter 5.2: Advanced Dynatrace Workflows Using JavaScript](./5_2%20Advanced%20Dynatrace%20Workflows.md)
**Goal:** Replace basic HTTP tasks with custom JavaScript code for more complex data fetching and transformation.

**Concepts Covered:**
* The `Run Javascript` workflow action
* Writing asynchronous `fetch` requests inside the Dynatrace JS runtime
* Adapting downstream tasks to handle altered JSON structures

**Exercise:** Duplicate your basic workflow, replace the initial HTTP GET task with a custom JavaScript function, adjust the Jinja payload to match the new nested JSON structure, and validate the successfully ingested logs.

**Outcome:** The ability to write serverless JavaScript functions directly within Dynatrace to handle complex logic and API interactions.

---

## Chapter 6: CI/CD Pipeline Observability with Jenkins

**Overall Value:** Software delivery pipelines are mission-critical, yet they often lack the same level of observability as production applications. This chapter focuses on integrating Jenkins CI/CD pipelines with Dynatrace.

### [Chapter 6.1: Environment Preparation (Jenkins)](./6_1%20Environment%20preparation.md)
**Goal:** Provision an AWS Ubuntu server and install Jenkins for continuous integration and delivery.

**Concepts Covered:**
* AWS EC2 initialization (`t3a.medium`)
* OpenJDK 17 and Jenkins repository configuration
* Initial Jenkins security setup and plugin installation

**Exercise:** Spin up the EC2 instance, install Java and Jenkins via the command line, unlock the Jenkins web UI using the initial admin password, and create your master administrator account.

**Outcome:** A fully functioning Jenkins automation server ready to run CI/CD workloads.

### [Chapter 6.2: Creating a Simple Continuous Delivery (CD) Pipeline](./6_2%20Continuous%20Delivery%20(CD)%20pipeline.md)
**Goal:** Define and automate a multi-stage software release pipeline.

**Concepts Covered:**
* Jenkins Pipeline job creation
* CRON-based scheduling (`H/15 * * * *`)
* Groovy script syntax for pipeline stages (Build, Deploy, Test)

**Exercise:** Create a scheduled Jenkins Pipeline with three distinct echo stages, manually trigger a build, and examine the console output.

**Outcome:** A functioning, automated CI/CD pipeline capable of running multi-stage deployments on a schedule.

### [Chapter 6.3: Sending CD Pipeline Signals to Dynatrace](./6_3%20Sending%20Continuous%20Delivery%20signals%20to%20Dynatrace.md)
**Goal:** Configure the Jenkins pipeline to actively push stage-execution metrics into Dynatrace as Business Events.

**Concepts Covered:**
* Groovy JSON data manipulation (`JsonOutput`)
* Dynatrace API token generation for the `/bizevents/ingest` endpoint
* Executing `curl` POST requests directly from Jenkins Pipeline steps

**Exercise:** Install the required Pipeline Utility plugins, inject Groovy code to capture build environment variables into a JSON payload, and execute an API call in each pipeline stage to push the event to Grail.

**Outcome:** A "Push" observability model where Jenkins actively reports its build, deploy, and test metrics to Dynatrace in real-time.

### [Chapter 6.4: Synchronous Monitoring Using Dynatrace Workflows](./6_4%20Synchronous%20CD%20monitoring%20of%20Continuous%20Deployment%20Pipelines.md)
**Goal:** Use Dynatrace Workflows to poll the Jenkins API at regular intervals, extracting deep pipeline metadata and pushing it to Grail.

**Concepts Covered:**
* Jenkins API token creation and authentication (Crumb Issuer)
* Advanced Dynatrace JavaScript functions for multi-step API polling (Pull)
* Dynatrace Business Events Client SDK (Push)

**Exercise:** Create a scheduled Dynatrace workflow running custom JavaScript to authenticate with Jenkins, poll all job stages and durations, map them to a BizEvents schema, and visualize the performance of your CI/CD pipelines on a custom dashboard.

**Outcome:** A "Pull" observability model leveraging Dynatrace to actively track external CI/CD health without modifying the pipeline's core code.

---

## Chapter 7: Local OpenShift Development & Cluster Management

**Overall Value:** Developing and testing containerized applications requires a robust, isolated environment. This chapter provides the foundation for working with Red Hat OpenShift, a leading enterprise Kubernetes platform.

### [Chapter 7.1: Install Red Hat OpenShift Local](./7_1%20Installing%20Red%20Hat%20Openshift%20Local.md)
**Goal:** Create a minimal OpenShift cluster on your local machine for development and testing.

**Concepts Covered:**
* Hardware prerequisites and Red Hat SSO
* OpenShift Local Installer deployment
* Command-line cluster initialization (`crc setup` and `crc start`)

**Exercise:** Download the installer, configure your local environment, and successfully spin up a local OpenShift cluster.

**Outcome:** A fully functioning, local OpenShift container platform running on your own hardware.

### [Chapter 7.2: Managing OpenShift Cluster from Web Console](./7_2%20Create%20Namespace%20and%20deploy%20containerized%20application.md)
**Goal:** Access and navigate the OpenShift web console to manage your cluster environment.

**Concepts Covered:**
* Web console authentication via `kubeadmin`
* Understanding OpenShift Projects vs. Kubernetes namespaces

**Exercise:** Log into the cluster management console and provision a new OpenShift Project.

**Outcome:** The administrative ability to navigate OpenShift, manage resources, and isolate workloads using Projects.

---

## Chapter 8: Serverless Architecture & Observability

**Overall Value:** Serverless computing abstracts away the underlying infrastructure, making deployment easier but creating "blind spots" for monitoring. This chapter bridges that gap using AWS Lambda and Dynatrace.

### [Chapter 8.1: Creating a Sample AWS Lambda Function](./8_1%20Create%20sample%20LAMBDA%20function.md)
**Goal:** Build a serverless AWS Lambda function from scratch and expose it via an API endpoint.

**Concepts Covered:**
* AWS Lambda configuration (Python 3.12 runtime, x86_64 architecture)
* API Gateway trigger setup and security configuration

**Exercise:** Create a new Lambda function, attach an open API Gateway trigger, and test the live endpoint directly in your browser.

**Outcome:** A live, scalable serverless function accessible over the public internet.

### [Chapter 8.2: Instrumenting Serverless - Lambda via Environment Variables](./8_2%20Instrumenting%20Serverless%20LAMBDA%20function.md)
**Goal:** Connect your AWS Lambda function to Dynatrace to monitor performance, traces, and logs.

**Concepts Covered:**
* Dynatrace Hub setup for AWS Lambda (Python)
* Configuring AWS Lambda environment variables for instrumentation
* Applying AWS Layers using a specified Amazon Resource Name (ARN)

**Exercise:** Generate connection tokens in Dynatrace, update your Lambda function's configuration, generate test traffic, and observe the resulting traces and logs in the Dynatrace console.

**Outcome:** Full observability into serverless code execution, eliminating monitoring blind spots in AWS Lambda.

### [Chapter 8.3: Prerequisites and AWS SAM CLI Installation](./8_3_OPTIONAL_LAMBDA_SAM_CLI_tool.md)
**Goal:** Set up your local development environment with Python and the AWS Serverless Application Model (SAM) CLI.

**Concepts Covered:**
* AWS console privilege requirements (Private Full Access)
* Python 3.12 installation 
* AWS SAM CLI downloading and configuration

**Exercise:** Install the required software on your local machine and verify the installation via the command line using `sam --version`.

**Outcome:** A local machine fully equipped to build, test, and deploy serverless infrastructure as code.

---

## Chapter 9: Application Instrumentation with OpenTelemetry

**Overall Value:** In modern cloud environments, leveraging OpenTelemetry (OTel)—the open-source industry standard for observability—allows you to instrument your code directly.

### [Chapter 9.1: Prepare Coding Environment](./9_1%20OPENTELEMETRY%20Coding%20environment%20preparation.md)
**Goal:** Provision a cost-effective Ubuntu development environment on AWS and install a web-based code editor.

**Concepts Covered:**
* AWS EC2 Spot Instance creation (Ubuntu 24.04, `t2.medium`)
* Configuring EC2 inbound port rules (Ports 8000 & 8080)
* Installing and configuring Visual Studio Code-Server for browser-based development

**Exercise:** Launch a Spot Instance, connect via SSH, update system packages, install VS Code-Server, and access your cloud IDE via the browser.

**Outcome:** A remote, cloud-hosted IDE accessible from anywhere, optimized for software development.

### [Chapter 9.2: Manually Instrument your PHP Application with OpenTelemetry](./9_2%20Manually%20instrument%20your%20PHP%20application%20with%20OpenTelemetry.md)
**Goal:** Configure a PHP environment with OpenTelemetry and write a script to ingest logs and metrics into Dynatrace.
**Concepts Covered:**
* PHP and Composer installation
* OpenTelemetry dependencies and VS Code PHP Debug extension setup
* Configuring `otel.php` with Dynatrace API credentials

**Exercise:** Create a PHP console application that utilizes the OpenTelemetry SDK to generate custom logs and metric counters, then verify their ingestion via the Dynatrace Logs and Notebooks apps.

**Outcome:** A functioning PHP application that programmatically generates and exports its own telemetry data using open-source standards.

### [Chapter 9.3: Manually Instrument your Python Application with OpenTelemetry](./9_3%20Manually%20instrument%20your%20Python%20application%20with%20OpenTelemetry.md)
**Goal:** Configure a Python virtual environment with OpenTelemetry and write a script to gather system metrics and logs.

**Concepts Covered:**
* Python virtual environment (`venv`) and PIP configuration
* Installing the OpenTelemetry SDK and `psutil` library
* Configuring `otel.py` with Dynatrace API credentials

**Exercise:** Build a Python console application that generates logs and uses callback functions to monitor CPU and RAM usage, then query the ingested data within Dynatrace using DQL.

**Outcome:** A functioning Python application that monitors its own host resource usage and exports it via OpenTelemetry.

---

## Chapter 10: Kubernetes Monitoring with Dynatrace ClassicFullStack

**Overall Value:** Containerized orchestrators like Kubernetes introduce complex layers of abstraction. This chapter guides you through establishing full-stack visibility within a cluster.

### [Chapter 10.1: Environment Preparation](./10_1%20Environment%20Preparation.md)
**Goal:** Provision a dedicated Kubernetes environment using MicroK8s on an enterprise-grade cloud instance.

**Concepts Covered:**
* AWS EC2 Spot Instance configuration (`m5.xlarge` with 4 vCPU, 16 GB RAM) NOTE use Ubuntu 22.x
* MicroK8s installation via Snap package manager (`--classic`)
* Configuring shell quality-of-life enhancements via `kubectl` alias mapping (`k`)

**Exercise:** Spin up the Ubuntu host, install MicroK8s, verify cluster status, and create a permanent command alias for local cluster management.

**Outcome:** A single-node, production-grade Kubernetes cluster ready for container orchestration.

### [Chapter 10.2: Install Dynatrace Operator - ClassicFullStack Deployment Mode](./10_2%20Install%20Dynatrace%20Operator%20-%20ClassicFullStack%20Deployment%20Mode.md)
**Goal:** Deploy the Dynatrace Operator onto your cluster to automatically monitor nodes and cluster infrastructure.

**Concepts Covered:**
* Dynatrace API token generation tailored for Kubernetes workloads
* Dedicated Kubernetes namespace creation and secure token secret handling
* Deploying the Dynatrace Operator manifests and tailoring a `DynaKube` Custom Resource (CR) file

**Exercise:** Create the `dynatrace` namespace, apply the operator YAML manifests, substitute your environment tenant details into the `classicFullStack.yaml` template, and confirm cluster recognition in the Dynatrace console.

**Outcome:** Automated, full-stack monitoring of a Kubernetes cluster, covering the host node, namespaces, and underlying infrastructure.

### [Chapter 10.3: Deploy EasyTrade Demo Application](./10_3%20Deploy%20EasyTrade%20Demo%20Application.md)
**Goal:** Deploy a multi-tier microservice application, expose its frontend, and validate end-to-end service monitoring.

**Concepts Covered:**
* Cloning the open-source EasyTrade multi-service repository
* Declaring a targeted application namespace and deploying release manifests
* Exposing containerized workloads through local Kubernetes NodePort services

**Exercise:** Clone and apply the EasyTrade manifests inside the cluster, configure AWS security group inbound rules to expose the frontend NodePort, generate live traffic in your browser, and track the detected application services in Dynatrace.

**Outcome:** A live, containerized microservice application running in Kubernetes, fully mapped and monitored by Dynatrace.

---

## Chapter 11: Deploying Environment ActiveGate in Kubernetes

**Overall Value:** To securely bridge the gap between your Kubernetes cluster and the Dynatrace platform, an ActiveGate is essential for routing traffic and executing API calls. 

### [Chapter 11.1: Deploying ActiveGate in a Kubernetes Container](./11_1%20Deploying%20ActiveGate%20in%20a%20Kubernetes%20Container.md)
**Goal:** Securely deploy an Environment ActiveGate within a dedicated Kubernetes namespace using API-generated credentials.

**Concepts Covered:**
* Dynatrace API operations via `curl` (generating tokens and fetching tenant endpoints)
* Kubernetes namespace and Secret creation (`dynatrace-tokens`)
* YAML manifest deployment for ActiveGate containerization

**Exercise:** Generate ActiveGate and tenant tokens via the Dynatrace API, create a `dynatrace` namespace and secret, deploy the ActiveGate via a custom YAML file, and validate its running status in both the CLI and the Dynatrace UI.

**Outcome:** A secure, containerized proxy gateway that safely routes internal cluster telemetry out to the Dynatrace SaaS tenant.

---

## Chapter 12: OpenTelemetry (OTel) Collector & Python Instrumentation

**Overall Value:** OpenTelemetry provides a vendor-agnostic framework for observability, but managing that data requires a robust collector. This chapter covers end-to-end OTel implementation.

### [Chapter 12.1: Building and Instrumenting a Python Application with OpenTelemetry](./12_1%20Building%20and%20Instrumenting%20a%20Python%20Application%20with%20OpenTelemetry.md)
**Goal:** Create a Python Flask web application and implement zero-code OpenTelemetry instrumentation.

**Concepts Covered:**
* Python virtual environments (`venv`) and Flask HTTP server creation
* OpenTelemetry zero-code instrumentation (`opentelemetry-distro`)
* Exporting telemetry data to the local terminal console

**Exercise:** Deploy a Dice Roll Python application, configure OTel to track metrics (roll counter) and distributed traces, and test the app to view the telemetry output locally in your SSH console.

**Outcome:** A Python web application automatically generating OTel traces and metrics without requiring deep code modifications.

### [Chapter 12.2: Deploying the Dynatrace OTel Collector and Ingesting Data](./12_2%20Deploying%20the%20Dynatrace%20OTel%20Collector%20and%20Ingesting%20Data.md)
**Goal:** Route OpenTelemetry data from your application to Dynatrace using a dedicated OTel Collector.

**Concepts Covered:**
* Docker-based Dynatrace OTel Collector deployment
* Collector YAML configuration (receivers, processors, exporters)
* OTLP data routing and Dynatrace OpenPipelines

**Exercise:** Launch the Dynatrace OTel Collector in Docker, update the Flask application to use OTLP exporters instead of the console, generate web traffic, and analyze the resulting distributed traces, logs, and metrics within custom Dynatrace dashboards.

**Outcome:** A centralized OpenTelemetry architecture where application telemetry is routed through a dedicated collector and securely ingested into Dynatrace.

---

## Chapter 13: IBM MQ Monitoring and Troubleshooting

**Overall Value:** Message queues are critical middleware for enterprise applications. This chapter provides hands-on experience with IBM MQ and the Dynatrace IBM MQ Extension.

### [Chapter 13.1: Run an IBM MQ Sample Environment on AWS EC2](./13_1%20Run%20an%20IBM%20MQ%20Sample%20Environment%20on%20AWS%20EC2.md)
**Goal:** Provision a functional IBM MQ message broker environment using Docker.

**Concepts Covered:**
* Docker volume persistence and IBM MQ container initialization
* MQSC CLI administration (`runmqsc`)
* Channel configuration (`SVRCONN`) and MQ authorization (`setmqaut`)

**Exercise:** Pull and run the IBM MQ image, access the container's shell, define a server-connection channel, create a local Linux user, and assign the necessary message queue access permissions.

**Outcome:** A containerized enterprise message broker ready to send and receive queues.

### [Chapter 13.2: Connect Dynatrace IBM MQ Extension](./13_2%20Connect%20Dynatrace%20IBM%20MQ%20Extension.md)
**Goal:** Configure the Dynatrace platform to monitor your IBM MQ server remotely via an ActiveGate.

**Concepts Covered:**
* Dynatrace Extensions hub configuration
* ActiveGate routing for extension workloads
* Remote queue manager connection parameters

**Exercise:** Add an IBM MQ configuration in the Dynatrace Extensions app, link it to your ActiveGate, input your AWS EC2 public IP and MQ credentials, and review the initial connection logs.

**Outcome:** Dynatrace successfully reaching out and polling the IBM MQ server for health and performance metrics.

### [Chapter 13.3: Debug and Troubleshoot IBM MQ Connection Issues](./13_3%20Debug%20and%20Troubleshoot%20IBM%20MQ%20Connection%20Issues.md)
**Goal:** Identify, debug, and resolve standard MQ connection and authorization errors.

**Concepts Covered:**
* Docker container troubleshooting and bash execution
* Reading and interpreting MQ `AMQERR01.LOG` files
* Diagnosing `MQRC_NOT_AUTHORIZED` (2035) errors

**Exercise:** Analyze a failed connection attempt via Dynatrace logs, trace the error back to the IBM MQ server error logs within the container, apply the required configuration fix, and validate successful metric ingestion in a pre-built Dynatrace MQ dashboard.
**Outcome:** Real-world troubleshooting experience resolving middleware authentication failures and restoring observability.

---

## 🚀 Getting Started

To get the most out of this workshop, ensure you have the following prerequisites ready:
* An active AWS Account with permissions to launch Spot instances.
* A Dynatrace environment (SaaS tenant) with administrative access to generate API tokens.
* A Red Hat SSO account for downloading OpenShift Local assets.






