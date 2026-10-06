# Publishing checklist

This file is excluded from the website. Delete it from the repo once you're done.

## 1. Fill in the placeholders

Search the whole folder for `[[FILL` and replace each one with a real number from your runs. Also replace:

- `YOUR-USERNAME` with your GitHub username (README.md and index.md)
- `YOUR-PROFILE` with your LinkedIn profile handle (README.md and index.md)
- `LOOM-VIDEO-ID-1`, `-2`, `-3` with your Loom video IDs. A Loom share link looks like `https://www.loom.com/share/abc123`; the ID is `abc123`. Each ID appears in index.md and in that workflow's README.

## 2. Add your files

Each workflow folder expects these files. Use these exact names, or update the image links in that README.

| Folder | Files |
| --- | --- |
| workflows/01-account-research | workflow.json · screenshots/canvas.png · screenshots/brief-row.png · screenshots/slack-post.png |
| workflows/02-lead-scoring-routing | workflow.json · screenshots/canvas.png · screenshots/form.png · screenshots/slack-alert.png · screenshots/lead-log.png |
| workflows/03-outreach-approval | workflow.json · screenshots/canvas.png · screenshots/approval-email.png · screenshots/gmail-draft.png |

Before adding each `workflow.json`, open it in a text editor and search for your email address, Google Sheet ID, Slack channel IDs and webhook URLs. Credentials themselves are never included in an n8n export, but those identifiers can be.

## 3. Create the repo

1. On github.com, click New repository. Name it `ai-gtm-engine` and set it to Public.
2. On the empty repo page, click "uploading an existing file", then drag in everything inside this folder (not the folder itself). Commit.

## 4. Turn on the website

1. Repo Settings → Pages.
2. Under Build and deployment, choose Deploy from a branch, branch `main`, folder `/ (root)`. Save.
3. After a minute or two the site is live at `https://melissa-bradbury.github.io/ai-gtm-engine/`.

## 5. Check it

- Open the site and each case study, and confirm every video plays and every screenshot loads.
- Open the repo view too. Loom players don't show inside GitHub's own file view, which is expected; the "Watch on Loom" link covers that.
- Add the site link to your LinkedIn Featured section and your resume.
