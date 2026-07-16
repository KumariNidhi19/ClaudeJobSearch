# Automated Daily Job Search (Claude Cowork)

A hands-off job hunt powered by **Claude Cowork** — no code, no API key. You set
up one daily scheduled task; every morning Claude reads your profile, resume, and
preferences, searches the web for fresh matching roles, applies your work-schedule
rules, skips duplicates, and updates `application-tracker.md` with the new matches.

**Target:** up to **20 new roles/day**, all locations (Pune preferred), each with
a direct job link and the company's careers page.

## How it works

```
Cowork scheduled task (runs daily, in the cloud, laptop can be closed)
        │  reads →  profile.md · resume.md · job-preferences.md
        ▼
   web search  →  LinkedIn / Naukri / Indeed / Wellfound / Instahyre / Cutshort
                  / Hirist / YC + careers pages of prominent product companies
        ▼
   applies your strict schedule rules + skips anything already in the tracker
        ▼
   appends new matches to application-tracker.md  →  2-line summary to you
```

## Files in this repo

| File | Purpose |
|---|---|
| `profile.md` | Structured profile Claude uses to judge fit. **Most important.** |
| `resume.md` | Full resume in markdown (contact details redacted for public repo). |
| `job-preferences.md` | Your hard rules — roles, location, strict schedule priority. |
| `prompts.md` | The daily task prompt + an on-demand cover-note prompt. |
| `cowork-setup.md` | Copy-paste global instructions + the scheduled-task prompt. |
| `application-tracker.md` | Auto-updated match table; your pipeline lives here too. |

## ⚠️ Public repo = privacy

This is a **public** repo, so anything committed is visible to the whole world
and scraped by bots.
- **Contact details are redacted** from `profile.md` and `resume.md`. Keep your
  real email/phone in a private note or in Cowork's account memory — never commit
  them here.
- If you'd rather not publish your resume and job hunt at all, make the repo
  **private** instead; everything below still works.

## Your schedule priority (enforced every run)

1. **Hybrid, 2–3 office days/week** — highest priority.
2. **Standard 5-day week** — onsite, hybrid, or remote.
3. **6-day / alternate-Saturday** — rejected, *unless* the employer is BCG,
   JPMorgan Chase, PwC, Deloitte, Capgemini, or comparable global-tier.

Unstated schedules are included but flagged for you to verify.

## Setup (about 10 minutes)

**Prereqs:** a paid Claude plan (Pro, Max, Team, or Enterprise) and the Claude
Desktop app, up to date. Scheduled tasks are in Cowork under "Scheduled".

1. **Push these files to your GitHub repo.**
   ```bash
   git init && git add . && git commit -m "job search files"
   git branch -M main
   git remote add origin https://github.com/<you>/<repo>.git
   git push -u origin main
   ```
2. **Give Cowork the files.** Pick ONE:
   - **GitHub connector (recommended for a repo):** connect GitHub in Cowork so
     the cloud task can read these files and commit the updated tracker back to
     the repo. In the task, refer to "my <repo> GitHub repo."
   - **Cowork Project:** create a Project called *Job Search*, upload the six
     `.md` files into it, and run the task inside that project. (Cloud scheduled
     tasks read files from your Claude account/projects, not a local folder.)
3. **Set global instructions.** Settings → Cowork → Global instructions → Edit →
   paste section 1 of `cowork-setup.md`.
4. **Create the daily task.** Open a new Cowork task, type `/schedule`, paste the
   prompt from section 2 of `cowork-setup.md`, choose **Daily** at your preferred
   time, and confirm.
5. **Test it now.** From the Scheduled page, run the task once on demand. Check
   the summary and the new rows in `application-tracker.md`.

After the first run, Claude may rewrite the task prompt slightly based on what it
learned — that's expected and makes later runs sharper.

## Cost & usage

No API billing. Cowork runs draw on your subscription's usage allowance, and
agentic tasks use more than plain chat. If you hit limits, run the search on
weekdays only, or narrow it to fewer job boards. Monitor in Settings → Usage.

## Getting good matches (and honest limits)

- **Quality follows your inputs.** Fill the optional fields in `profile.md`
  (expected CTC, notice period) and `job-preferences.md`. Specific in, specific out.
- **Web search sees the public web, not private job-board APIs.** LinkedIn and
  Naukri are heavily anti-bot, so not every live listing is indexed and results
  vary day to day. Treat the tracker as a strong lead list — always open the link
  and confirm the role is open and the schedule before applying.
- **Schedule is often unstated;** those come back flagged `unknown`. Verify on the
  company site or in a recruiter call.
- **Tune the prompt** in `prompts.md` / `cowork-setup.md` to add boards, change the
  recency window, or tighten seniority.

## Handy extras

- **Cover notes:** paste the `COVER_NOTE` prompt from `prompts.md` into any Cowork
  chat with a role, and Claude drafts a tailored note using your real wins.
- **Weekly digest:** add a second scheduled task ("summarize this week's Inbox
  rows into a shortlist") for a Friday review.
- **Mobile:** you can review results and kick off runs from the Claude mobile app.
