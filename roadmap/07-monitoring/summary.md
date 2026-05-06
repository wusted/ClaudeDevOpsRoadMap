# Module 07: Monitoring & Observability (Prometheus + Grafana)

## Why This Module

Diego is already a monitoring expert — Splunk Certified Admin with years of log analysis. This module transitions that expertise from log-centric monitoring to the full observability stack (metrics, logs, traces) that DevOps teams use for cloud-native infrastructure.

## Key Concepts

### From Splunk to Cloud-Native Observability

| Diego Knows (Splunk) | DevOps Equivalent |
|---|---|
| Splunk indexers | Prometheus TSDB / Loki |
| SPL queries | PromQL / LogQL |
| Splunk dashboards | Grafana dashboards |
| Splunk alerts | Alertmanager + PagerDuty |
| Forwarders | Exporters / agents |
| Splunk apps/TAs | Grafana plugins / mixins |

Diego's advantage: He understands WHY monitoring matters and HOW to investigate issues. This module is about learning the cloud-native tools, not the philosophy.

### Three Pillars of Observability

1. **Metrics**: Numeric measurements over time (Prometheus)
   - Counters, gauges, histograms, summaries
   - Time series data, labels, cardinality
2. **Logs**: Event records (Loki, ELK)
   - Structured logging (JSON)
   - Log aggregation and correlation
3. **Traces**: Request flow across services (Jaeger, Tempo)
   - Distributed tracing (spans, trace IDs)
   - Service maps and latency analysis

### Prometheus Architecture

- **Pull model**: Prometheus scrapes targets (vs Splunk push model)
- **Exporters**: Expose metrics in Prometheus format
- **PromQL**: Query language for metrics (Diego's SPL skills transfer)
- **Alertmanager**: Alert routing, grouping, silencing
- **Service discovery**: Auto-find targets in Kubernetes

### Grafana

- Dashboard creation (panels, variables, annotations)
- Data source integration (Prometheus, Loki, CloudWatch, etc.)
- Alerting (unified alerting since Grafana 9)
- Dashboard-as-code (JSON models, Grafonnet, Terraform provider)

### SLOs and SLIs

- Service Level Indicators (what you measure)
- Service Level Objectives (what you target)
- Error budgets (how much failure is acceptable)
- Burn rate alerts (alert before SLO breach, not after)

### Infrastructure Monitoring

- Node exporter (Linux system metrics — Diego knows what these mean)
- cAdvisor (container metrics)
- kube-state-metrics (Kubernetes object metrics)
- Application instrumentation (custom metrics)

## Topics

1. Observability fundamentals (metrics, logs, traces)
2. Prometheus setup and configuration
3. PromQL queries (connect to Diego's SPL expertise)
4. Grafana dashboards and visualization
5. Alertmanager and alert routing
6. Loki for log aggregation
7. Kubernetes monitoring stack
8. Application instrumentation
9. SLOs, SLIs, and error budgets
10. Infrastructure monitoring with Terraform (monitoring-as-code)
