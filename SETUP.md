# Setup

Everything you need to run the three workflows in your own n8n instance.

## Requirements

| Credential | Used by | Notes |
| --- | --- | --- |
| OpenAI API | All three | Model `gpt-5-mini`. A full run of all three on the test data costs well under $1. |
| Google Sheets OAuth2 | All three | One Google account. |
| Gmail OAuth2 | Workflow 3 | Same Google account; used for the approval email and drafts. |
| Slack | Workflows 1 and 2 | Channels `#abm-research` and `#hot-leads`. Swap for Gmail Send nodes if you don't use Slack. |

Use an n8n instance reachable from the internet (n8n Cloud or a hosted server). The public lead form and the Gmail approval buttons don't work on a laptop-only install.

## The Google Sheet

Create one sheet called **GTM Engine** with four tabs, or upload [`data/GTM_Engine.xlsx`](data/GTM_Engine.xlsx) to Google Drive and open it with Google Sheets. Column names in row 1 must match exactly.

| Tab | Columns |
| --- | --- |
| Target Accounts | company_name, domain, industry, employee_range, status, researched_at |
| Account Briefs | domain, company_name, icp_fit, icp_fit_reason, company_summary, priorities, pain_points, buying_committee, messaging_angles, recent_triggers, confidence, researched_at |
| Mock Leads | first_name, last_name, email, company, job_title, company_size, need, timeline |
| Lead Log | lead_id, submitted_at, first_name, last_name, email, company, job_title, company_size, timeline, need, email_domain, is_target_account, fit_score, intent_score, total_score, tier, reasoning, key_signals, next_step, talking_points, alerted_at, outreach_status, touch_1_subject, touch_1_body, touch_2_subject, touch_2_body, touch_3_subject, touch_3_body, linkedin_note, reviewed_at |

Test data for Target Accounts and Mock Leads is in [`data/`](data/).

## The ICP block

Every prompt sells the same fictional product. Paste this wherever a prompt says `[ICP BLOCK]`, or replace it with your own product and ICP.

<pre>
COMPANY AND ICP
Northwind Revenue Cloud (fictional) is a revenue enablement platform that helps B2B sales teams ramp new reps faster, keep messaging consistent, and tie enablement to deal outcomes.

Ideal customer: B2B SaaS or technology company, 200 to 5,000 employees, North American headquarters or a major North American sales team, 25+ quota-carrying reps, growing its sales team or recently funded, runs Salesforce or HubSpot.

Buying committee: CRO or VP Sales (economic buyer); VP or Director of Revenue Operations; Director of Sales Enablement; VP Marketing or Demand Generation (influencer).

Common pains: new-rep ramp longer than 5 months; inconsistent messaging across reps; falling win rates; enablement content nobody uses; no way to prove enablement ROI.

Not a fit: companies under 50 employees; consumer, local-services or healthcare-practice businesses; students; job seekers; competitors (sales enablement vendors).
</pre>


