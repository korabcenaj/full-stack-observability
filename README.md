# Full-Stack Observability

> A self-managed metrics, alerting, logging, tracing, and network-flow stack that supports troubleshooting across application and Kubernetes boundaries, with optional energy telemetry when available.

**Status:** Validated · **Type:** Platform Capability · **Domain:** Reliability and operations

This repository contains the sanitized GitOps manifests, dashboard definitions, and alert configurations for the observability stack running on the homelab Kubernetes platform, as described in the [Korab Cenaj portfolio case study](https://korab.space/projects/full-stack-observability/).

Content is evidence-bounded: workload readiness is verified via a dated point-in-time snapshot, and unmeasured or missing telemetry is explicitly acknowledged rather than hidden.

## Contents
- `infra-repo/observability/` — GitOps manifests from the homelab cluster:
  - `monitoring.yaml` — kube-prometheus-stack (Prometheus + Grafana + Alertmanager)
  - `loki.yaml` — Loki log aggregation
  - `tempo.yaml` — Tempo distributed tracing
  - `dashboards/` — Grafana dashboard definitions
  - HTTPRoutes for Prometheus and Grafana ingress
- `enterprise-lab/observability/` — Prometheus configuration and alerts

## Problem

An application symptom can originate in code, resource pressure, a request path, storage, or a recent deployment. Separate consoles make those signals slow to correlate during investigation.

## Solution

Prometheus and Alertmanager cover metrics and alerts; Grafana brings signals together; Loki and Tempo retain logs and traces; Cilium/Hubble adds flow context; Kepler remains an optional input to capacity analysis.

## Architecture

Workloads and nodes emit metrics, logs, traces, and flow data into specialized stores; dashboards and alerts guide an operator back to the affected resource and recent change. Grafana acts purely as the visualization and correlation layer so underlying signal stores remain swappable.

## Validation & Evidence

- Prometheus, Alertmanager, Grafana, Loki, and Tempo workloads Ready on 16 July 2026
- Relevant Flux Helm releases Ready
- Kepler energy values omitted when no measured range is available (preventing false "zero usage" readings)

## Lessons Learned

- Correlating four signal types (metrics, logs, traces, flows) only works if they share consistent labels — inconsistent labeling was the main early friction point.
- Treating "no data" as distinct from "zero" for optional telemetry (Kepler) prevented at least one misleading capacity reading.
- A unified Grafana view is only as good as the alert routing underneath it — dashboards without well-tuned Alertmanager rules become something to stare at during an incident, not something that pages the right signal first.

## Limitations

- Self-managed capability, not validated at employer/production scale.
- Readiness reflects a 16 July 2026 snapshot; telemetry coverage varies by component and time window, and is not a continuous uptime guarantee.
- Kepler energy telemetry is opportunistic and not available for all workloads or time ranges.
- Formal SLOs, error-budget tracking, and long-term retention/query performance under sustained load are explicitly out of scope.

## Technologies

Prometheus, Alertmanager, Grafana, Loki, Tempo, Cilium, Hubble, Kepler, Kubernetes, FluxCD

---
See the full case study at [https://korab.space/projects/full-stack-observability/](https://korab.space/projects/full-stack-observability/).
<!-- canary-check-471428 -->
