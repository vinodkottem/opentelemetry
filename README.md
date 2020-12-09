# Opentelemetry setup for multiple backends [wip]

This helps to create full OTEL setup and test it to receive traces in multiple formats and export to multiple formats

* Flows

1. Zipkin-trace-generator  --> (@Zipkin)Collector(@Zipkin)  ---> Zipkin backends


## Setup OpenTelemetry collector

The following steps will deploy a OTEL collector and agent daemonset in `telemetry` namespace to receive traces in zipkin and jaeger

Note: All files are configured to run in `telemetry` namespace

* Create namespace `telemetry`

```bash
kubectl create namespace telemetry
```

* Apply files in `collector-setup` 

Note: Refer config for both collector & agent for more details

```bash
cd collector-setup
kubectl apply -f collector.yaml
```

## Setup zipkin to receive traces from OTEL collector and expose zipkin UI on NodePort `31001`

* Apply files in `zipkin-setup`

```bash
cd zipkin-setup
kubectl apply -f all.yaml
```

* Access zipkin UI @  [localhost:31001](http://localhost:31001)

## Setup zipkin trace load generator

* Apply files in `zipkin-omnition-load`

```bash
cd zipkin-omnition-load
kubectl apply -f deploy.yaml
```


