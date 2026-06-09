# 1 — Explore Without Queries: Drilldown & Correlation

*Time: ~15 min. Goal: get answers from metrics, logs, and traces without writing a single query — and pivot between signals.*

The Drilldown apps let you explore telemetry by clicking, not by typing PromQL/LogQL/TraceQL. This is the "week one shouldn't be about learning the tool" promise in action.

## A. Metrics Drilldown

1. Go to **Drilldown → Metrics**.
2. Browse the metrics emitted by the e-commerce app. Filter by label — try `service_name` (or `service.name`) and pick `checkoutservice` or `frontend`.
3. Click a metric to see it broken out by label dimensions automatically. Notice you never wrote a query.

**Try:** find request rate or latency for the `frontend` service and note the time range where traffic is heaviest.

## B. Logs Drilldown

1. Go to **Drilldown → Logs**.
2. Filter to a service (e.g. `service_name = cartservice`). Drilldown surfaces log **volume**, detected **patterns**, and **fields** for you.
3. Click into a spike or an error pattern to read the underlying lines.

**Try:** isolate any `error`/`exception` level logs and identify which service is noisiest.

## C. Traces Drilldown

1. Go to **Drilldown → Traces**.
2. Explore the **RED** view — rate, errors, duration — across services without TraceQL.
3. Open a slow or errored trace and walk the span waterfall. See which service and operation dominates the latency.

## D. Correlate across signals (the payoff)

This is where it clicks. From a single trace you can hop to the exact logs for that request:

1. In Traces Drilldown, open a trace for `checkoutservice` or `frontend`.
2. Find a span with high latency or an error tag.
3. Use the span's **Logs for this span** / trace-to-logs link to jump straight into the logs emitted during that request (trace ↔ logs correlation comes from the shared `trace_id`).
4. Now go the other way: from an error log line, follow the **trace_id** back into the trace to see the full request path.

> [!TIP]
> OTel instrumentation injects `trace_id` into logs automatically, which is what makes this one-click pivot possible. No manual derived-field setup needed for OTLP data.

## ✅ Checkpoint

You found a hotspot in metrics, confirmed it in logs, and saw the full request path in traces — moving between all three signals by clicking. Keep the service you found interesting (e.g. `checkoutservice`, `cartservice`, or `frontend`) in mind; you'll point the Assistant at it next.

Next: **[Module 2 — Application Observability & RCA →](./02-application-observability.md)**
