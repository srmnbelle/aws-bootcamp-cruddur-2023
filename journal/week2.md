# Week 2 — Distributed Tracing

## **HW Checklist**

- [**REQUIRED**](#assignments)
  - [ ] [1]()
  - [ ] [2]()
  - [ ] [3]()
- [**EXTRA CHALLENGES**](#extra-challenges)
  - [ ] [1]()
  - [ ] [2]()
  - [ ] [3]()

## **LECTURES**

### Live Stream | [FREE AWS Cloud Project Bootcamp (Week 2) - Distributed Tracing](https://www.youtube.com/watch?v=2GD9xCzRId4)

- Distributed tracing
  - modern standard on "observability"
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
  - Save your API key and service name to Gitpod

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

  - asd

- some task

### Pre-recorded |

## **ASSIGNMENTS**

### 1

### 2

### 3

## **EXTRA CHALLENGES**

### 1

### 2

### 3
