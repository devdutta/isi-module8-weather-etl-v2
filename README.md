# Weather ETL Agent — V2 (Debate Round) — ISI Module 10

This repository contains the **Weather ETL Agent V2** workflow for the ISI course
*Applied Agentic AI for Modern Data Engineering* — **Module 10: AgenticOps for Lifecycle Management of Autonomous AI Agents**.

> **⚠️ V2 is optional.** It is **NOT required** for the Module 10 Assignment or Quiz — both are based entirely on **V1**. V2 is shared purely for **advanced learning**, for students who want to see how a multi-LLM debate pattern works and how observability scales with a more complex pipeline.

---

## What's in this repo

| File | Description |
|------|-------------|
| `Weather_ETL_Agent_V2.yml` | The Dify workflow DSL file for Weather ETL Agent V2. Import this into Dify Cloud. |

---

## What's different in V2

V2 is V1 plus a **Round 2 debate round**. After the first Analyst → Reviewer pass, the workflow runs a second exchange before generating the report:

```
... Weather Analyst → Quality Reviewer → Analyst R2 → Reviewer R2 → Report Generator → Output
```

- **Analyst R2** — the Weather Analyst responds to the Reviewer's critique, defending or revising its analysis.
- **Reviewer R2** — the Quality Reviewer reads the Analyst's rebuttal and produces a final assessment.
- The **Report Generator** then synthesises the *full debate* (both rounds) into the final report — so disagreements that survived two rounds are surfaced explicitly.

In a LangFuse trace this shows up as **extra GENERATION spans** (Analyst R2, Reviewer R2) and a longer trace tree than V1.

---

## 1. Import V2 into Dify

1. Download `Weather_ETL_Agent_V2.yml` from this repo (use the **Download raw file** button on GitHub, or clone the repo).
2. Open **Dify Cloud** (`https://cloud.dify.ai`) and go to **Studio**.
3. Click **Import DSL file**.
4. On the **Local File** tab, select the `Weather_ETL_Agent_V2.yml` you downloaded, then click **Create**.
   - *(Alternative — "From URL" tab: paste the raw GitHub URL of `Weather_ETL_Agent_V2.yml` and click **Create**.)*
5. Dify creates a new app with the full V2 workflow. If you see a DSL-version warning, it's safe to proceed — Dify Cloud always runs the latest version.
6. Open the new app in the workflow editor and walk through the nodes — look for **Analyst R2** and **Reviewer R2** to see the debate round.

> The V2 workflow uses the same model and the same external weather API (wttr.in) as V1. No new credentials are needed for the workflow itself.

---

## 2. (Optional) Trace V2 in LangFuse

You can observe V2 in LangFuse exactly the way you did for V1 in the Module 10 assignment:

1. In your new V2 app in Dify, go to **Monitoring** → next to **Langfuse**, click **Config**.
2. Paste your **Secret Key** (`sk-lf-...`), **Public Key** (`pk-lf-...`), and **Host** URL (`https://us.cloud.langfuse.com` for US, `https://cloud.langfuse.com` for EU) — the same LangFuse project keys from the assignment are fine, or create a fresh project.
3. Click **Save & Enable** — the status should show **IN SERVICE** (green dot).
4. **Publish** the V2 workflow, then **Run App** → enter the cities and report type → **Execute**.
5. Open LangFuse, go to your project → **Tracing**, filter **Is Root Observation → uncheck False**, and open the most recent trace.
6. In the trace tree you'll now see the **Analyst R2** and **Reviewer R2** GENERATION spans in addition to the V1 nodes — compare token counts and latency against your V1 trace.

(Full LangFuse + Dify setup details are in the Module 10 Assignment, Part A.)

---

## Notes

- DSL format: Dify `version: 0.6.0`, `kind: app`.
- This is teaching material for ISI Kolkata. Use freely for learning.
- Questions: raise them on the Module 10 discussion forum on the learning platform.
