# 1. Week 2 — Distributed Tracing
- [1. Week 2 — Distributed Tracing](#1-week-2--distributed-tracing)
  - [1.1. Task List](#11-task-list)
  - [1.2. Week 2 - Spending Considerations](#12-week-2---spending-considerations)
  - [1.3. Observability vs Monitoring](#13-observability-vs-monitoring)
    - [1.3.1. Current State of logging](#131-current-state-of-logging)
    - [1.3.2. Why logging is hard](#132-why-logging-is-hard)
    - [1.3.3. Why Observability](#133-why-observability)
    - [1.3.4. Observability vs Monitoring](#134-observability-vs-monitoring)
    - [1.3.5. Observability in AWS](#135-observability-in-aws)
    - [1.3.6. 3 Pillar of observability](#136-3-pillar-of-observability)
    - [1.3.7. Building Security Metrics logs for Tracing](#137-building-security-metrics-logs-for-tracing)
    - [1.3.8. Central Observability Platform - Security](#138-central-observability-platform---security)
  - [1.4. HoneyComb](#14-honeycomb)
    - [1.4.1. Setup Honeycomb API key in gitpod](#141-setup-honeycomb-api-key-in-gitpod)
    - [1.4.2. Add the following Environment Variables to `backend-flask` in docker compose](#142-add-the-following-environment-variables-to-backend-flask-in-docker-compose)
    - [1.4.3. Add the opentelemetry packages in the `requirements.txt`](#143-add-the-opentelemetry-packages-in-the-requirementstxt)
    - [1.4.4. Then Install these dependencies:](#144-then-install-these-dependencies)
    - [1.4.5. Add to the `app.py`](#145-add-to-the-apppy)
    - [1.4.6. Initialize tracing and an exporter that can send data to Honeycomb](#146-initialize-tracing-and-an-exporter-that-can-send-data-to-honeycomb)
    - [1.4.7. Initialize automatic instrumentation with Flask](#147-initialize-automatic-instrumentation-with-flask)
    - [1.4.8. Acquiring a Tracer](#148-acquiring-a-tracer)
    - [1.4.9. Creating spans](#149-creating-spans)
    - [1.4.10. Exploring Honeycomb](#1410-exploring-honeycomb)
      - [1.4.10.1. Span Logs](#14101-span-logs)
      - [1.4.10.2. app.now Logs](#14102-appnow-logs)
      - [1.4.10.3. app.result\_length Logs](#14103-appresult_length-logs)
      - [1.4.10.4. Visualize MAX(app.result\_length)](#14104-visualize-maxappresult_length)
      - [1.4.10.5. Visualize HEATMAP(duration\_ms) and P90(duration\_ms)](#14105-visualize-heatmapduration_ms-and-p90duration_ms)
  - [1.5. CloudWatch Logs](#15-cloudwatch-logs)
    - [1.5.1. Setup CloudWatch](#151-setup-cloudwatch)
    - [1.5.2. Install the CloudWatch library](#152-install-the-cloudwatch-library)
    - [1.5.3. Configure cloudwatch in `app.py`](#153-configure-cloudwatch-in-apppy)
    - [1.5.4. Configuring Logger to Use CloudWatch in `app.py`](#154-configuring-logger-to-use-cloudwatch-in-apppy)
    - [1.5.5. For every request the logger should generate response use the below code in `app.py`](#155-for-every-request-the-logger-should-generate-response-use-the-below-code-in-apppy)
    - [1.5.6. Setup logger in `home_activities.py`](#156-setup-logger-in-home_activitiespy)
    - [1.5.7. Setup the env var in your backend-flask for `docker-compose.yml`](#157-setup-the-env-var-in-your-backend-flask-for-docker-composeyml)
    - [1.5.8. Check in cloudwatch for the logs](#158-check-in-cloudwatch-for-the-logs)
  - [1.6. X-Ray](#16-x-ray)
    - [1.6.1. Setup X-Ray](#161-setup-x-ray)
    - [1.6.2. Install python dependencies](#162-install-python-dependencies)
    - [1.6.3. Configuring xray to use CloudWatch in `app.py`](#163-configuring-xray-to-use-cloudwatch-in-apppy)
    - [1.6.4. Setup AWS X-Ray Resources](#164-setup-aws-x-ray-resources)
    - [1.6.5. Setup AWS X-Ray Group](#165-setup-aws-x-ray-group)
    - [1.6.6. Setup AWS X-Ray Sampling Groups](#166-setup-aws-x-ray-sampling-groups)
    - [1.6.7. Add Deamon Service to Docker Compose](#167-add-deamon-service-to-docker-compose)
    - [1.6.8. Add these two env vars to our backend-flask in our `docker-compose.yml` file](#168-add-these-two-env-vars-to-our-backend-flask-in-our-docker-composeyml-file)
    - [1.6.9. Hit some backend api activities and check xrays in aws](#169-hit-some-backend-api-activities-and-check-xrays-in-aws)
  - [1.7. Rollbar](#17-rollbar)
    - [1.7.1. Setup Rollbar](#171-setup-rollbar)
    - [1.7.2. Install deps](#172-install-deps)
    - [1.7.3. We need to set our access token](#173-we-need-to-set-our-access-token)
    - [1.7.4. Import for Rollbar](#174-import-for-rollbar)
    - [1.7.5. Initialize Rollbar](#175-initialize-rollbar)
    - [1.7.6. Add an endpoint just for testing rollbar to `app.py`](#176-add-an-endpoint-just-for-testing-rollbar-to-apppy)
    - [1.7.7. Add to backend-flask for `docker-compose.yml`](#177-add-to-backend-flask-for-docker-composeyml)
    - [1.7.8. Rollbar walk through](#178-rollbar-walk-through)
      - [1.7.8.1. Warning log](#1781-warning-log)
      - [1.7.8.2. Error log](#1782-error-log)
## 1.1. Task List
- [x] Watch Week 2 Live-Stream Video(26/02/2023)
- [x] Watch Chirag Week 2 - Spending Considerations(03/03/2023)
- [x] Watched Ashish's Week 2 - Observability Security Considerations(27/02/2023)
- [x] Instrument Honeycomb with OTEL(27/02/2023)
- [x] Instrument AWS X-Ray(27/02/2023)
- [x] Configure custom logger to send to CloudWatch Logs(27/02/2023)
- [x] Integrate Rollbar and capture and error(28/02/2023)

## 1.2. Week 2 - Spending Considerations
- Honeycomb spend information(2 Millions)
- Rollbar is for error data(5000 events)
- AWS X-Rays 1,00,000 Forever free
  - 1 Million is free
- AWS Cloudwatch 10 metrics always free
  - 5GB is free
## 1.3. Observability vs Monitoring
### 1.3.1. Current State of logging
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
  
### 1.3.2. Why logging is hard
- Time consuming
- Tons of data
- Increase alert fatigue

### 1.3.3. Why Observability
- Decreased Alert Fatigue for Security and Operation teams
- Visibility of end to end of logs,metrics and tracing
- Troubleshoot
- Understand application health
- Accelerate collaboration between teams
- Reduce overall operational cost
- Increase customer satisfaction

### 1.3.4. Observability vs Monitoring
| Factors          | Observability                                       | Monitoring                 |
| ---------------- | --------------------------------------------------- | -------------------------- |
| Fault Management | why did it occur                                    | when & where did it occurs |
| Recovery         | What can i do to prevent the issue from reoccurring | Is my system back up?      |

### 1.3.5. Observability in AWS
- The way to  breakdown the entire application for viewing it for better understanding

### 1.3.6. 3 Pillar of observability
1. Metrics
   - AWS Cloudwatch
2. Traces
   - AWS X Rays
3. Logs
   - AWS Cloudwatch
   - AWS Trail
### 1.3.7. Building Security Metrics logs for Tracing
1. Which Application?
2. TYpe of Application?
3. Threat Modelling Session
4. Identity Attack Vectors
5. Map Attack vectors
6. Identity instrumentation agents to create tracing
7. AWS Service like AWS Distro for openTelemetry
8. Dashboard for Practical Attack
9. Repeat for next application

### 1.3.8. Central Observability Platform - Security
- Event driven Architecture
- Open Source Dashboards
- SIEM(Security Incident and Event Management)

## 1.4. HoneyComb
### 1.4.1. Setup Honeycomb API key in gitpod
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

### 1.4.2. Add the following Environment Variables to `backend-flask` in docker compose

```yml
OTEL_EXPORTER_OTLP_ENDPOINT: "https://api.honeycomb.io"
OTEL_EXPORTER_OTLP_HEADERS: "x-honeycomb-team=${HONEYCOMB_API_KEY}"
OTEL_SERVICE_NAME: "${HONEYCOMB_SERVICE_NAME}"
```

### 1.4.3. Add the opentelemetry packages in the `requirements.txt`
- Add the following files to our `\aws-bootcamp-cruddur-2023\backend-flask\requirements.txt`

```
opentelemetry-api 
opentelemetry-sdk 
opentelemetry-exporter-otlp-proto-http 
opentelemetry-instrumentation-flask 
opentelemetry-instrumentation-requests
```

### 1.4.4. Then Install these dependencies:

```sh
cd backend-flask/
pip install -r requirements.txt
```
![opentelemetry](../_docs/assets/opentelemetry.png)

### 1.4.5. Add to the `app.py`

```py
from opentelemetry import trace
from opentelemetry.instrumentation.flask import FlaskInstrumentor
from opentelemetry.instrumentation.requests import RequestsInstrumentor
from opentelemetry.exporter.otlp.proto.http.trace_exporter import OTLPSpanExporter
from opentelemetry.sdk.trace import TracerProvider
from opentelemetry.sdk.trace.export import BatchSpanProcessor
```

### 1.4.6. Initialize tracing and an exporter that can send data to Honeycomb

```py
provider = TracerProvider()
processor = BatchSpanProcessor(OTLPSpanExporter())
provider.add_span_processor(processor)
trace.set_tracer_provider(provider)
tracer = trace.get_tracer(__name__)
```

### 1.4.7. Initialize automatic instrumentation with Flask

```py
app = Flask(__name__)
FlaskInstrumentor().instrument_app(app)
RequestsInstrumentor().instrument()
```

### 1.4.8. Acquiring a Tracer

```py
trace = trace.get_tracer("home.activities")
```

### 1.4.9. Creating spans

```py

with tracer.start_as_current_span("http-handler"):
    with tracer.start_as_current_span("my-cool-function"):

```
### 1.4.10. Exploring Honeycomb
#### 1.4.10.1. Span Logs
![honeycomb_span](../_docs/assets/honeycomb_span.png)
![honeycomb_span](../_docs/assets/honeycomb_span1.png)
#### 1.4.10.2. app.now Logs
![honeycomb_span](../_docs/assets/honeycomb_span2.png)
#### 1.4.10.3. app.result_length Logs
![honeycomb_span](../_docs/assets/honeycomb_span3.png)
#### 1.4.10.4. Visualize MAX(app.result_length)
![honeycomb_span](../_docs/assets/honeycomb_span4.png)
#### 1.4.10.5. Visualize HEATMAP(duration_ms) and P90(duration_ms)
![honeycomb_span](../_docs/assets/honeycomb_span5.png)

## 1.5. CloudWatch Logs

### 1.5.1. Setup CloudWatch

Add to the `requirements.txt`

```
watchtower
```
### 1.5.2. Install the CloudWatch library
```sh
pip install -r requirements.txt
```
### 1.5.3. Configure cloudwatch in `app.py`

```
import watchtower
import logging
from time import strftime
```
### 1.5.4. Configuring Logger to Use CloudWatch in `app.py`
```py

LOGGER = logging.getLogger(__name__)
LOGGER.setLevel(logging.DEBUG)
console_handler = logging.StreamHandler()
cw_handler = watchtower.CloudWatchLogHandler(log_group='cruddur')
LOGGER.addHandler(console_handler)
LOGGER.addHandler(cw_handler)
LOGGER.info("Test log")
```
### 1.5.5. For every request the logger should generate response use the below code in `app.py`
```py
@app.after_request
def after_request(response):
    timestamp = strftime('[%Y-%b-%d %H:%M]')
    LOGGER.error('%s %s %s %s %s %s', timestamp, request.remote_addr, request.method, request.scheme, request.full_path, response.status)
    return response
```

### 1.5.6. Setup logger in `home_activities.py`
```py
LOGGER.info('Hello Cloudwatch! from  /api/activities/home')
```
### 1.5.7. Setup the env var in your backend-flask for `docker-compose.yml`

```yml
      AWS_DEFAULT_REGION: "${AWS_DEFAULT_REGION}"
      AWS_ACCESS_KEY_ID: "${AWS_ACCESS_KEY_ID}"
      AWS_SECRET_ACCESS_KEY: "${AWS_SECRET_ACCESS_KEY}"
```
### 1.5.8. Check in cloudwatch for the logs
![cloudwatch](../_docs/assets/cloudwatchlog0.png)
![cloudwatch](../_docs/assets/cloudwatchlog1.png)
![cloudwatch](../_docs/assets/cloudwatchlog2.png)

## 1.6. X-Ray

### 1.6.1. Setup X-Ray
Add to the `requirements.txt`

```py
aws-xray-sdk
```

### 1.6.2. Install python dependencies

```sh
pip install -r requirements.txt
```

###  1.6.3. Configuring xray to use CloudWatch in `app.py`

```py
from aws_xray_sdk.core import xray_recorder
from aws_xray_sdk.ext.flask.middleware import XRayMiddleware
xray_url = os.getenv("AWS_XRAY_URL")
xray_recorder.configure(service='backend-flask', dynamic_naming=xray_url)
XRayMiddleware(app, xray_recorder)
```

###  1.6.4. Setup AWS X-Ray Resources

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
###  1.6.5. Setup AWS X-Ray Group
```sh
FLASK_ADDRESS="https://4567-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}"
aws xray create-group \
   --group-name "Cruddur" \
   --filter-expression "service(\"backend-flask\")"
```
![xray](../_docs/assets/xray1.png)
![xray](../_docs/assets/xray2.png)

###  1.6.6. Setup AWS X-Ray Sampling Groups
```sh
aws xray create-sampling-rule --cli-input-json file://aws/json/xray.json
```
![xray](../_docs/assets/xray3.png)
![xray](../_docs/assets/xray4.png)

### 1.6.7. Add Deamon Service to Docker Compose

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

### 1.6.8. Add these two env vars to our backend-flask in our `docker-compose.yml` file

```yml
      AWS_XRAY_URL: "*4567-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}*"
      AWS_XRAY_DAEMON_ADDRESS: "xray-daemon:2000"
```

### 1.6.9. Hit some backend api activities and check xrays in aws
![aws1](../_docs/assets/demoan1.png)
![aws1](../_docs/assets/demoan2.png)


## 1.7. Rollbar
- Create a new project in Rollbar called `Cruddur`
- https://rollbar.com/

### 1.7.1. Setup Rollbar
- Add to `requirements.txt`

```
blinker
rollbar
```
### 1.7.2. Install deps

```sh
pip install -r requirements.txt
```

### 1.7.3. We need to set our access token

```sh
export ROLLBAR_ACCESS_TOKEN=""
gp env ROLLBAR_ACCESS_TOKEN=""
```
![rollbar](../_docs/assets/rollbar.png)

### 1.7.4. Import for Rollbar

```py
import rollbar
import rollbar.contrib.flask
from flask import got_request_exception
```
### 1.7.5. Initialize Rollbar
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

### 1.7.6. Add an endpoint just for testing rollbar to `app.py`

```py
@app.route('/rollbar/test')
def rollbar_test():
    rollbar.report_message('Hello World!', 'warning')
    return "Hello World!"
```

### 1.7.7. Add to backend-flask for `docker-compose.yml`

```yml
ROLLBAR_ACCESS_TOKEN: "${ROLLBAR_ACCESS_TOKEN}"
```

### 1.7.8. Rollbar walk through
#### 1.7.8.1. Warning log
![rollbar2](../_docs/assets/rollbar1.png) 
#### 1.7.8.2. Error log
![rollbar3](../_docs/assets/rollbar500.png) 
[Rollbar Flask Example](https://github.com/rollbar/rollbar-flask-example/blob/master/hello.py)