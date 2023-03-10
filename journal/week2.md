# Week 2 — Distributed Tracing

## **HW Checklist**

- [**REQUIRED**](#assignments)
  - [x] [Instrument Honeycomb with OTEL](#instrument-honeycomb-with-otel)
  - [x] [Instrument AWS X-Ray](#instrument-aws-x-ray)
  - [x] [Instrument AWS X-Ray Subsegments](#instrument-aws-x-ray-subsegments)
  - [x] [Configure custom logger to send to CloudWatch Logs](#configure-custom-logger-to-send-to-cloudwatch-logs)
  - [x] [Integrate Rollbar and capture and error](#integrate-rollbar-and-capture-and-error)
- [**EXTRA CHALLENGES**](#extra-challenges)
  - [ ] [Instrument Honeycomb for the frontend application](#instrument-honeycomb-for-the-frontend-application-to-observe-network-latency-between-frontend-and-backend-hard)
  - [ ] [Add custom instrumentation to Honeycomb](#add-custom-instrumentation-to-honeycomb-to-add-more-attributes-eg-userid-add-a-custom-span)
  - [ ] [Run custom queries in Honeycomb](#run-custom-queries-in-honeycomb-and-save-them-later-eg-latency-by-userid-recent-traces)

## **LECTURES**

### Live Stream | [FREE AWS Cloud Project Bootcamp (Week 2) - Distributed Tracing](https://www.youtube.com/watch?v=2GD9xCzRId4)

- Personal thoughts: I LOVE Jessica and Andrew's **energy** and passion on teaching this instrumentation topic 🔥
- Distributed tracing
  - modern standard on "observability" (hot buzz word for your resume)
  - a story of what's happening
    - "trace" - the story
    - "span" - every row, has start time and duration, repesents a single unit of work of as apart of serving a request
    - "fields" - details on each span
- Observability tools
  - logging
  - tracing
  - metrics
- Instructional material: [omenking's Week 2](https://github.com/omenking/aws-bootcamp-cruddur-2023/tree/week-2)
- Initial Set-up

  - Log-in to [honeycomb](honeycomb.io)
  - Create new environment
  - Save your API key to Gitpod

    ```bash
    export HONEYCOMB_API_KEY="<API key here>"
    gp env HONEYCOMB_API_KEY="<API key here>"
    ```

  - Add to backend-flask services environment in `docker-compose.yml`
    - OTel - short for open telemetry; [documentation](https://opentelemetry.io/docs/)
    - This step configures OTEL to send to honeycomb
    ```yml
    OTEL_EXPORTER_OTLP_ENDPOINT: "https://api.honeycomb.io"
    OTEL_EXPORTER_OTLP_HEADERS: "x-honeycomb-team=${HONEYCOMB_API_KEY}"
    OTEL_SERVICE_NAME: "backend-flask"
    ```

- Sending data to Honeycomb

  - Install packages
    - Change directory to `/backend-flask`
      - Doing `pip install opentelemetry-api` won't work ?
    - Add to `requirements.txt` file
      ```
      opentelemetry-api
      opentelemetry-sdk
      opentelemetry-exporter-otlp-proto-http
      opentelemetry-instrumentation-flask
      opentelemetry-instrumentation-requests
      ```
    - Run `pip install -r requirements.txt`
  - Initialize

    - Add to `app.py`

      ```py
      # HoneyComb
      from opentelemetry import trace
      from opentelemetry.instrumentation.flask import FlaskInstrumentor
      from opentelemetry.instrumentation.requests import RequestsInstrumentor
      from opentelemetry.exporter.otlp.proto.http.trace_exporter import OTLPSpanExporter
      from opentelemetry.sdk.trace import TracerProvider
      from opentelemetry.sdk.trace.export import BatchSpanProcessor

      # Initialize tracing and an exporter that can send data to Honeycomb
      provider = TracerProvider()
      processor = BatchSpanProcessor(OTLPSpanExporter())
      provider.add_span_processor(processor)
      trace.set_tracer_provider(provider)
      tracer = trace.get_tracer(__name__)

      # Initialize automatic instrumentation with Flask
      FlaskInstrumentor().instrument_app(app)
      RequestsInstrumentor().instrument()
      ```

- Configure front-end
  - Change directory to `/frontend-react-js`
  - Do `npm i`
- Compose up the `docker-compose.yml`
  - Add to `gitpod.yml` to unlock 3000 and 4567 ports by default
    ```yml
    ports:
      - name: frontend
        port: 3000
        onOpen: open-browser
        visibility: public
      - name: backend
        port: 4567
        visibility: public
      - name: xray-daemon
        port: 2000
        visibility: public
    ```
- Open Cruddur app

  - Open link using port 3000
  - Open link using port 4567 and append `/api/activities/home`

- Troubleshooting

  - Add to `app.py`

    ```py
    from opentelemetry.sdk.trace.export import ConsoleSpanExporter, SimpleSpanProcessor

    # Show this in the logs within the backend-flask app (STDOUT)
    simple_processor = SimpleSpanProcessor(ConsoleSpanExporter())
    provider.add_span_processor(simple_processor)
    ```

  - Following the livestream, `env | grep HONEY` shows nothing for me. So I had to export my API keys again. Docker logs for my back-end also show spans but few seconds it returns:
    ```bash
    Failed to export batch code: 401, reason: {"message":"missing 'x-honeycomb-team' header"}
    ```
  - ⭐ Committing changes to git, closing gitpod, `npm i` on frontend, composing up the .yml SOLVED IT

- Add spans and attributes

  - [Acquiring a tracer](https://docs.honeycomb.io/getting-data-in/opentelemetry/python/#acquiring-a-tracer)
    - Open `/backend-flask/services/home_activities.py`
    - Add the lines:
      ```py
      # Acquiring tracer
      from opentelemetry import trace
      tracer = trace.get_tracer("home.activities")
      ```
  - [Create the span](https://docs.honeycomb.io/getting-data-in/opentelemetry/python/#creating-spans)

    - Add the lines under the run() function:

      ```py
      # Creating a span
      with tracer.start_as_current_span("home-activities-mock-data"):
      ```

  - [Add attributes](https://docs.honeycomb.io/getting-data-in/opentelemetry/python/#adding-attributes-to-spans)

    - Add the lines:

    ```py
    span = trace.get_current_span()
    # now statement here
    span.set_attribute("app.now", now.isoformat())
    span.set_attribute("app.result_length", len(results))
    ```

    - Tab matters 😅

### Additional Instructions | [Week 2 Instrument XRay](https://www.youtube.com/watch?v=n2DTsuBrD_A&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=33&t=1s)

- Xray - AWS built-in solution similar to honeycomb
- AWS XRay APIs reference here: [boto3](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/xray.html) and [github](https://github.com/aws/aws-xray-sdk-python)
- Middleware - "software" between application and request for filtering, post-processing, or formatting

- Set-up

  - Code npm install in `.gitpod.yml`
  - Add `aws-xray-sdk` to `requirements.txt` and run `pip install -r requirements.txt`
  - Add the ff code to `app.py`

    ```py
    # AWS XRay
    from aws_xray_sdk.core import xray_recorder
    from aws_xray_sdk.ext.flask.middleware import XRayMiddleware

    xray_url = os.getenv("AWS_XRAY_URL")
    xray_recorder.configure(service='backend-flask', dynamic_naming=xray_url)
    XRayMiddleware(app, xray_recorder)
    ```

  - Create `xray.json` under aws/json folder with content:
    ```json
    {
      "SamplingRule": {
        "RuleName": "Cruddur",
        "ResourceARN": "*",
        "Priority": 9000,
        "FixedRate": 0.1,
        "ReservoirSize": 5,
        "ServiceName": "backend-flask",
        "ServiceType": "*",
        "Host": "*",
        "HTTPMethod": "*",
        "URLPath": "*",
        "Version": 1
      }
    }
    ```
  - CREATE GROUP using AWS CLI; then double-check if reflected in AWS UI [here](https://us-east-1.console.aws.amazon.com/cloudwatch/home?region=us-east-1#xray:settings/groups)
    ```bash
    aws xray create-group \
    --group-name "Cruddur" \
    --filter-expression "service(\"backend-flask\")"
    ```
  - CREATE SAMPLING RULE using AWS CLI
    ```bash
    aws xray create-sampling-rule --cli-input-json file://aws/json/xray.json
    ```
  - Add daemon service to `docker-compose.yml`

    ```yml
    # this under frontend-react-js services section
    xray-daemon:
      image: "amazon/aws-xray-daemon"
      environment:
        AWS_ACCESS_KEY_ID: "${AWS_ACCESS_KEY_ID}"
        AWS_SECRET_ACCESS_KEY: "${AWS_SECRET_ACCESS_KEY}"
        AWS_REGION: "us-east-1"
      command:
        - "xray -o -b xray-daemon:2000"
      ports:
        - 2000:2000/udp

    # this under backend-flask env vars:
    AWS_XRAY_URL: "*4567-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}*"
    AWS_XRAY_DAEMON_ADDRESS: "xray-daemon:2000"
    ```

- Debugging

  - `Compose Up` the `docker-compose.yml` file
    - backend-flask will not be running; View logs using docker extension will show
      > NameError: name 'app' is not defined
      - Move the line `XRayMiddleware(app, xray_recorder)` under `app = Flask(__name__)`
    - unfortunately, my frontend-react-js is also not running; View logs using docker extension shows
      > sh: 1: react-scripts: not found
      - `cd frontend-react-js` and `npm i`
  - Check if being logged by clicking `View Logs` of aws-xray-daemon in Docker extension or by viewing through AWS website under CloudWatch/XRay traces/Traces menu

- [Starting a custom sub-segment](https://github.com/aws/aws-xray-sdk-python#start-a-custom-segmentsubsegment)
  - Edit `user_activities.py` - not working as of the end of the video

### Additional Instructions | [ Week 2 - X-Ray Subsegments Solved ](https://www.youtube.com/watch?v=4SGTW0Db5y0&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=38)

- Reference article: [How to add custom X-Ray Segments for Containerised Flask Application](https://olley.hashnode.dev/aws-free-cloud-bootcamp-instrumenting-aws-x-ray-subsegments)
- Preliminaries
  - `npm i` the frontend
  - `compose up` the docker file
  - Open the port 3000 and append /@username
  - `view logs` the aws-xray-daemon
- Debugging:
  - Add the lines in `app.py`
    ```python
    @xray_recorder.capture('activities_home') # under /api/activities/home
    @xray_recorder.capture('activities_users') # under /api/activities/@<string:handle>
    @xray_recorder.capture('activities_show') # under /api/activities/<string:activity_uuid>
    ```
  - Refresh the port 3000 link a lot then check AWS XRay traces site
  - Add `xray_recorder.end_subsegment()` in `user_activities.py`
  - `mock-data` span should show in the AWS traces site!

### Additional Instructions | [Week 2 CloudWatch Logs](https://www.youtube.com/watch?v=ipdFizZjOF4&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=34&t=1s)

- Reference instructions: [omenking's Week 2](https://github.com/omenking/aws-bootcamp-cruddur-2023/blob/week-2/journal/week2.md)
- Initial Set-up
  - Edit `requirements.txt` and RUN `pip install -r requirements.txt`
  - Edit `app.py` following the reference instructions
  - Edit `home_activities.py` and ADD line `LOGGER.info("HomeActivities")`
  - Edit `docker-compose.yml`
  - `Compose up` and open port 4567 and append `/api/activities/home`
- Debugging
  - Will initially show error: `NameError: name 'LOGGER' is not defined`
  - Following the video, changing LOGGER to logger, my code still returns `TypeError: unsupported operand type(s) for @: 'Response' and 'method'`
    - Just copy pasted the code in app.py two times 😓 OK now!
- Disable codelines to save spend.

### Additional Instructions | [Week 2 - Rollbar](https://www.youtube.com/watch?v=xMBDAb5SEU4&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=36)

- Reference instructions: [omenking's Week 2](https://github.com/omenking/aws-bootcamp-cruddur-2023/blob/week-2/journal/week2.md)
- Initial Set-up
  - Create Rollbar account, select Flask SDK, note your access token
  - Edit `requirements.txt` and RUN `pip install -r requirements.txt`
  - Edit `app.py` following the reference instructions
  - `Compose up` and open port 4567 and append `/api/activities/home`
- Debugging
  - Move the `@app.before_first_request` code block lower
  - Check port 4567 and append `/rollbar/test` if showing `Hello World!`
  - Attach shell to backend through docker and check env for rollbar access tokens
    - Commit to git and restart gitpod
    - ⭐ ADD `ROLLBAR_ACCESS_TOKEN: "${ROLLBAR_ACCESS_TOKEN}"` to the `docker-compose.yml`
      - You should see the rollbar items on the website now!
  - Remove `return` in `home_activities.py` to test error logs in rollbar - and fix before committing to git

### Security Session | [Observability vs Monitoring Explained in AWS](https://www.youtube.com/watch?v=bOf4ITxAcXc&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=32)

- Logging - can be (1) on-premise logs or (2) cloud logs
- Observability - looking at the holistic view
- Observability vs Monitoring
  - monitoring is the logs itself; will provide fault and recovery info
  - observability is the entire life cycle of a program; will identify & prevent issues
- Observability in AWS - breaking down the app into multiple processes
- 3 pillars
  - logs
  - metrics - answers how/why/what
  - traces - identify cause
- Cloudtrail -> Cloudwatch demo
- Steps for security metrics/logs for tracing
  - Use of threat model - phishing email, ddos, distributed nano attacks, malware
  - Note industry standards/techniques by hacker; documentation: "attack mitter"
  - Identify instrumentation agents - cloudwatch, security hub, etc
- Central observability platform
  - AWS Security hub & eventbridge
  - Just design a event-driven architecture - analogy: toll gates
  - Others: SIEM? Open-source dashboards?

### Pricing Session | [AWS Bootcamp Week 2 - Honeycomb, Rollbar, AWS X-Ray and AWS Cloudwatch Logs pricing considerations](https://www.youtube.com/watch?v=2W3KeqCjtDY&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=39)

- Honeycomb - freetier allows 20M events/month
- Rollbar - 5k events/month
- AWS X-ray - 100k traces/month; pricing differs depending if traces/scanning
- AWS Cloudwatch - 5GB log data; note to disable!

### Additional Instructions | [Week 2- Github Codespaces Crash Course](https://www.youtube.com/watch?v=L9KKBXgKopA&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=37)

- To be watched

### Cloud Career Session | [Pick the right cloud role: A beginners guide!](https://www.youtube.com/watch?v=E0haz6mymxY&list=PLBfufR7vyJJ7k25byhRXJldB5AiwgNnWv&index=35&t=308s)

- To be watched

## **ASSIGNMENTS**

### Instrument Honeycomb with OTEL

<img width="955" alt="livestream logs backend" src="https://user-images.githubusercontent.com/64080430/221867085-ccabfff9-37a9-4dad-89e5-6a5c34b478a9.png">

> Docker logs at backend

<img width="459" alt="livestream honeycomb data - tracer with span" src="https://user-images.githubusercontent.com/64080430/221867133-56ecac7c-8782-4827-8916-ac56d10b1a39.png">

> Honeycomb trace data with span

### Instrument AWS X-Ray

<img width="959" alt="XRAY aws traces spans" src="https://user-images.githubusercontent.com/64080430/222966985-d667db3b-5266-44e2-9694-c2eb743d09bb.png">

### Instrument AWS X-Ray Subsegments

<img width="960" alt="XRAY subsegment mock-data" src="https://user-images.githubusercontent.com/64080430/222966956-cc4b13fc-2db8-49fe-a62d-ca50905c049a.png">

> `mock-data` now shows on AWS XRay traces UI

### Configure custom logger to send to CloudWatch Logs

<img width="957" alt="CLOUDWATCH" src="https://user-images.githubusercontent.com/64080430/224535413-1b15f565-d35f-46bf-9ef9-7d58fccb22ef.png">

> Verify logs at AWS Cloudwatch app

### Integrate Rollbar and capture and error

<img width="960" alt="ROLLBAR" src="https://user-images.githubusercontent.com/64080430/224545909-c78cedb7-c0ac-4c6f-81ba-70c1e329d5fa.png">

> Viewing _intentional_ error logs in Rollbar

## **EXTRA CHALLENGES**

### Instrument Honeycomb for the frontend-application to observe network latency between frontend and backend [HARD]

- To test latency between frontend and backend

### Add custom instrumentation to Honeycomb to add more attributes eg. UserId, Add a custom span

- Add attribute with context, how it is useful

### Run custom queries in Honeycomb and save them later eg. Latency by UserID, Recent Traces

- Done in livestream, try others then save them
