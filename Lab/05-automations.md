# 5 — Customize & Automate the Assistant

*Time: ~15 min. Goal: make the Assistant yours — teach it your environment (Memories), set its standards (Rules), and put it on a schedule (Automations).*

Everything here lives under **Assistant → Settings** (left nav → **Assistant → Settings**, or the gear in the Assistant panel). Settings has: Custom rules, Skills, Quickstart prompts, **Assistant memories**, **Automations**, SQL table discovery, Python Sandbox, Integrations, and External connections.

## A. Assistant memories — teach it your infrastructure

1. **Assistant → Settings → Assistant memories.**
2. These are *AI-generated memories about your infrastructure discovered from your data sources.* Click **Start Discovery Scan** and the Assistant scans your telemetry to learn your services, namespaces, and dependencies.
3. Once built, the Assistant maps natural language ("how is checkout?") to the right metrics and labels in *your* environment — faster, more accurate answers with less hand-holding.

> [!TIP]
> Memories are why the Assistant in earlier modules "just knew" `checkoutservice` lives in `ecommerce-prod` and what it depends on.

## B. Custom rules — set the house standards

1. **Assistant → Settings → Custom rules** — "guide how the Assistant responds and behaves in every conversation."
2. This stack already has examples to inspect: **Executive Overview**, **Platform Overview**, **E-commerce Dashboard Guidelines**, **Default GitHub Repo**, and **Use Profiles when investigating OOMs**.
3. Open one with **Edit** to see how a rule is written, and note the scope (**Just me** / **Everybody**, and which **Applications** it applies to). Rules are how you make every agent meet *your* bar.

While you're here, glance at **Skills** and **Quickstart prompts** — reusable capabilities and one-click starting prompts you can curate for the team.

## C. Automations — agents on a schedule

*Schedule recurring agent work so insights come to you — "a morning report with your coffee."*

1. **Assistant → Settings → Automations** — "configure prompts that run automatically on a schedule, or trigger them manually."
2. Describe an automation in plain language in the input box, then **Generate**. For example:

```
Every weekday at 8am, summarize the last 24 hours of errors across the ecommerce-prod
services. Call out the top 3 by error rate and any new error patterns since yesterday.
```

3. Or start from a **Suggested automation** and customize it. They're grouped into **Incident**, **Alerts**, **Reports**, and **Personal**, e.g.:
   - *Active incident status summary* — twice a day, draft a stakeholder-friendly summary of active sev1/sev2 incidents.
   - *Weekly postmortem digest* — summarize last week's resolved incidents, recurring themes, and open action items.
   - *Morning incident context briefing* — for each active incident, summarize related alerts, deploys, and recent activity.
4. Save it; it appears under **Your automations** (scope **Just me** / **Everybody**).

> [!TIP]
> Same agent, three entry points: **Automations** to *schedule* it, **Investigations** to *summon* it on demand, and **IRM webhooks** to *auto-trigger* it on alerts.

## ✅ Checkpoint

You taught the Assistant your environment, saw how rules enforce standards across the org, and scheduled recurring agent work. Now let’s break something and watch the agents swarm.

Next: **[Module 6 — Break it & Investigate →](./06-investigations.md)**
