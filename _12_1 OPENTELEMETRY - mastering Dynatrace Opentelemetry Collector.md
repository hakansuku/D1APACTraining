# 12_1_1 Building an simple application and instrumenting with Opentelemetry LOGS , METRICS and TRACES 

## In this tutorial we will spin a Ubuntu linux AWS::EC2 instance , we will build a simple web application and enable opentelemetry in Pyton.

- Prepare a development ubuntu VM instance (refer to previous exercise 1_2)
- SSH into the Ubuntu terminal 
  
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/OTELcollector/SSHterminal.jpg)

- update and upgrade ubuntu
```
sudo su
apt update -y
apt upgrade -y
```

- Create application directory and install python-venv 

```
mkdir otel-getting-started
cd otel-getting-started
apt install -y  python3.14-venv
python3 -m venv venv
source ./venv/bin/activate
```
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/OTELcollector/pythonvenv.jpg)

- Install Flask, instrument with opentelemetry and install exporter
> Zero-code instrumentation will generate telemetry data on your behalf. Here we’ll use the opentelemetry-instrument agent. Install the opentelemetry-distro package, which contains the OpenTelemetry API, SDK and also the tools opentelemetry-bootstrap and opentelemetry-instrument
```
pip install flask
pip install opentelemetry-distro
opentelemetry-bootstrap -a install
pip install opentelemetry-exporter-otlp
```
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/OTELcollector/flask.jpg)

- Create and launch an HTTP Server
> Create a file app.py and add the following code to it:
> I simply used vi editor 
```
vi app.py
```
> paste the following code into the app.py file and save.
```
# These are the necessary import declarations
from opentelemetry import trace
from opentelemetry import metrics

from random import randint
from flask import Flask, request
import logging

# Acquire a tracer
tracer = trace.get_tracer("diceroller.tracer")
# Acquire a meter.
meter = metrics.get_meter("diceroller.meter")

# Now create a counter instrument to make measurements with
roll_counter = meter.create_counter(
    "dice.rolls",
    description="The number of rolls by roll value",
)

app = Flask(__name__)
logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)

@app.route("/rolldice")
def roll_dice():
    # This creates a new span that's the child of the current one
    with tracer.start_as_current_span("roll") as roll_span:
        player = request.args.get('player', default = None, type = str)
        result = str(roll())
        roll_span.set_attribute("roll.value", result)
        # This adds 1 to the counter for the given roll value
        roll_counter.add(1, {"roll.value": result})
        if player:
            logger.warning("%s is rolling the dice: %s", player, result)
        else:
            logger.warning("Anonymous player is rolling the dice: %s", result)
        return result

def roll():
    return randint(1, 6)
```
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/OTELcollector/apppy.jpg)

- Now run the application on port 8080
> Below command will launch the instrumented app and display logs,traces and metrics into the console while running
> NOTE: observe how --traces_exporter console --metrics_exporter console --logs_exporter console parameters are set to console.  We will change this later to feed into Dynatrace OTEL collector.
```
opentelemetry-instrument --traces_exporter console --metrics_exporter console --logs_exporter console --service_name dice-server flask run --host=0.0.0.0 -p 8080
```
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/OTELcollector/apprunning.jpg)

- ensure your Ubuntu host has network inbound port 8080 open and has public ip
> make sure you add into inbound rule for TCP port 8080 for the application to be accessible

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/OTELcollector/inboundport.jpg)

- Now test your application via browser 
> use http://<your ip address>:8080/rolldice

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/OTELcollector/testapp.jpg)

> observe that each time you send the http request via browser , dice rolls and gives a random result. 
> At the same time you will be able to observe the traces, metrics and logs being displayed in the SSH console terminal while the application is running 

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/OTELcollector/traces.jpg?raw=true)

> In the next chapter I will show how to install Dynatrace Opentelemetry collector and configure to accept opentelemetry for ingestion to a tenant

- End of document -



