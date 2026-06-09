# 7 — AI Observability: Observe the Agentic App

*Time: ~20 min. Goal: the meta-moment — the e-commerce app is itself an AI agent app, and Grafana's AI Observability lets you see inside its LLM calls, costs, and quality.*

Remember `chatservice`? The store has an AI shopping assistant built from multiple agents (`general_agent`, `product_agent`, `cart_agent`) backed by Claude and GPT models. AI Observability gives you a forensic view of how those agents behave — the same tooling Grafana uses to improve the Assistant itself.

## A. Generate your own conversation, then trace it back

This is the payoff — you'll create AI telemetry and immediately find it.

1. Open the **storefront** (the e-commerce app — ask your facilitator for the URL, or use the `frontend` route). Find the **shopping assistant / chat** widget.
2. Have a short conversation about **telescopes** — e.g.:
   > "I'm a beginner — recommend a telescope under $200 for viewing planets."
   
   Ask a follow-up or two ("what about for astrophotography?", "add the first one to my cart") so multiple agents get involved. **Note the rough time** you chatted.
3. Now switch to Grafana: **Observability → AI → Conversations**.
4. Find **your** conversation at the top of the list (sort/filter by most recent; match the timestamp). Open it.
5. Drill into the turns: see which agents handled it (`general_agent`, `product_agent`, `cart_agent`), which **models** were called, the **tool calls**, and the **token count** for *your* questions.

> [!TIP]
> This is the whole point of AI Observability — every real user conversation becomes debuggable telemetry. You just watched your own words turn into a traceable, costed, multi-agent flow.

## B. Insights — performance, cost & usage

1. Open the AI Observability **Analytics / Insights** view.
2. You'll see headline metrics: **Conversations**, **Avg Tokens / Conversation**, **Avg Calls / Conversation**, **Rated** and **Bad-Rated %**, plus an **AI analysis** summary (e.g. "token efficiency improved — lower avg tokens per conversation").
3. Filter by **Provider**, **Model**, or **Agent**. Which agent is busiest? Which model is most expensive per conversation?

## C. Conversations — debug down to the token

1. Back in **Conversations**, beyond your own, each row is a real shopping conversation — duration, **calls**, **tokens**, which **agents** and **models** were involved, and a **quality** rating.
2. Open one (e.g. an "…Telescope Recommendations" conversation). Drill into the turns: see every sub-agent hop, tool call, and token count. This is the "new primitive" — conversation data you can debug like a trace.

**Try:** find a conversation that used the most tokens or calls and figure out *why* (a multi-agent loop? a long tool chain?).

## D. Agents — system-prompt analysis

1. Open **Agents**.
2. AI Observability analyses each agent's **system prompt against real conversations** and flags weaknesses worth improving.
3. Pick an agent and read what it suggests. (This is exactly how the Grafana team tightens the Assistant's own prompts.)

## E. Evaluations — quality gates

1. Open **Evaluation**.
2. Online evals score agent responses continuously in production. Combined with Grafana Alerting, a drop in quality can page you — a full feedback loop for AI changes.

## F. Ask the Assistant about the agents

```
Which shopping agent has the highest token cost per conversation, and what's driving it?
```
```
Have any AI conversations been rated bad recently? Summarize the common themes.
```

## ✅ Checkpoint

You inspected a live agentic app the way you'd inspect any service — usage, cost, per-conversation detail, prompt quality, and evals. Observing AI *with* AI. Last stop: a prompt challenge.

Next: **[Module 8 — Assistant Challenge →](./08-assistant-challenge.md)**
