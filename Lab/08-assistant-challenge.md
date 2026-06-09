# 8 — 🧠 Challenge: Actually Useful Prompts

*Time: ~15 min. The finale.*

By now you have:

- Explored metrics, logs, and traces queryless (Drilldown) and correlated between them
- Seen Application Observability — service inventory, Service Map, Entity graph (knowledge graph) and RCA workbench
- Toured Kubernetes Observability and let the Assistant explain pod/node health
- Driven the Assistant to query, correlate, and build a dashboard
- Run a multi-agent Investigation on a real failure injected via a k6 test
- Inspected the app's own AI Observability — conversations, agents, token cost, evals
- Customized the Assistant with Memories + Rules and scheduled an Automation

## The goal

Find the **most useful** thing the Assistant can do for *your* day job. Work solo or in pairs.

Craft prompts and capture the responses. At the end, be ready to share your **best 1–2 prompts**, the response, and a one-line "why this is useful / when I'd reach for it in real life."

> [!TIP]
> Think like someone on-call. The best prompts tend to:
> - Find the errors that actually matter (not just noisy ones)
> - Spot patterns *before* they become incidents
> - Tell you what to look at *next*
> - Reduce toil by doing the task, not just describing it

## Prompt ideas to riff on

```
What are the most common causes of errors across my services in the last hour?
```
```
Are there any unusual spikes in request patterns, latency, or status codes today?
```
```
If I were paged for @checkoutservice right now, what should I investigate first — and why?
```
```
Compare this week's error patterns to last week's. What's new or getting worse?
```
```
Build me an SLO-style view for the frontend service and tell me if we're burning error budget.
```
```
Walk a brand-new engineer through how the checkout flow works based on the traces.
```
```
Which shopping agent is the most expensive per conversation, and how would you cut its token cost?
```
```
Are any pods in ecommerce-prod unhealthy, and is that affecting user-facing services?
```

## Bonus rounds

- **Investigation prompt-off:** have your facilitator run a *different* k6 failure test (Broken DB Connection vs. Slow DB Query) and see whose Deep Investigation nails the root cause fastest.
- **Teach-me mode:** ask the Assistant to explain a PromQL or TraceQL query it wrote, well enough that you could write it yourself next time.
- **Customize it:** write a Custom Rule (e.g. "always answer with the affected service and a next step") and re-run a prompt to see the behavior change.

## Share out

Drop your best prompt + response in the workshop channel (or read it to the room). We'll vote on the most *actually useful* one. 🏆

---

Thanks for exploring, breaking, and investigating with us — across application, Kubernetes, and AI observability.

Docs: [Grafana Assistant](https://grafana.com/docs/grafana-cloud/machine-learning/assistant/) · [Investigations](https://grafana.com/docs/grafana-cloud/machine-learning/assistant/guides/investigation/) · [Application Observability](https://grafana.com/docs/grafana-cloud/monitor-applications/application-observability/) · [Kubernetes Monitoring](https://grafana.com/docs/grafana-cloud/monitor-infrastructure/kubernetes-monitoring/) · [AI Observability](https://grafana.com/blog/ai-observability-for-agents-in-grafana-cloud/)
