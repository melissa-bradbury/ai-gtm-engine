# Outreach Generator with Human Approval

[← All workflows](../../)

Drafts a 3-touch email sequence and a LinkedIn note for every hot lead, grounded in the lead's own words and the account brief, then waits for a human to approve before creating a Gmail draft.

## Watch the demo

<div style="position:relative;padding-bottom:56.25%;height:0;margin-bottom:1em;"><iframe src="https://www.loom.com/embed/LOOM-VIDEO-ID-3" frameborder="0" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;"></iframe></div>

[Watch on Loom](https://www.loom.com/share/LOOM-VIDEO-ID-3)

## The problem

AI can write outreach in seconds, but most teams end up with one of two bad outcomes: generic AI emails that hurt the brand, or AI drafts nobody trusts, so reps rewrite them from scratch. The missing piece is a fast, accountable review step.

## What I built

An outreach drafter with a human approval gate built into the workflow itself.

| Phase | What happens |
| --- | --- |
| 1 · Queue and context | Picks up hot leads marked pending by the scoring workflow and attaches each one's account brief |
| 2 · Draft | One AI call writes three emails and a LinkedIn note, plus a short note explaining which details it used |
| 3 · Review | Emails the full sequence to a reviewer with Approve and Reject buttons, and pauses until they click |
| 4 · Act and record | Approved: creates a Gmail draft to the lead and saves the sequence. Rejected: logs it. Then moves to the next lead. |

## Design decisions

- **Nothing sends itself.** Approval creates a draft, not a sent email, so the rep stays in control of timing and can add a personal line.
- **The AI shows its work.** Every sequence includes one line per email saying which detail it used and why. Reviewers check those three lines instead of rereading every email for invented facts, which makes review fast enough that people actually do it.
- **Grounded, not generic.** The prompt allows only facts from the lead's form and the account brief, bans filler openers, and caps each email at 110 words with one call to action.
- **Every click is a metric.** Approval rate without edits is tracked per run, showing whether the prompts are earning trust over time.

## Results

| Metric | Result |
| --- | --- |
| Drafts approved without edits | [[FILL: e.g. 3 of 4]] |
| Time from approval click to Gmail draft | [[FILL: e.g. ~2 seconds]] |
| Average words per email | [[FILL: e.g. 85]] |
| Invented facts found in review | [[FILL: e.g. 0]] |

## Screenshots

![The workflow in n8n](screenshots/canvas.png)

![The approval email](screenshots/approval-email.png)

![The resulting Gmail draft](screenshots/gmail-draft.png)

## Under the hood

**Nodes:** Manual Trigger · Google Sheets · Code (account context) · Loop Over Items · Basic LLM Chain with OpenAI gpt-5-mini and a Structured Output Parser · Gmail (send and wait for approval) · IF · Gmail (create draft) · Google Sheets

<details>
<summary>Writing rules from the system prompt</summary>

<pre>
Sequence plan:
- Touch 1 (day 0): respond to what they told us, name their problem in their own terms, ask for 20 minutes.
- Touch 2 (day 3): add value with one specific idea tied to their priorities or an account trigger.
- Touch 3 (day 7): a short, polite close-the-loop note that makes "not now" easy to say.

Rules:
1. Each email body under 110 words; subject lines under 7 words, no clickbait.
2. Exactly one call to action per email.
3. Use only facts from the lead and the account context. Never invent statistics, customer names or events.
4. No filler openers.
5. Plain text, written like a person.
6. LinkedIn note under 280 characters, no pitch.
7. personalization_notes: one line per touch saying which detail was used and why.
</pre>

</details>

## Files

 Test data and sheet structure: see [SETUP.md](../../SETUP.md).
