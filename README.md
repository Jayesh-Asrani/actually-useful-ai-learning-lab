# Actually Useful AI with Grafana Cloud — Hands-on Workshop

Explore, break, and investigate a real cloud-native application with **Grafana Assistant** and **Assistant Investigations** — across application, Kubernetes, and AI observability.

> [!IMPORTANT]
> Your environment is already provisioned. Just [log in and get oriented](./00-login-and-orient.md) — no setup required.

## What you'll do

You'll work in a live Grafana Cloud stack monitoring an **astronomy e-commerce store** — ~20 OpenTelemetry-instrumented microservices on **Kubernetes**, which is itself an **agentic AI app** (shopping agents backed by Claude + GPT). You'll explore it without writing queries, drive the Assistant in natural language, watch a failure get injected via a **k6 load test**, run a multi-agent **Investigation** to find the root cause, and inspect the app's own **AI Observability** — the on-call loop, minus the PromQL.

## About the demo app (OpenTelemetry Astronomy Shop)

The app is built on the [**OpenTelemetry Demo**](https://opentelemetry.io/docs/demo/) — the community's reference distributed system for learning observability: a web store selling telescopes and astronomy gear. It's **polyglot by design**: each microservice is written in a different language so it exercises OpenTelemetry instrumentation across the ecosystem, and services talk over a mix of **gRPC and HTTP**.

Representative services (language in parentheses):

| Service | Role | Language |
|---------|------|----------|
| `frontend` / `frontend-proxy` | Web UI + Envoy edge proxy | TypeScript / Envoy |
| `cartservice` | Shopping cart (backed by Valkey/Redis) | .NET / C# |
| `productcatalogservice` | Product listings | Go |
| `checkoutservice` | Orchestrates an order | Go |
| `paymentservice` | Charges the order | JavaScript / Node.js |
| `shippingservice` | Shipping quotes | Rust |
| `currencyservice` | Currency conversion | C++ |
| `emailservice` | Order confirmation emails | Ruby |
| `recommendationservice` | Product recommendations | Python |
| `adservice` | Contextual ads | Java |
| `frauddetectionservice` | Fraud checks (via Kafka) | Kotlin |
| `accountingservice` | Order accounting (via Kafka) | .NET |
| `flagd` | Feature-flag service (drives failure scenarios) | Go / OpenFeature |
| `load generator` | Drives realistic traffic | Python / Locust |

**Architecture at a glance:** the `frontend` (behind `frontend-proxy`) calls downstream services over gRPC/HTTP; `checkoutservice` fans out to payment, shipping, email, currency, and cart; **Kafka** carries async events to accounting and fraud detection; **Valkey/Redis** backs the cart; and **flagd** toggles fault-injection feature flags. A bundled **load generator** keeps traffic flowing. Full diagram: [OTel Demo architecture](https://opentelemetry.io/docs/demo/architecture/).

> [!NOTE]
> This workshop stack **extends** the standard demo: it adds a `chatservice` with shopping **AI agents** (Module 6), a database tier, and **k6 tests** that trigger the failure scenarios in place of the demo's feature-flag UI.

## Format

~2.5 hours, hands-on, in a pre-provisioned Grafana Cloud stack with live telemetry. No prior Grafana or PromQL experience required.

## Agenda

| # | Module | Time | What you walk away with |
|---|--------|------|--------------------------|
| 0 | [Log in & get oriented](./00-login-and-orient.md) | 10 min | Logged in, signals confirmed, Assistant located |
| 1 | [Explore without queries — Drilldown & correlation](./Lab/01-explore-drilldown.md) | 15 min | Queryless exploration; pivot trace → logs → metrics |
| 2 | [Application Observability, knowledge graph & RCA](./Lab/02-application-observability.md) | 20 min | Service inventory (RED), Service Map, Entity graph, RCA workbench |
| 3 | [Kubernetes Observability + Assistant](./Lab/03-kubernetes-observability.md) | 15 min | Cluster/workload health; ask the Assistant about pods & nodes |
| 4 | [Meet the Assistant — chat, query, dashboard](./Lab/04-assistant-chat.md) | 20 min | Build queries & a dashboard in natural language |
| 5 | [Customize & automate — Memories, Rules & Automations](./Lab/05-automations.md) | 15 min | Teach it your env, set standards, schedule recurring work |
| 6 | [Break it & investigate — k6 + Assistant Investigations](./Lab/06-investigations.md) | 30 min | Inject a failure via k6; run a Deep Investigation, read the report |
| 7 | [AI Observability — observe the agentic app](./Lab/07-ai-observability.md) | 20 min | Conversations, agents, token cost, evals for the shopping agents |
| 8 | [Challenge: actually useful prompts](./Lab/08-assistant-challenge.md) | 15 min | Your best on-call prompts, shared with the room |


## The capabilities you'll touch

- **Grafana Assistant** (GA) — context-aware AI co-pilot inside Grafana Cloud.
- **Assistant Investigations** (public preview) — multi-agent swarm across metrics, logs, traces, and profiles that produces a structured RCA report.
- **Drilldown apps** — queryless exploration of Metrics, Logs, and Traces.
- **Application Observability** — OTel-native service inventory, RED metrics, Service Map, plus the **Entity graph** (Asserts knowledge graph) and **RCA workbench**.
- **Kubernetes Observability** — clusters, workloads, nodes, cost, and alerts, with Assistant on top.
- **AI Observability** — conversations, agents, models, token cost, and online evals for the app's own LLM agents.
- **k6 performance testing** — load tests that generate traffic and inject failure scenarios.
- **Automations** — schedule recurring agent work in natural language.

## Docs to bookmark

- [Get started with Grafana Assistant](https://grafana.com/docs/grafana-cloud/machine-learning/assistant/get-started/)
- [Run investigations](https://grafana.com/docs/grafana-cloud/machine-learning/assistant/guides/investigation/)
- [Application Observability](https://grafana.com/docs/grafana-cloud/monitor-applications/application-observability/)
- [Kubernetes Monitoring](https://grafana.com/docs/grafana-cloud/monitor-infrastructure/kubernetes-monitoring/)
- [AI Observability](https://grafana.com/blog/ai-observability-for-agents-in-grafana-cloud/)
- [Grafana Cloud k6](https://grafana.com/docs/grafana-cloud/testing/k6/)
