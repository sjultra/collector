# Collector

A [Telegraf](https://www.influxdata.com/time-series-platform/telegraf/) agent that pushes metrics to [Monitoring](https://github.com/sjultra/monitoring)'s ingest endpoint, plus the Grafana dashboards that show them. Each install brings its own inputs and dashboards; the agent and output are the chart's.

## Chart

`helm/service`. Values:
- `inputs` (required): Telegraf input plugins as TOML. May use `${VAR}` from `env`.
- `env`: environment for the agent.
- `dashboards`: `{ "<name>.json": "<dashboard JSON>" }`, each a ConfigMap labeled `grafana_dashboard: "1"`.
- `output.url`: defaults to `http://ingest.victoriametrics.svc:8428` (InfluxDB line protocol).

```
helm install speedtest helm/service --create-namespace --namespace speedtest \
  --set-string inputs='[[inputs.internet_speed]]'
```

Published as `oci://ghcr.io/sjultra/charts/collector`. To release: Releases → "Draft a new release" → tag `vX.Y.Z` → Publish.
