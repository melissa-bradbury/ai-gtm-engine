# ABM Account Research Agent

[← All workflows](../../)

Turns a list of target accounts into evidence-based account briefs, scored against the ICP, saved for the sales team and posted to Slack.

## Watch the demo

<div style="position:relative;padding-bottom:56.25%;height:0;margin-bottom:1em;"><iframe src="https://www.loom.com/embed/e341022ddd9f47fa893e195b33cc0354" frameborder="0" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;"></iframe></div>

[Watch on Loom](https://www.loom.com/share/e341022ddd9f47fa893e195b33cc0354)

## The problem

Account-based outbound lives or dies on relevance, and relevance takes research. Reading a company's website, scanning recent news and mapping the buying committee takes a rep an estimated 30–45 minutes per account. Most teams either skip it and send generic outreach, or do it inconsistently, so the quality of a first touch depends on which rep picked up the account.

## What I built

An agent that researches every account marked "New" in a target account list and writes a structured brief a BDR can act on immediately.

| Phase | What happens |
| --- | --- |
| 1 · Intake | Reads new accounts from the target list and processes them one at a time |
| 2 · Evidence gathering | Fetches the company's homepage and recent news headlines, then assembles one research packet |
| 3 · Brief generation | One AI call judges ICP fit and writes priorities, pain points, buying committee, messaging angles and reasons to reach out now, in a fixed structure |
| 4 · Store and notify | Saves the brief to a shared sheet, marks the account researched, and posts a summary to Slack |

## Design decisions

- **The model only sees evidence.** The prompt restricts the AI to the research packet and well-known facts. Anything inferred must start with "Likely:", so a rep can tell facts from educated guesses at a glance.
- **Honest confidence beats confident fiction.** When a website blocks the request or news is thin, the brief comes back rated low confidence instead of padded with invented detail.
- **Fit is a fixed vocabulary.** ICP fit is always strong, moderate or weak, so briefs can be sorted, counted, and used by the lead scoring workflow without interpretation.
- **One account at a time.** A slow or blocked website can't hold up the rest of the run, and the execution log reads account by account.

## Results

| Metric | Result |
| --- | --- |
| Time per account brief | ~1 minute vs. an estimated 30–45 minutes manually |
| Accounts researched per run | 5 in the demo |
| AI cost per brief | under one cent |
| Briefs rated low confidence | 0 of 6 blocked automated requests |

## Screenshots

![The workflow in n8n](screenshots/canvas.png)

![A finished account brief in Google Sheets](screenshots/brief-row.png)

![The Slack summary a BDR sees](screenshots/slack-post.png)

## Under the hood

**Nodes:** Manual Trigger · Google Sheets · Loop Over Items · HTTP Request (website and Google News RSS) · HTML extraction · Code (research packet) · Basic LLM Chain with OpenAI gpt-5-mini and a Structured Output Parser · Edit Fields · Google Sheets · Slack

<details>
<summary>System prompt</summary>

<pre>
You are a senior ABM strategist preparing an account brief for a B2B sales team.

[ICP BLOCK: see SETUP.md]

You will receive a research packet about one company: its website text and recent news headlines. Write a brief that helps a BDR and an account-based marketer decide whether and how to engage this account.

Rules:
1. Use only the evidence in the packet plus widely known facts about the company. Never invent numbers, names, funding rounds or events.
2. When a point is an inference rather than a stated fact, start it with "Likely:".
3. Judge ICP fit against the ICP above as strong, moderate or weak. Explain why in one or two sentences that cite specific evidence.
4. Priorities and pain points must connect to what the product solves: rep ramp, messaging consistency, win rates, enablement ROI. Skip anything that would be true of every company.
5. Buying committee: the 3 to 4 roles most likely involved, and what each one would care about.
6. Messaging angles: 3 specific hooks a rep could open with, each tied to a priority, a pain point or a recent trigger.
7. Recent triggers: news that creates a reason to reach out now. Return an empty list if there are none.
8. Confidence: high if the packet had rich website text and relevant news; medium if one source was thin; low if most of the packet was "unavailable".

Return ONLY valid JSON.
</pre>

</details>

## Files

- Test data and sheet structure: see [SETUP.md](../../SETUP.md).
