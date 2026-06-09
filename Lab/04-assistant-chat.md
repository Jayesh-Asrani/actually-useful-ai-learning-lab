# 4 — Meet the Assistant: Chat, Query, Dashboard

*Time: ~25 min. Goal: drive Grafana in natural language — ask questions, build queries, correlate signals, and create a dashboard, no PromQL required.*

Open the **Assistant** (sparkle ✦ icon, top-right). The chat panel is context-aware: it knows what page you're on, your data sources, and your dashboards.

> [!TIP]
> Use **`@` mentions** to anchor the Assistant to a specific service or data source — e.g. `@checkoutservice` or `@loki`. This dramatically improves accuracy.

## A. Ask about system health

Type these one at a time and watch how it picks the right metrics/labels for *your* data:

```
What's the error rate for @checkoutservice over the last hour?
```
```
Which service has the highest p95 latency right now?
```
```
Find logs mentioning "timeout" or "exception" in the last 15 minutes and tell me which service they came from.
```

## B. Build a query you didn't have to write

```
Write a PromQL query for the request rate of the frontend service, grouped by HTTP status code, and show it to me.
```

- Ask it to **explain** the query line by line. (Great for the "teach yourself observability" angle.)
- Ask it to **open this in Explore** so you can see the panel.

## C. Correlate signals in one thread

Chain the conversation — this is the on-call workflow:

```
1. Look at CPU/latency for @checkoutservice.
2. Are there any error logs for the same service during that window?
3. Pull a trace that shows where the time is going.
4. Explain how these findings relate to each other.
```

Notice it carries context between turns and pivots metrics → logs → traces for you.

## D. Build a dashboard by describing it

```
Create a dashboard for the checkoutservice with panels for request rate, error rate, p95 latency, and a panel of recent error logs. Use the OTel data from this stack.
```

- Let it generate the panels, then ask for tweaks: *"add a panel for the paymentservice latency"* or *"change the latency panel to p99."*
- **Save** the dashboard. You just built an observability dashboard without touching a query editor.

## ✅ Checkpoint

You answered health questions, generated and understood a query, correlated three signals in one thread, and built + saved a dashboard — all in natural language. Now let’s make the Assistant yours — memories, rules, and automations.

Next: **[Module 5 — Customize & Automate →](./05-automations.md)**
