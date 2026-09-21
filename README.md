# AIOps Monitoring Assessment

## Pull Request
Open pull request: [DebbieAUG/github-skills-challenge#180](https://github.com/DebbieAUG/github-skills-challenge/pull/180)

This repository simulates a lightweight AIOps monitoring workflow for a payment service. The service emits operational telemetry in the form of request timing, CPU and memory usage, and log events. The goal is to detect abnormal behaviour, turn the relevant observations into anomaly events, and pass those events through a simple event-streaming pipeline to an AIOps output layer.

## Service being monitored
The monitored service is a payment-processing application called `payment-service`. It handles transaction requests and emits telemetry such as request latency, resource utilization, and log entries.

## Operational problem being addressed
The service occasionally shows slow response times, high CPU or memory consumption, and error-level logs. Without automated detection, these issues can be missed until customers experience failures or the service becomes unstable. This assessment focuses on identifying those abnormal patterns early and routing the findings through a basic event-driven workflow.

## Purpose of AIOps in this assessment
AIOps is used to detect unusual operational signals automatically, summarize why they are suspicious, and forward the findings through a producer-topic-consumer pipeline so the downstream operations workflow can act on the issue.

## Operational data analysis
The data in `data/service_data.json` contains a time series of service records. Each object includes:

- `timestamp`: when the observation was recorded
- `service`: the monitored application name
- `response_time_ms`: a metric that tracks request latency
- `cpu_percent`: a metric for CPU utilization
- `memory_percent`: a metric for memory utilization
- `log_level`: the severity of the operational log entry
- `message`: the corresponding log or event message

### Normal observations
Entries with response times around 120-150 ms, CPU around 40-50%, memory around 50-57%, and `INFO` log levels are consistent with normal service operations. These records show steady throughput without unusual resource pressure.

### Anomalous observations
The unusual records are around `2026-09-20T10:05:00` and `2026-09-20T10:06:00`.

They show:
- significantly higher latency (`610` ms and `640` ms)
- elevated CPU usage (`75%` and `94%`)
- elevated memory usage (`70%` and `91%`)
- `ERROR` log messages such as `Payment service timeout` and `Database connection timeout`

These are the expected anomalies and they are clearly distinguishable from the stable records that surround them.

## Anomaly detection findings
The `AnomalyDetector` flags a record when it exceeds the configured operational thresholds or reports an error-level log. The reasons are captured in a readable `reasons` list, which makes it clear why a record was marked as anomalous.

Detected anomalies include:
- high response time
- high CPU utilization
- high memory utilization
- error log detected

This approach is effective for this synthetic data because the abnormal records are obvious and separated from normal behaviour.

## Event-processing flow
The event-processing flow is:

1. Operational data is ingested.
2. `AnomalyDetector` inspects each record.
3. An anomaly event is created when a record meets the detection rules.
4. `EventProducer` publishes the anomaly event to the topic.
5. `EventConsumer` reads the published event from the same topic.
6. The downstream AIOps pipeline output consumes and summarizes the event.

The core components are:
- `EventProducer`: publishes an anomaly to the in-memory topic
- `EventTopic`: stores the messages in memory as a lightweight topic simulation
- `EventConsumer`: receives the message from the topic
- `ANOMALY` event: the message payload containing the service, timestamp, and reasons

## Final workflow execution result
The end-to-end workflow processes the operational data, identifies the two anomalous service records, publishes the corresponding anomaly events, and the consumer successfully receives them. The final output reports the detected operational issue and explains the reasons behind the event.

## Issues identified and corrected
The project initially had a few workflow issues:

- import resolution was failing because the package structure was not correctly exposed for test execution
- the anomaly detector was checking the wrong log severity (`WARNING` instead of `ERROR`)
- the producer and consumer were writing to different in-memory topics, which prevented the simulated event flow from completing correctly

These issues were fixed while preserving the existing architecture.

## Limitation and possible improvement
This detection approach is rule-based and relies on static thresholds. A limitation is that it can miss more subtle degradations that do not exceed the configured thresholds. A possible improvement would be to add baseline or rolling-window-based detection so the service can identify unusual trends rather than only fixed threshold breaches.

## Reproduction steps
1. Open the repository in VS Code or GitHub Codespaces.
2. Ensure Python dependencies are installed with `pip install -r requirements.txt`.
3. Run the anomaly workflow from the project root:
   `python src/aiops_pipeline.py`
4. Run the automated validation suite:
   `pytest -q`
5. Review the detected anomalies and the event flow output.

---

The project now demonstrates the complete AIOps monitoring loop: operational data → anomaly detection → event generation → producer → topic → consumer → final AIOps output.

