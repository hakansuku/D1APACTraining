| # D1APACTraining |
| --- |
 ## This repository is for training internal Dynatrace One Product Specialists on empowering individual technical knowledge via hand-on workshops 

Learning workshops 

## Workshop 1 : Managed Cluster environment

:blue_book: Learning value : 
 - Gain confidence in Linux commands 
 - Gain proficiency using cloud environment. 
 - Improve knowledge supporting on-premise customers 

  ### [1_1 - Obtaining licenses :link: ](https://github.com/hakansuku/D1APACTraining/blob/main/1_1%20Obtain%20Dynatrace%20License.md)
  
  > creating Mission control account
  > adding license / quota

  ### [1_2 - Cloud environment preparation (AWS) :link:](https://github.com/hakansuku/D1APACTraining/blob/main/1_2%20Cloud%20environment%20preparation.md)
  
  > - Regions / availability zones
  > - EC2 / Spot instance request / costing
  > - Security groups / ports 
  > - Trust keys (RSA / PEM)
  > - VM types / AMI images
  > - Terminal communication access

  ### [1_3 - Preparing environment (Linux) :link:](https://github.com/hakansuku/D1APACTraining/blob/main/1_3%20Learning%20the%20linux%20envrionment%20and%20preparation.md)
  > - Permissions
  > - environment setup
  >   - linux basic commands 
  >   - monitoring processes/memory/cpu 
  >   - partitions / volume storage / file systems
  >   - mounting devices
  >   - editing configuration files

  ### [1_4 - Cluster Installation & maintenance :link: ](https://github.com/hakansuku/D1APACTraining/blob/main/1_4%20Cluster_Installation_maintenance.md)
  > - product architecture / folder structures
  > - communication 
  > - Cluster upgrade / published versions
  > - CMC configuration / nodes / AG / Cluster stats and events
  > - Common maintenance issues

## Workshop 2 : Mobile application monitoring

:blue_book: Learning value : 
 - Gain confidence with mobile development environment
 - Experience native mobile development from design to coding , testing and monitoring.
 - Expand knowledge and benefits Dynatrace bring to mobile application monitoring
 - Query , segment and aggregate session data using custom action properties for visual analysis
 - Improve knowledge supporting mobile monitoring customers

  ### [2_1 - Mobile Development Environment preparation :link: ](https://github.com/hakansuku/D1APACTraining/blob/main/2_1%20Mobile%20Development%20Environment%20preparatio.md)
  > - Android Studio / configuration / SDK libraries / projects
  > - Native android app / Kotlin language / builds and structures
  > - Gradle build tool / Repositories /dependencies / plugins
  > - Device manager/ Virtual devices / Android OS

  ### [2_2 - Build your native Android application :link: ](https://github.com/hakansuku/D1APACTraining/blob/main/2_2%20Build%20your%20native%20Android%20application.md)
  > - Native android app / Kotlin language / builds and folder structures
  > - manifest / layout editor / components
  > - Configurations / Code / Design / Build / Run / Debug / Test / logs
  > - Pairing to physical device 

  ### [2_3 - Monitoring with Dynatrace :link: ](https://github.com/hakansuku/D1APACTraining/blob/main/2_3%20Monitoring%20with%20Dynatrace.md)
  > - Instrument dynatrace mobile OneAgent / configuration
  > - Data privacy / tagging / custom actions
  > - sessions / key user actions / APDEX thresholds
  > - custom USQL queries queries / segmentation and aggregation of session data
  > - custom action properties / custom metrics / dashboards
 
## Workshop 3 : Unleash the full power of logs using Dynatrace Pattern Language (DPL)

:blue_book: Learning value : 
 - Gain confidence with Dynatrace Pattern Language 
 - Experience ingesting reshaping Log data processing.
 - Expand knowledge and benefits Dynatrace bring helping organizations more quickly detect anomalies and respond to them.
 - Ingest / match / reshape / filter/ parse log data using DPL to unlock information.
 - Improve knowledge supporting customers enhance data visibility, insights and security

### [3_1 - Log management environment preparation :link: ](https://github.com/hakansuku/D1APACTraining/blob/main/3_1%20Log%20management%20environment%20preparation.md)
  > - ( :exclamation: **pre-requisite**) SaaS Dynatrace (3rd gen) tenant with Grail enabled environment access.  
  >    Pls ask me for an account if you don't have one.
  > - Dynatrace API Swagger UI / Environment API v2 / Logs / Access Token and scope
  > - Ingest sample log record data / validate

### [3_2 - Combine DQL query with DPL to parse unstructured text log data :link: ](https://github.com/hakansuku/D1APACTraining/blob/main/3_2%20Combine%20DQL%20query%20with%20DPL%20to%20parse%20unstructured%20text%20log%20data.md)
  > - DQL query fetch and parse commands and parameters
  > - DPL log-processing-grammar / DPL architect / schema / visual feedback / pattern quality / preset patterns
  > - Extract fields with data type and format / conversion pattern

### [3_3 - Parse and extract elegantly using structured JSON data :link: ](https://github.com/hakansuku/D1APACTraining/blob/main/3_3%20Parse%20and%20extract%20elegantly%20using%20structured%20JSON%20data%20.md)
  > - Analyze visually JSON structures
  > - Extract elegantly fields with data type and format
  > - Optimize logs using log processing commands

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
- Learn by building a workflow define triggers and apply programming language to define conditions and query
- Explore query data, transform, filter results and further ingest into Dynatrace for analysis, notification and alerting


### [5_1 Basic Workflows :link: ](https://github.com/hakansuku/D1APACTraining/blob/main/5_1%20Basic%20Dynatrace%20Workflows.md)
 > - Basic Settings / Task Types / Trigger types
 > - Create a workflow that is triggered on demand

### [5_2 Advanced Workflows :link: ](https://github.com/hakansuku/D1APACTraining/blob/main/5_2%20Advanced%20Dynatrace%20Workflows.md)
 > - JavaScript / Dynatrace SDK
 > - Loops and characteristics

## Workshop 6 : Site Reliability Engineering with Dynatrace
:blue_book: Learning value : 

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
> - You will validate the information using Notebooks app and DQL to observe the bizevents ingested.
> - You will create a dashboard to visualize the events ingested






