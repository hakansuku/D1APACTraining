# 12_2_1 Deploying Dynatrace collector and configuring for LOGS , METRICS and TRACES ingestion from the previous Roll Dice application

## In this tutorial we will deploy Dynatrace Opentelemetry collector and configure to collect Dice Roll application (metrics,logs,traces) opentelemetry.  We will then validate the ingested data in Dynatrace Dashboard.

- Open a new SSH terminal to the ubuntu host 
> (for simplicity we will deploy Dynatrace OTEL collector in the same ubuntu host we used for the Dice Roll application)
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/OTELcollector/dockerpull.jpg?raw=true)

- Install docker and pull the Dynatrace opentelemetry collector 
> Latest documentation available in https://docs.dynatrace.com/docs/ingest-from/opentelemetry/collector
> You can download the Dynatrace OTel Collector release from GitHub. It is also available as a container image at GitHub Packages and can be pulled using the following Docker command:
```
apt install docker.io -y
docker pull ghcr.io/dynatrace/dynatrace-otel-collector/dynatrace-otel-collector:0.47.0
```
- In your Dynatrace tenant go to Access Tokens and generate an API token with the following 3 scopes 
> Ingest Logs , Ingest Metrics and Ingest Opentelemetry Traces

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/OTELcollector/oteltoken.jpg)

> NOTE!!: Make sure you copy and keep the generated token as it will be needed to configure OTEL collector configuration below.

### 12_2_2 Creating configuration file for Dynatrace OTEL collector
> To successfully configure your OTel Collector instance, you need to configure each component (receiver, optional processor, and exporter) individually in the Collector YAML configuration file and enable them via additional pipeline objects

- Create a file called config.yaml and paste the following configuration
> reference https://docs.dynatrace.com/docs/ingest-from/opentelemetry/collector/configuration

> NOTICE you will need to modify the endpoint with your tenant 
> Modify below to point 1) endpoint: "https://<your tenant>.live.dynatrace.com/api/v2/otlp"
> header token with your generated token 2) Authorization: "Api-Token dt0c01.XXXXXXXXXXXXXXXYLSLBD6.XZ4MV2NFGQEGQWRYTKVCHVXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"

```
receivers:
  otlp:
    protocols:
      grpc:
        endpoint: 0.0.0.0:4317
      http:
        endpoint: 0.0.0.0:4318

processors:
  cumulativetodelta:
    max_staleness: 25h

exporters:
  otlp_http:
    endpoint: "https://XXXXXXXX.dev.dynatracelabs.com/api/v2/otlp"
    headers:
      Authorization: "Api-Token dt0c01.XXXXXXXXXXXXXXXXXXXXX6.XZ4MV2NFGQEGQWRYTKVCHVXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"

service:
  pipelines:
    traces:
      receivers: [otlp]
      processors: []
      exporters: [otlp_http]
    metrics:
      receivers: [otlp]
      processors: [cumulativetodelta]
      exporters: [otlp_http]
    logs:
      receivers: [otlp]
      processors: []
      exporters: [otlp_http]
```

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/OTELcollector/configyaml.jpg)
  
- In the same directory where your created config.yaml file is located, Run Dynatrace Opentelemetry collector in docker using below command. 
> -d parameter run the collector in the backgroud 
```
docker run -d   --name dynatrace-otel-collector   -p 4317:4317   -p 4318:4318   -v $(pwd)/config.yaml:/etc/otelcol/config.yaml   ghcr.io/dynatrace/dynatrace-otel-collector/dynatrace-otel-collector:0.47.0   --config /etc/otelcol/config.yaml
```
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/OTELcollector/runcollector.jpg)

> validate collector has started with below command
```
docker logs dynatrace-otel-collector
```
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/OTELcollector/validatecollectorlog.jpg)

### 12_2_3 Connecting application to Dynatrace Openelemetry Collector

- Next we will stop and Restart Dice Roll application with different parameters

> Go back to the SSH connection with the application running.  Stop the application using CTRL+C

> For restrating the application we will be replacing previous command parameters console with oltp (--traces_exporter otlp --metrics_exporter otlp --logs_exporter otlp) This is how we now pointing to the collector. 

> FYI- we did not have to specify collector port as the default Collector endpoint will be used, which is 0.0.0.0:4317 for gRPC and 0.0.0.0:4318 for HTTP. (https://opentelemetry.io/docs/zero-code/python/configuration/)

> Now restart the application with different parameters like below command
```
opentelemetry-instrument --traces_exporter otlp --metrics_exporter otlp --logs_exporter otlp --service_name dice-server flask run --host=0.0.0.0 -p 8080
```
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/OTELcollector/restartotlp.jpg)

### Generating some traffic 
- start rolling your dice ! to generate some traffic using the browser using your HTTP url
> my URL is http://13.125.75.141:8080/diceroll

## 12_2_4 Validating received opentelemetry in Dashboards app
- Open Dashboard app and create new dashboard with name Diceroll opentelemetry
- 1)Add simple Logs tile  
- 2)Add Traces tile
- 3)Add spans tile
- 4)Add Metric tile (metric name roll_counter)

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/OTELcollector/dashboardotel.jpg)

## 12_2_5 Openpipelines, Services Analysis and Distributed traces
- Open Openpipelines and and view log, trace and metric data flowing through opentelemetry pipelines.  
> Notice that you're able to open in Notebooks to validate data getting ingested

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/OTELcollector/openpipelinetraces.jpg)

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/OTELcollector/openpipelineslogs.jpg)

- Open Services app
> Observe how dynatrace discovers the service and provides full information based on the opentelemetry 
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/OTELcollector/services.jpg)

- Click on View Traces from the Services app
> Observe traces for each request and all relevant trace information at granular level

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/OTELcollector/distributed.jpg)


-End of Document-


