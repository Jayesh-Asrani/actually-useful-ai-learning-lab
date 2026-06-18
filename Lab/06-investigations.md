# 6 — Break It & Investigate: Assistant Investigations

*Time: ~30 min. The centerpiece. Goal: inject a real failure, launch a multi-agent Deep Investigation, and read the RCA report it produces.*

> [!NOTE]
> Assistant Investigations is in **public preview**. You need the **Assistant Investigation User** role — pre-assigned on your workshop login.

## How Investigations work (30-second mental model)

When you launch an investigation, a **lead investigator** plans the work and fans out specialized agents — **Prometheus** (metrics), **Loki** (logs), **Tempo** (traces), **Pyroscope** (profiles), and **SQL** — that gather evidence in parallel. A **reporter** compiles everything into a structured report: **Summary**, **Report**, **Timeline**, and **Activity** log.

## Step 1 — The failure is injected (once, by your instructor)

Your instructor injects the failure **once for the whole room** by running a **k6 performance test** — **Trigger Service Restart with Failure** — in the `ecommerce` project (Testing & synthetics → Performance → Projects → `ecommerce` → open the test → **Run**). It restarts a service unhealthy and produces a clean error spike for everyone to investigate against the same window.

- **Note the start time your instructor announces** — you'll hand it to the Assistant as a timeframe.
- No need to run anything yourself; everyone investigates the same incident.

> [!NOTE]
> Want to see how it's triggered? Open **Testing & synthetics → Performance → `ecommerce`** and look at the test your instructor ran. Other failure scenarios live there too — **Broken DB Connection RCA Feature Flag Controller**, **Slow DB Query RCA Feature Flag Controller**, **Trigger Beta Rollout With Failure** — for the challenge round later.

## Step 2 — Ask the Assistant which service is affected

Give it ~2–3 min for errors to accumulate. Then open the **Assistant** (✦) and ask it to find the culprit for you:

```
Something just started failing on the e-commerce app (namespace ecommerce-prod) in
the last few minutes. Which service is most affected, is the symptom errors or latency,
and roughly when did it start? Answer with the single affected service name first.
```

**Write down the service name it gives you** — you'll use it in the RCA workbench and the investigation below. (Throughout the rest of this module, replace `<SERVICE>` with that name.)

## Step 3 — Scope the RCA workbench to the affected service

1. Go to **Observability → RCA workbench**.
2. In the scope/search box, instead of *all services*, enter:

   ```
   <SERVICE> connected services
   ```

   This narrows the workbench to the affected service **plus everything connected to it** — much clearer than the whole app once you know where the problem is.
3. Review the result: you should see `<SERVICE>` and its **affected + connected services** light up with the error spike, saturation, and latency from the restart. This is the blast radius.

## Step 4 — Analyse the RCA workbench

1. In the **bottom-left** of the RCA workbench, click **Analyse**.
2. This runs the workbench's correlated root-cause analysis across `<SERVICE>` and its connected services — ranking the most likely cause and the related anomalies (errors, saturation, latency) on a shared timeline.
3. Read what it surfaces: note the suspected root cause and which connected services were dragged in. You'll compare this against what the Deep Investigation concludes next.

## Step 5 — Launch a Deep Investigation

1. Open the **Assistant** and switch the chat mode to **Investigation** (a.k.a. **Deep Investigation**). You can also open **Assistant → Investigations** to see the workspace.
2. Paste this prompt, swapping in the service name from Step 2:

```
Run a deep investigation. <SERVICE> on the e-commerce app (namespace ecommerce-prod)
started erroring a few minutes ago after an unhealthy restart. Investigate <SERVICE>
and its connected and dependent services over the last 30 minutes. Correlate metrics,
logs, and traces to find the root cause, map the blast radius across upstream and
downstream services, and recommend the next steps to remediate.
```

3. Watch the **investigation workspace**. The agents announce progress as they query metrics, logs, and traces. You can **steer** mid-flight — e.g. *"focus on the restart and pod health"* or *"check the downstream services specifically."*

## Step 6 — Read the report

When the agents finish, review:

- **Summary** — the headline finding + recommended next steps (brief stakeholders with this).
- **Report** — full findings with the actual queries and evidence each agent collected. It's editable Markdown — add a note correcting or confirming a finding.
- **Timeline** — agent tasks in order; useful for the post-incident review.
- **Activity** — raw events, so you can reproduce any single step.

**Validate it:** does the root cause match the injected failure (the service restart)? Did it identify the right service and the downstream impact?

## Step 7 — Turn findings into action

Ask the Assistant:

```
Convert this investigation into an incident summary I could post in Slack, and list 3 follow-up tasks.
```

## Step 8 — Compare notes

Compare your investigation’s root cause with a neighbour’s — did the agents converge on the same culprit? The restart test recovers on its own once it finishes; your instructor can run a different failure test (Broken DB Connection, Slow DB Query) for another round.

## ✅ Checkpoint

You investigated a real injected failure, ran a multi-agent investigation, validated the root cause against ground truth, and produced a shareable incident summary — the full "what's happening → what do I do" loop.

## Discussion

- Where would IRM webhooks fit? (Investigations can auto-launch from alert groups / incidents.)
- How does the knowledge graph from Module 2 make the investigation smarter?

Next: **[Module 7 — AI Observability →](./07-ai-observability.md)**
