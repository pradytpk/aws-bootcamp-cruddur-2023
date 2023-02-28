# 1. Week 2 — Distributed Tracing
- [1. Week 2 — Distributed Tracing](#1-week-2--distributed-tracing)
  - [1.1. Task List](#11-task-list)
  - [1.2. Observability vs Monitoring](#12-observability-vs-monitoring)
    - [1.2.1. Current State of logging](#121-current-state-of-logging)
    - [1.2.2. Why logging is hard](#122-why-logging-is-hard)
    - [1.2.3. Why Observability](#123-why-observability)
    - [1.2.4. Observability vs Monitoring](#124-observability-vs-monitoring)
    - [1.2.5. Observability in AWS](#125-observability-in-aws)
    - [1.2.6. 3 Pillar of observability](#126-3-pillar-of-observability)
    - [1.2.7. Building Security Metrics logs for Tracing](#127-building-security-metrics-logs-for-tracing)
    - [1.2.8. Central Observability Platform - Security](#128-central-observability-platform---security)
  - [1.3. HoneyComb](#13-honeycomb)
    - [1.3.1. Setup Honeycomb API key in gitpod](#131-setup-honeycomb-api-key-in-gitpod)
    - [1.3.2. Add the following Environment Variables to `backend-flask` in docker compose](#132-add-the-following-environment-variables-to-backend-flask-in-docker-compose)
    - [1.3.3. Add the opentelemetry packages in the `requirements.txt`](#133-add-the-opentelemetry-packages-in-the-requirementstxt)
    - [1.3.4. Then Install these dependencies:](#134-then-install-these-dependencies)
    - [1.3.5. Add to the `app.py`](#135-add-to-the-apppy)
    - [1.3.6. Initialize tracing and an exporter that can send data to Honeycomb](#136-initialize-tracing-and-an-exporter-that-can-send-data-to-honeycomb)
    - [1.3.7. Initialize automatic instrumentation with Flask](#137-initialize-automatic-instrumentation-with-flask)
    - [1.3.8. Acquiring a Tracer](#138-acquiring-a-tracer)
    - [1.3.9. Creating spans](#139-creating-spans)
    - [1.3.10. Exploring Honeycomb](#1310-exploring-honeycomb)
      - [1.3.10.1. Span Logs](#13101-span-logs)
      - [1.3.10.2. app.now Logs](#13102-appnow-logs)
      - [1.3.10.3. app.result\_length Logs](#13103-appresult_length-logs)
      - [1.3.10.4. Visualize MAX(app.result\_length)](#13104-visualize-maxappresult_length)
      - [1.3.10.5. Visualize HEATMAP(duration\_ms) and P90(duration\_ms)](#13105-visualize-heatmapduration_ms-and-p90duration_ms)
  - [1.4. CloudWatch Logs](#14-cloudwatch-logs)
    - [1.4.1. Setup CloudWatch](#141-setup-cloudwatch)
    - [1.4.2. Install the CloudWatch library](#142-install-the-cloudwatch-library)
    - [1.4.3. Configure cloudwatch in `app.py`](#143-configure-cloudwatch-in-apppy)
    - [1.4.4. Configuring Logger to Use CloudWatch in `app.py`](#144-configuring-logger-to-use-cloudwatch-in-apppy)
    - [1.4.5. For every request the logger should generate response use the below code in `app.py`](#145-for-every-request-the-logger-should-generate-response-use-the-below-code-in-apppy)
    - [1.4.6. Setup logger in `home_activities.py`](#146-setup-logger-in-home_activitiespy)
    - [1.4.7. Setup the env var in your backend-flask for `docker-compose.yml`](#147-setup-the-env-var-in-your-backend-flask-for-docker-composeyml)
    - [1.4.8. Check in cloudwatch for the logs](#148-check-in-cloudwatch-for-the-logs)
  - [1.5. X-Ray](#15-x-ray)
    - [1.5.1. Setup X-Ray](#151-setup-x-ray)
    - [1.5.2. Install python dependencies](#152-install-python-dependencies)
    - [1.5.3. Configuring xray to use CloudWatch in `app.py`](#153-configuring-xray-to-use-cloudwatch-in-apppy)
    - [1.5.4. Setup AWS X-Ray Resources](#154-setup-aws-x-ray-resources)
    - [1.5.5. Setup AWS X-Ray Group](#155-setup-aws-x-ray-group)
    - [1.5.6. Setup AWS X-Ray Sampling Groups](#156-setup-aws-x-ray-sampling-groups)
    - [1.5.7. Add Deamon Service to Docker Compose](#157-add-deamon-service-to-docker-compose)
    - [1.5.8. Add these two env vars to our backend-flask in our `docker-compose.yml` file](#158-add-these-two-env-vars-to-our-backend-flask-in-our-docker-composeyml-file)
    - [1.5.9. Hit some backend api activities and check xrays in aws](#159-hit-some-backend-api-activities-and-check-xrays-in-aws)
  - [1.6. Rollbar](#16-rollbar)
    - [Setup Rollbar](#setup-rollbar)
    - [Install deps](#install-deps)
    - [We need to set our access token](#we-need-to-set-our-access-token)
    - [Import for Rollbar](#import-for-rollbar)
    - [Initialize Rollbar](#initialize-rollbar)
    - [Add an endpoint just for testing rollbar to `app.py`](#add-an-endpoint-just-for-testing-rollbar-to-apppy)
    - [Add to backend-flask for `docker-compose.yml`](#add-to-backend-flask-for-docker-composeyml)
    - [Rollbar walk through](#rollbar-walk-through)
      - [Warning log](#warning-log)
      - [Error log](#error-log)
## 1.1. Task List
- [x] Watch Week 2 Live-Stream Video(26/02/2023)
- [ ] Watch Chirag Week 2 - Spending Considerations
- [x] Watched Ashish's Week 2 - Observability Security Considerations(27/02/2023)
- [x] Instrument Honeycomb with OTEL(27/02/2023)
- [x] Instrument AWS X-Ray(27/02/2023)
- [x] Configure custom logger to send to CloudWatch Logs(27/02/2023)
- [x] Integrate Rollbar and capture and error(28/02/2023)
## 1.2. Observability vs Monitoring
### 1.2.1. Current State of logging
- On-Premise Logs
  - infrastructure
  - Applications
  - Antivirus
  - Fire wall etc
- Cloud Logs
  - Infrastructure
  - Applications
  - Anti-Virus
  - Firewall
  
### 1.2.2. Why logging is hard
- Time consuming
- Tons of data
- Increase alert fatigue

### 1.2.3. Why Observability
- Decreased Alert Fatigue for Security and Operation teams
- Visibility of end to end of logs,metrics and tracing
- Troubleshoot
- Understand application health
- Accelerate collaboration between teams
- Reduce overall operational cost
- Increase customer satisfaction

### 1.2.4. Observability vs Monitoring
|Factors| Observability  | Monitoring  |
|---|---|---|
|Fault Management|  why did it occur | when & where did it occurs  |
|Recovery|  What can i do to prevent the issue from reoccurring | Is my system back up?  |

### 1.2.5. Observability in AWS
- The way to  breakdown the entire application for viewing it for better understanding

### 1.2.6. 3 Pillar of observability
1. Metrics
   - AWS Cloudwatch
2. Traces
   - AWS X Rays
3. Logs
   - AWS Cloudwatch
   - AWS Trail
### 1.2.7. Building Security Metrics logs for Tracing
1. Which Application?
2. TYpe of Application?
3. Threat Modelling Session
4. Identity Attack Vectors
5. Map Attack vectors
6. Identity instrumentation agents to create tracing
7. AWS Service like AWS Distro for openTelemetry
8. Dashboard for Practical Attack
9. Repeat for next application

### 1.2.8. Central Observability Platform - Security
- Event driven Architecture
- Open Source Dashboards
- SIEM(Security Incident and Event Management)

## 1.3. HoneyComb
### 1.3.1. Setup Honeycomb API key in gitpod
- Create a new Environment in ui.honeycomb.io
- Get the api keys for the services
```sh
export HONEYCOMB_API_KEY="MY API KEY"
export HONEYCOMB_SERVICE_NAME="Cruddur"
gp env HONEYCOMB_API_KEY="MY API KEY"
gp env HONEYCOMB_SERVICE_NAME="Cruddur"
env | grep HONEY
```
![honeycomb](../_docs/assets/honeycombapi_setup_confirmation.png)

### 1.3.2. Add the following Environment Variables to `backend-flask` in docker compose

```yml
OTEL_EXPORTER_OTLP_ENDPOINT: "https://api.honeycomb.io"
OTEL_EXPORTER_OTLP_HEADERS: "x-honeycomb-team=${HONEYCOMB_API_KEY}"
OTEL_SERVICE_NAME: "${HONEYCOMB_SERVICE_NAME}"
```

### 1.3.3. Add the opentelemetry packages in the `requirements.txt`
- Add the following files to our `\aws-bootcamp-cruddur-2023\backend-flask\requirements.txt`

```
opentelemetry-api 
opentelemetry-sdk 
opentelemetry-exporter-otlp-proto-http 
opentelemetry-instrumentation-flask 
opentelemetry-instrumentation-requests
```

### 1.3.4. Then Install these dependencies:

```sh
cd backend-flask/
pip install -r requirements.txt
```
![opentelemetry](../_docs/assets/opentelemetry.png)

### 1.3.5. Add to the `app.py`

```py
from opentelemetry import trace
from opentelemetry.instrumentation.flask import FlaskInstrumentor
from opentelemetry.instrumentation.requests import RequestsInstrumentor
from opentelemetry.exporter.otlp.proto.http.trace_exporter import OTLPSpanExporter
from opentelemetry.sdk.trace import TracerProvider
from opentelemetry.sdk.trace.export import BatchSpanProcessor
```

### 1.3.6. Initialize tracing and an exporter that can send data to Honeycomb

```py
provider = TracerProvider()
processor = BatchSpanProcessor(OTLPSpanExporter())
provider.add_span_processor(processor)
trace.set_tracer_provider(provider)
tracer = trace.get_tracer(__name__)
```

### 1.3.7. Initialize automatic instrumentation with Flask

```py
app = Flask(__name__)
FlaskInstrumentor().instrument_app(app)
RequestsInstrumentor().instrument()
```

### 1.3.8. Acquiring a Tracer

```py
trace = trace.get_tracer("home.activities")
```

### 1.3.9. Creating spans

```py

with tracer.start_as_current_span("http-handler"):
    with tracer.start_as_current_span("my-cool-function"):

```
### 1.3.10. Exploring Honeycomb
#### 1.3.10.1. Span Logs
![honeycomb_span](../_docs/assets/honeycomb_span.png)
![honeycomb_span](../_docs/assets/honeycomb_span1.png)
#### 1.3.10.2. app.now Logs
![honeycomb_span](../_docs/assets/honeycomb_span2.png)
#### 1.3.10.3. app.result_length Logs
![honeycomb_span](../_docs/assets/honeycomb_span3.png)
#### 1.3.10.4. Visualize MAX(app.result_length)
![honeycomb_span](../_docs/assets/honeycomb_span4.png)
#### 1.3.10.5. Visualize HEATMAP(duration_ms) and P90(duration_ms)
![honeycomb_span](../_docs/assets/honeycomb_span5.png)

## 1.4. CloudWatch Logs

### 1.4.1. Setup CloudWatch

Add to the `requirements.txt`

```
watchtower
```
### 1.4.2. Install the CloudWatch library
```sh
pip install -r requirements.txt
```
### 1.4.3. Configure cloudwatch in `app.py`

```
import watchtower
import logging
from time import strftime
```
### 1.4.4. Configuring Logger to Use CloudWatch in `app.py`
```py

LOGGER = logging.getLogger(__name__)
LOGGER.setLevel(logging.DEBUG)
console_handler = logging.StreamHandler()
cw_handler = watchtower.CloudWatchLogHandler(log_group='cruddur')
LOGGER.addHandler(console_handler)
LOGGER.addHandler(cw_handler)
LOGGER.info("Test log")
```
### 1.4.5. For every request the logger should generate response use the below code in `app.py`
```py
@app.after_request
def after_request(response):
    timestamp = strftime('[%Y-%b-%d %H:%M]')
    LOGGER.error('%s %s %s %s %s %s', timestamp, request.remote_addr, request.method, request.scheme, request.full_path, response.status)
    return response
```

### 1.4.6. Setup logger in `home_activities.py`
```py
LOGGER.info('Hello Cloudwatch! from  /api/activities/home')
```
### 1.4.7. Setup the env var in your backend-flask for `docker-compose.yml`

```yml
      AWS_DEFAULT_REGION: "${AWS_DEFAULT_REGION}"
      AWS_ACCESS_KEY_ID: "${AWS_ACCESS_KEY_ID}"
      AWS_SECRET_ACCESS_KEY: "${AWS_SECRET_ACCESS_KEY}"
```
### 1.4.8. Check in cloudwatch for the logs
![cloudwatch](../_docs/assets/cloudwatchlog0.png)
![cloudwatch](../_docs/assets/cloudwatchlog1.png)
![cloudwatch](../_docs/assets/cloudwatchlog2.png)

## 1.5. X-Ray

### 1.5.1. Setup X-Ray
Add to the `requirements.txt`

```py
aws-xray-sdk
```

### 1.5.2. Install python dependencies

```sh
pip install -r requirements.txt
```

###  1.5.3. Configuring xray to use CloudWatch in `app.py`

```py
from aws_xray_sdk.core import xray_recorder
from aws_xray_sdk.ext.flask.middleware import XRayMiddleware
xray_url = os.getenv("AWS_XRAY_URL")
xray_recorder.configure(service='backend-flask', dynamic_naming=xray_url)
XRayMiddleware(app, xray_recorder)
```

###  1.5.4. Setup AWS X-Ray Resources

Add `aws/json/xray.json`

```json
{
  "SamplingRule": {
      "RuleName": "Cruddur",
      "ResourceARN": "*",
      "Priority": 9000,
      "FixedRate": 0.1,
      "ReservoirSize": 5,
      "ServiceName": "Cruddur",
      "ServiceType": "*",
      "Host": "*",
      "HTTPMethod": "*",
      "URLPath": "*",
      "Version": 1
  }
}
```
###  1.5.5. Setup AWS X-Ray Group
```sh
FLASK_ADDRESS="https://4567-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}"
aws xray create-group \
   --group-name "Cruddur" \
   --filter-expression "service(\"backend-flask\")"
```
![xray](../_docs/assets/xray1.png)
![xray](../_docs/assets/xray2.png)

###  1.5.6. Setup AWS X-Ray Sampling Groups
```sh
aws xray create-sampling-rule --cli-input-json file://aws/json/xray.json
```
![xray](../_docs/assets/xray3.png)
![xray](../_docs/assets/xray4.png)

### 1.5.7. Add Deamon Service to Docker Compose

```yml
  xray-daemon:
    image: "amazon/aws-xray-daemon"
    environment:
      AWS_ACCESS_KEY_ID: "${AWS_ACCESS_KEY_ID}"
      AWS_SECRET_ACCESS_KEY: "${AWS_SECRET_ACCESS_KEY}"
      AWS_REGION: "${AWS_REGION}"
    command:
      - "xray -o -b xray-daemon:2000"
    ports:
      - 2000:2000/udp
```

### 1.5.8. Add these two env vars to our backend-flask in our `docker-compose.yml` file

```yml
      AWS_XRAY_URL: "*4567-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}*"
      AWS_XRAY_DAEMON_ADDRESS: "xray-daemon:2000"
```

### 1.5.9. Hit some backend api activities and check xrays in aws
![aws1](../_docs/assets/demoan1.png)
![aws1](../_docs/assets/demoan2.png)


## 1.6. Rollbar
- Create a new project in Rollbar called `Cruddur`
- https://rollbar.com/

### Setup Rollbar
- Add to `requirements.txt`

```
blinker
rollbar
```
### Install deps

```sh
pip install -r requirements.txt
```

### We need to set our access token

```sh
export ROLLBAR_ACCESS_TOKEN=""
gp env ROLLBAR_ACCESS_TOKEN=""
```
![rollbar](../_docs/assets/rollbar.png)

### Import for Rollbar

```py
import rollbar
import rollbar.contrib.flask
from flask import got_request_exception
```
### Initialize Rollbar
```py
rollbar_access_token = os.getenv('ROLLBAR_ACCESS_TOKEN')
@app.before_first_request
def init_rollbar():
    """init rollbar module"""
    rollbar.init(
        # access token
        rollbar_access_token,
        # environment name
        'production',
        # server root directory, makes tracebacks prettier
        root=os.path.dirname(os.path.realpath(__file__)),
        # flask already sets up logging
        allow_logging_basic_config=False)
    # send exceptions from `app` to rollbar, using flask's signal system.
    got_request_exception.connect(rollbar.contrib.flask.report_exception, app)
```

### Add an endpoint just for testing rollbar to `app.py`

```py
@app.route('/rollbar/test')
def rollbar_test():
    rollbar.report_message('Hello World!', 'warning')
    return "Hello World!"
```

### Add to backend-flask for `docker-compose.yml`

```yml
ROLLBAR_ACCESS_TOKEN: "${ROLLBAR_ACCESS_TOKEN}"
```

### Rollbar walk through
#### Warning log
![rollbar2](../_docs/assets/rollbar1.png) 
#### Error log
![rollbar3](../_docs/assets/rollbar500.png) 
[Rollbar Flask Example](https://github.com/rollbar/rollbar-flask-example/blob/master/hello.py)