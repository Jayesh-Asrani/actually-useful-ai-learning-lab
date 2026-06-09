# 3 — Kubernetes Observability + Assistant

*Time: ~15 min. Goal: see the cluster the e-commerce app runs on, and let the Assistant explain it for you.*

The e-commerce services run on Kubernetes. Grafana's Kubernetes Monitoring gives you a fleet-to-pod view with no dashboards to build.

## A. Cluster & workload health

1. Left nav → **Observability → Kubernetes**.
2. The **Overview** shows **Availability**, **Stability**, **Infrastructure**, and **Efficiency** at a glance, with `cluster` and `namespace` filters at the top.
3. Set **namespace = `ecommerce-prod`** to scope to our app.
4. Walk the left-nav sub-pages:
   - **Workloads** — deployments/statefulsets for the e-commerce services. Look for restarts, crash loops, or pending pods.
   - **Nodes** — node CPU/memory pressure.
   - **Cost** — what this namespace/workload is costing.
   - **Alerts** — any firing Kubernetes alerts.

**Try:** find a workload with the most restarts or highest memory, and open it to see pod-level detail.

## B. Let the Assistant explain it

Open the **Assistant** (✦) while you're on a Kubernetes page — it's context-aware, so it already knows what you're looking at.

```
What's the health of the ecommerce-prod namespace right now?
```
```
Which pods in ecommerce-prod have restarted recently, and why?
```
```
Is any node under CPU or memory pressure? Which workloads are driving it?
```
```
Explain what the checkoutservice deployment depends on in this cluster.
```

> [!TIP]
> Because Kubernetes telemetry, the App Observability Service Map, and the Asserts Entity graph all feed the same knowledge graph, the Assistant can connect "pod is restarting" to "service error rate is up" to "checkout is failing" — the vertical slice from infra to user impact.

## C. Connect it back to RCA

From a Kubernetes page, note the **RCA Workbench** link in the header. During an incident you'll bounce between *what's failing for users* (Application), *what's unhealthy underneath* (Kubernetes), and *why* (RCA workbench + Assistant).

## ✅ Checkpoint

You've seen the cluster under the app and used the Assistant to interpret pod/node health in plain language. Next: drive the Assistant properly — queries, correlation, and a dashboard.

Next: **[Module 4 — Meet the Assistant →](./04-assistant-chat.md)**
