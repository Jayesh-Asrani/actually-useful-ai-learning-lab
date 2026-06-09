# 2 — Application Observability, Knowledge Graph & RCA

*Time: ~20 min. Goal: see the Grafana Cloud differentiators the Assistant reasons on top of — service inventory, the Service Map, the Entity graph (knowledge graph), and the RCA workbench.*

Application Observability turns raw OTel data into an OTel-native view of your services. Nothing to build — it auto-detects services from telemetry.

## A. Service Inventory (RED, out of the box)

1. Left nav → **Observability → Application**.
2. You'll see the e-commerce services in the `ecommerce-prod` namespace — `frontend`, `cartservice`, `checkoutservice`, `paymentservice`, `productcatalogservice`, `recommendationservice`, `currencyservice`, `chatservice`, and more — with aggregated **RED** metrics (**R**ate, **E**rrors, **D**uration p95).
3. Sort by error rate or p95 duration. Note which services carry the most traffic and which look hot. (Use the time picker — widen to the last hour if it's quiet.)

## B. Service overview, Service Map & "Explain" a trace

1. Click a service (try `checkoutservice` or `frontend`).
2. The overview shows RED detail, top operations, and **upstream/downstream dependencies**.
3. Open the **Service Map** tab to see the topology — how requests flow `frontend → checkoutservice → paymentservice / shippingservice`, etc. This dependency graph is what the Assistant uses to reason about blast radius.
4. Drill into **Traces** for the service and open a slow or errored trace. Rather than decoding the span waterfall by hand, click **Explain** (the Assistant action on the trace) — the Assistant reads the whole trace and tells you, in plain language, where the time went, which span failed, and what to look at next.

> [!TIP]
> Use **Explain** on *any* trace, panel, or query you don't immediately understand — it's the fastest way for a newcomer to read a trace without knowing the services. Then ask a follow-up like *"why is this span slow?"* or *"show me the logs for the failing span."*
>
> Talking point: the Assistant doesn't guess your topology. It reads this map + your dashboards, which is why it can answer "how is checkout?" *and* know what checkout depends on.

## C. Entity graph — the knowledge graph (Asserts)

1. Left nav → **Observability → Entity graph**.
2. This is the **Asserts** knowledge graph: services, pods, nodes, and their relationships, enriched with health signals (Saturation, Errors, Latency, Traffic — "SLATE").
3. Pick an e-commerce service and explore how an unhealthy entity relates to its neighbours. Note one relationship you'd want to follow during an incident.

## D. RCA workbench

1. Left nav → **Observability → RCA workbench**.
2. In the service/scope selector at the top, **select all services** (use **Select all** so the workbench spans the whole `ecommerce-prod` app, not just one service). This gives you the full correlated picture across the app.
3. This is the root-cause workbench — with everything selected, it surfaces correlated anomalies (error spikes, saturation, latency) across all related entities on one timeline.
4. Look at what's currently flagged. (It gets much more interesting in Module 6 once we inject a failure — keep all services selected so the blast radius shows up.)

## ✅ Checkpoint

You've seen the layer that makes Grafana's AI observability-*native*: a service inventory with RED out of the box, an auto-built Service Map, the Asserts Entity graph, and the RCA workbench. Next: the Kubernetes layer underneath it.

Next: **[Module 3 — Kubernetes Observability →](./03-kubernetes-observability.md)**
