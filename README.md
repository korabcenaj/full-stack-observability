# Full-Stack Observability

Self-managed metrics, alerting, logging, tracing, and network-flow observability
for the homelab Kubernetes platform.

## Contents
- `infra-repo/observability/` — GitOps manifests from the homelab cluster:
  - `monitoring.yaml` — kube-prometheus-stack (Prometheus + Grafana + Alertmanager)
  - `loki.yaml` — Loki log aggregation
  - `tempo.yaml` — Tempo distributed tracing
  - `dashboards/` — Grafana dashboard definitions
  - HTTPRoutes for Prometheus and Grafana ingress
- `enterprise-lab/observability/` — Prometheus configuration and alerts

Illustrative demonstration content for a portfolio platform.
