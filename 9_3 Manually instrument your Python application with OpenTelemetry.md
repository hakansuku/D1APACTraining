# 9_3_1 Manually instrument your Python application with OpenTelemetry

## In this tutorial we will instrument Python application with Opentelemetry using the environment created in previous tutorial 9_1

- install pyhton3-venv and pip with below commands:
> use root user
```
apt install python3.12-venv -y
apt install python3-pip -y
python3 -m venv /home/ubuntu/dynatrace-app
```
> phython3 -v  (checks installation)

- install opentelemetry SDK  :

```
cd /home/ubuntu/dynatrace-app
/home/ubuntu/dynatrace-app/bin/pip install opentelemetry-api
/home/ubuntu/dynatrace-app/bin/pip install opentelemetry-sdk
/home/ubuntu/dynatrace-app/bin/pip install opentelemetry-exporter-otlp-proto-http
/home/ubuntu/dynatrace-app/bin/pip install psutil
```
- Open VS code from your browser and login
- click on extensions icon and install Python Debug extension

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/PHP/pythonextension.png?raw=true)

- Using VS code create a file otel.py in /home/ubuntu/dynatrace-app/ directory and copy and paste the below code:
  
- make sure you replace under the // ===== GENERAL SETUP ===== section with your environment ID and your own token
	> $DT_API_URL = 'https://_YOUR_ENVIRONMENT_ID_.live.dynatrace.com/api/v2/otlp';
 
 	> $DT_API_TOKEN = 'YOUR_OWN_TOKEN';
 
```
import logging
import random
import time
import json
import logging
import psutil

from opentelemetry.sdk.resources import Resource

# Import exporters
from opentelemetry.exporter.otlp.proto.http.trace_exporter import OTLPSpanExporter
from opentelemetry.exporter.otlp.proto.http.metric_exporter import OTLPMetricExporter
from opentelemetry.exporter.otlp.proto.http._log_exporter import OTLPLogExporter

# Trace imports
from opentelemetry.trace import set_tracer_provider, get_tracer_provider
from opentelemetry.sdk.trace import TracerProvider, sampling
from opentelemetry.sdk.trace.export import BatchSpanProcessor

# Metric imports
from opentelemetry import metrics as metrics
from opentelemetry.sdk.metrics.export import (
    AggregationTemporality,
    PeriodicExportingMetricReader,
)
from opentelemetry.sdk.metrics import MeterProvider, Counter, UpDownCounter, Histogram, ObservableCounter, ObservableUpDownCounter
from opentelemetry.metrics import set_meter_provider, get_meter_provider
from opentelemetry.metrics import Observation, CallbackOptions

# Logs import
from opentelemetry.sdk._logs import LoggerProvider, LoggingHandler
from opentelemetry.sdk._logs.export import BatchLogRecordProcessor
from opentelemetry._logs import set_logger_provider

# ===== GENERAL SETUP =====
# Notice that I removed .apps from DT_API_URL = 
DT_API_URL = "https://<environment ID>.live.dynatrace.com/api/v2/otlp"
DT_API_TOKEN = "<YOUR TOKEN>"

merged = dict()
for name in ["dt_metadata_e617c525669e072eebe3d0f08212e8f2.json", "/var/lib/dynatrace/enrichment/dt_metadata.json", "/var/lib/dynatrace/enrichment/dt_host_metadata.json"]:
  try:
    data = ''
    with open(name) as f:
      data = json.load(f if name.startswith("/var") else open(f.read()))
      merged.update(data)
  except:
    pass

merged.update({
  "service.name": "python-quickstart", #TODO Replace with the name of your application
  "service.version": "1.0.1", #TODO Replace with the version of your application
})
resource = Resource.create(merged)

# ===== TRACING SETUP =====

tracer_provider = TracerProvider(sampler=sampling.ALWAYS_ON, resource=resource)
set_tracer_provider(tracer_provider)

tracer_provider.add_span_processor(
  BatchSpanProcessor(
    OTLPSpanExporter(
      endpoint = DT_API_URL + "/v1/traces",
      headers = {
        "Authorization": "Api-Token " + DT_API_TOKEN
      }
    )
  )
)

# ===== METRIC SETUP =====

exporter = OTLPMetricExporter(
  endpoint = DT_API_URL + "/v1/metrics",
  headers = {"Authorization": "Api-Token " + DT_API_TOKEN},
  preferred_temporality = {
    Counter: AggregationTemporality.DELTA,
    UpDownCounter: AggregationTemporality.CUMULATIVE,
    Histogram: AggregationTemporality.DELTA,
    ObservableCounter: AggregationTemporality.DELTA,
    ObservableUpDownCounter: AggregationTemporality.CUMULATIVE,
  }
)

reader = PeriodicExportingMetricReader(exporter)
provider = MeterProvider(metric_readers=[reader], resource=resource)
set_meter_provider(provider)
meter = get_meter_provider().get_meter("my-meter", "0.1.2")

# ===== LOG SETUP =====

logger_provider = LoggerProvider(resource=resource)
set_logger_provider(logger_provider)  
# I found that root logger loglevel default is WARNING so ignored DEBUG and INFO level logs.  
logging.getLogger().setLevel(logging.INFO)

logger_provider.add_log_record_processor(
  BatchLogRecordProcessor(OTLPLogExporter(
    endpoint = DT_API_URL + "/v1/logs",
  headers = {"Authorization": "Api-Token " + DT_API_TOKEN}
  ))
)
handler = LoggingHandler(level=logging.INFO, logger_provider=logger_provider)

# Attach OTLP handler to root logger
logging.getLogger().addHandler(handler)
```
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/PHP/otel.png?raw=true)

### 9_2_2 Creating a Python console application (Pythonsampleapp)

- Create a file PythonSampleapp.py in /home/ubuntu/dynatrace-app/ directory and copy and paste the below code:
```
from otel import *

cpu_gauge = None
ram_gauge = None

# Callback to gather cpu usage
def get_cpu_usage_callback(_: CallbackOptions):
    for (number, percent) in enumerate(psutil.cpu_percent(percpu=True)):
        attributes = {"cpu_number": str(number)}
        yield Observation(percent, attributes)

# Callback to gather RAM memory usage
def get_ram_usage_callback(_: CallbackOptions):
    ram_percent = psutil.virtual_memory().percent
    yield Observation(ram_percent)

requests_counter = meter.create_counter(
      name="requests",
      description="number of requests",
      unit="1"
    )

requests_size = meter.create_histogram(
   name="request_size_bytes",
   description="size of requests",
   unit="byte"
   )

cpu_gauge = meter.create_observable_gauge(
        callbacks=[get_cpu_usage_callback],
        name="cpu_percent",
        description="per-cpu usage",
        unit="1"
    )

ram_gauge = meter.create_observable_gauge(
        callbacks=[get_ram_usage_callback],
        name="ram_percent",
        description="RAM memory usage",
        unit="1",
    )

staging_attributes = {"environment": "staging"}
testing_attributes = {"environment": "testing"}


print ('Python Console application started...')
print ('Sending logs...')
logging.info("Minkook loglevel info")
logging.warning("Minkook loglevel warning")
logging.error("Minkook loglevel error")
logging.critical("Minkook loglevel critical")

number = 1
try:
    while True:
        # Update the metric instruments using the direct calling convention
        print ("sending metric data (requests,request_size_bytes,cpu_percent,ram_percent)..."+str(number))
        requests_counter.add(random.randint(0, 25), staging_attributes)
        requests_size.record(random.randint(0, 300), staging_attributes)
        requests_counter.add(random.randint(0, 35), testing_attributes)
        requests_size.record(random.randint(0, 100), testing_attributes)
        number+=1
        time.sleep(5)

except KeyboardInterrupt:
    logging.critical("exiting...")
```
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/PHP/consoleapp.png?raw=true)

### Running the console application
- Click on Run and Debug button to run the PythonSampleapp console application 
- Observe the debug console while the application runs

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/PHP/rundebug.png?raw=true)

### Checking the logs in your Dynatrace Logs app 
> apply a filter to find the logs (content = * Minkook * ) there should be 2 logs per application run.

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/PHP/tenantlogs.png?raw=true)

### Checking metrics ingested (requests,request_size_bytes,cpu_percent,ram_percent) in Notebook app

- Open notebooks app and write query as below to check for request_counter metric.

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/PHP/notebooks.png?raw=true)



End of Document
