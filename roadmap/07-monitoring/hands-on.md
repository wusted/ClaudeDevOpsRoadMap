# Module 07: Monitoring & Observability — Hands-On Exercises

## Module Repository: `observability-stack`

All deliverables for this module live in `repos/observability-stack/` and on GitHub at `github.com/<username>/observability-stack`. Create it with `/setup-repo` before starting Exercise 7.1.

The repo's README should describe it as a complete observability portfolio: Prometheus + Grafana stacks (local and Kubernetes), custom dashboards, alert pipelines, SLO definitions, and monitoring-as-code patterns.

Replace earlier paths like `devops-lab/monitoring/...` with in-repo equivalents.

---

## Exercise 7.1: Prometheus + Grafana Stack (Local)

**Objective**: Deploy the monitoring stack locally and understand the pull model.

**Steps**:
1. Create `devops-lab/monitoring/docker-compose.yml` with:
   - Prometheus (with config file)
   - Grafana (with provisioned datasources)
   - Node Exporter (system metrics)
   - A sample app with /metrics endpoint
2. Configure Prometheus scrape targets
3. Access Prometheus UI, explore metrics, run basic PromQL queries
4. Access Grafana, verify Prometheus datasource
5. Import the Node Exporter dashboard (ID: 1860)
6. Compare the pull model vs Splunk's forwarder push model

**Validation**: Prometheus scraping all targets, Grafana showing live system metrics

---

## Exercise 7.2: PromQL Mastery

**Objective**: Build proficiency in PromQL (translate Diego's SPL skills).

**Context**: PromQL is different from SPL but the analytical thinking is the same.

**Steps**:
1. Practice queries against node_exporter metrics:
   - CPU usage percentage: `100 - (avg by(instance)(rate(node_cpu_seconds_total{mode="idle"}[5m])) * 100)`
   - Memory usage: `node_memory_MemTotal_bytes - node_memory_MemAvailable_bytes`
   - Disk I/O rate: `rate(node_disk_read_bytes_total[5m])`
2. Practice label filtering and aggregation
3. Work with `rate()`, `increase()`, `histogram_quantile()`
4. Create recording rules for expensive queries
5. Document a "PromQL cheat sheet" comparing equivalent SPL queries

**Validation**: Can write queries for CPU, memory, disk, network. Cheat sheet maps SPL → PromQL.

---

## Exercise 7.3: Custom Grafana Dashboards

**Objective**: Build production-quality dashboards from scratch.

**Steps**:
1. Create a dashboard for the sample application:
   - Request rate (requests/sec)
   - Error rate (4xx and 5xx responses)
   - Latency (p50, p95, p99)
   - Saturation (CPU, memory usage)
2. Add template variables (instance selector, time range)
3. Add annotations (deployments, incidents)
4. Create a "RED method" dashboard (Rate, Errors, Duration)
5. Export the dashboard as JSON
6. Provision it via Grafana's file-based provisioning

**Validation**: Dashboard shows the four golden signals, variables work, JSON is exportable/reproducible

---

## Exercise 7.4: Alerting Pipeline

**Objective**: Build an alerting system from metric to notification.

**Steps**:
1. Define alert rules in Prometheus:
   - High CPU (>80% for 5 minutes)
   - High memory (>90%)
   - Service down (target unreachable for 1 minute)
   - High error rate (>5% of requests failing)
2. Configure Alertmanager:
   - Route critical alerts to one channel, warnings to another
   - Group related alerts
   - Configure silence and inhibition rules
3. Test by triggering alerts (stress test, stop a service)
4. Integrate with a notification channel (Slack webhook, email, or PagerDuty free tier)

**Validation**: Alerts fire correctly, routing works, notifications reach the configured channel

---

## Exercise 7.5: Kubernetes Monitoring Stack

**Objective**: Deploy the complete monitoring stack on Kubernetes using Helm.

**Steps**:
1. Install kube-prometheus-stack via Helm:
   ```
   helm install monitoring prometheus-community/kube-prometheus-stack
   ```
2. Explore the pre-built dashboards (node, pod, namespace, cluster)
3. Deploy your app from Module 06 with Prometheus annotations
4. Create a ServiceMonitor custom resource for your app
5. Build a custom dashboard for your application in the cluster
6. Set up alerts specific to your application's SLIs
7. Simulate a failure and trace the alert path

**Validation**: Full stack running in K8s, custom app metrics scraped, alerts configured and tested

---

## Exercise 7.6: Monitoring as Code (Terraform + Grafana)

**Objective**: Manage dashboards and alerts with Terraform (IaC for observability).

**Steps**:
1. Use the Grafana Terraform provider
2. Create dashboards via Terraform resources (JSON model)
3. Create alert rules via Terraform
4. Create notification channels via Terraform
5. Store in git, apply via CI pipeline
6. Modify a dashboard via PR, observe the change applied automatically

**Validation**: Grafana configuration fully managed by Terraform, changes deployed via git
