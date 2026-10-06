---
layout: default
title: AI-Powered GTM Engine
---

Three connected n8n workflows that research target accounts, score and route inbound leads, and draft outreach that a human approves before anything is sent. Built by Melissa Bradbury, a B2B SaaS demand generation and ABM leader with 20+ years in demand gen, ABM, marketing operations and BDR leadership.

[Connect on LinkedIn](https://www.linkedin.com/in/melissabradbury/) · [View the code](https://github.com/melissa-bradbury/ai-gtm-engine)

![How the three workflows connect](assets/gtm-engine-flow.svg)

## 1 · ABM Account Research Agent

Turns a list of target accounts into evidence-based account briefs, scored against the ICP, in about 1 minute each instead of an estimated 30–45 minutes of manual research.

<div style="position:relative;padding-bottom:56.25%;height:0;margin-bottom:1em;"><iframe src="https://www.loom.com/embed/e341022ddd9f47fa893e195b33cc0354" frameborder="0" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;"></iframe></div>

**[Read the case study](workflows/01-account-research/)**

## 2 · Inbound Lead Scoring and Routing

Scores every inbound lead on fit and intent, routes it by clear business rules, and alerts a BDR in Slack within [[FILL: seconds]] for hot leads, with target accounts promoted automatically.

<div style="position:relative;padding-bottom:56.25%;height:0;margin-bottom:1em;"><iframe src="https://www.loom.com/embed/LOOM-VIDEO-ID-2" frameborder="0" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;"></iframe></div>

**[Read the case study](workflows/02-lead-scoring-routing/)**

## 3 · Outreach Generator with Human Approval

Drafts a 3-touch sequence grounded in the account brief, emails it for one-click approval, and creates a Gmail draft only after a human says yes.

<div style="position:relative;padding-bottom:56.25%;height:0;margin-bottom:1em;"><iframe src="https://www.loom.com/embed/LOOM-VIDEO-ID-3" frameborder="0" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;"></iframe></div>

**[Read the case study](workflows/03-outreach-approval/)**

## The design principles

- **The model judges, the rules decide.** AI scores fit and intent; routing thresholds and overrides live in readable code that RevOps can audit and tune.
- **Evidence only.** Prompts restrict the model to the data it was given, label inferences, and report low confidence instead of inventing facts.
- **A human approves anything customer-facing.** Outreach becomes a draft only after approval, and every draft explains which details it used.
- **Structured output everywhere.** Fixed schemas make every AI result sortable, countable and safe to route on.

<small>The product being sold, Northwind Revenue Cloud, is fictional. Target accounts are real public companies; all contacts in the test data are invented.</small>
