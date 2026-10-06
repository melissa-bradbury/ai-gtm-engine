# Inbound Lead Scoring and Routing

[← All workflows](../../)

Scores every inbound lead on fit and intent, routes it by clear business rules, alerts a BDR in Slack for hot leads, and logs every decision with timestamps.

## Watch the demo

<div style="position:relative;padding-bottom:56.25%;height:0;margin-bottom:1em;"><iframe src="https://www.loom.com/embed/LOOM-VIDEO-ID-2" frameborder="0" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;"></iframe></div>

[Watch on Loom](https://www.loom.com/share/LOOM-VIDEO-ID-2)

## The problem

Inbound leads are the most expensive leads a marketing team produces, and they decay fast. In many teams a hand-raiser from a target account sits in a queue for hours while reps work through whatever came in first. Traditional point-based scoring doesn't help much: it can't read "we're hiring 20 AEs and need to cut ramp time in half" and recognize urgency.

## What I built

A lead pipeline with a public form at the front, an AI judgment layer in the middle, and deterministic routing at the end.

| Phase | What happens |
| --- | --- |
| 1 · Capture | A public n8n form (plus a test path that runs mock leads from a sheet) normalizes every lead into one shape |
| 2 · Enrich | Flags free email domains and checks whether the lead's company already has an account brief from the research agent |
| 3 · Score | AI scores fit and intent separately, 0–100, with reasoning and BDR talking points; a short code block applies the routing rules |
| 4 · Route and log | Hot leads trigger an instant Slack alert; every lead is logged with tier, reasoning and timestamps |

## Design decisions

- **The model judges, the rules decide.** AI is good at reading intent from free text. It shouldn't own routing policy. Weights, thresholds and overrides live in eight readable lines of code that a CMO and CRO can agree on in a lead-management SLA, and change in a meeting.
- **Two scores, not one.** Fit and intent are separate questions. A student with an urgent-sounding need has high intent and no fit; a CRO downloading a report has high fit and low intent. Separating them makes every routing decision explainable in one line.
- **Business overrides are explicit.** Target accounts never wait in the warm queue. Free email addresses can't be marked hot without a human check. Competitors are always disqualified.
- **No lead disappears.** Account lookups are done in a way that can't silently drop a lead when its company has no brief, a common failure in lookup-based automations.

## Results

| Metric | Result |
| --- | --- |
| Form submission to BDR Slack alert | ~8 seconds |
| Test leads correctly tiered | 10 of 10 |
| Tier mix across 10 test leads | [[FILL: e.g. 4 hot · 2 warm or nurture · 4 disqualified]] |
| Competitor and student leads | [[FILL: disqualified automatically]] |

## Screenshots

![The workflow in n8n](screenshots/canvas.png)

![The lead form](screenshots/form.png)

![A hot-lead alert in Slack](screenshots/slack-alert.png)

![The Lead Log with tiers and reasoning](screenshots/lead-log.png)

## Under the hood

**Nodes:** n8n Form Trigger · Manual Trigger and Google Sheets (test path) · Edit Fields · Code (lead prep, account context, routing rules) · Google Sheets · Basic LLM Chain with OpenAI gpt-5-mini and a Structured Output Parser · Switch · Slack · Google Sheets

<details>
<summary>Routing rules</summary>

<pre>
total = fit x 0.6 + intent x 0.4

competitor, or fit below 20   -> disqualify
total 75 or higher            -> hot
total 55 to 74                -> warm
anything else                 -> nurture

Overrides:
target account and warm       -> hot
free email address and hot    -> warm

SLA by tier: hot = BDR call within 1 hour; warm = follow-up within 24 hours;
nurture = nurture sequence; disqualify = no sales follow-up
</pre>

</details>

## Files

- `workflow.json`: import into n8n via Workflows → Import from File. You'll need your own OpenAI, Google Sheets and Slack credentials.
- Test data and sheet structure: see [SETUP.md](../../SETUP.md).
