```markdown
# Nijjara ERP Final Nov (Apps Script bound to Google Sheet)

This repo mirrors the Apps Script project bound to the Google Sheet `Nijjara_ERP_Final_Nov`.

Important IDs:
- Script ID: 1mDMZv5RgyECio9Sl7AJP6IuKI09hyJWBaYSyGD_P3n-kEXa7QRT32Oen
- Google Sheet ID: 1Ga1S_mAcinUS-Tg07yS4KgDD3WkBuZC0PKrlPwDtWTM
- GCP Project Number: 1097031500425
- Owner account: nijjaraerp@gmail.com

Prerequisites (local)
- Node.js + npm
- clasp CLI: `npm install -g @google/clasp`
- git
- (optional) GitHub CLI `gh` if you want to create the repo from CLI

Local one-time setup and initial import (recommended)
1. Login to clasp (authorizes your Google account):
   - `clasp login`
   - This opens a browser and creates `~/.clasprc.json` (DO NOT COMMIT that file).

2. Clone the container-bound project locally:
   - mkdir project && cd project
   - `clasp clone 1mDMZv5RgyECio9Sl7AJP6IuKI09hyJWBaYSyGD_P3n-kEXa7QRT32Oen`
   - This will download your `.gs`, `.html`, and `appsscript.json` files and create `.clasp.json` (already present in this repo).

3. Initialize git and push to a new GitHub repo:
   - `git init`
   - `git add .`
   - `git commit -m "Import Apps Script project"`
   - Create repo on GitHub:
     - Using UI: create a new repo named e.g. `Nijjara-ERP-Final-Nov` under your account `nijjaraerp`
     - Or using gh CLI:
       `gh repo create nijjaraerp/Nijjara-ERP-Final-Nov --public --source=. --push`
     - Or add remote and push:
       `git remote add origin https://github.com/nijjaraerp/Nijjara-ERP-Final-Nov.git`
       `git branch -M main`
       `git push -u origin main`

Typical local workflow after initial setup
- Before editing locally, pull any remote Apps Script changes:
  `clasp pull`
  then commit & push to GitHub:
  `git add . && git commit -m "sync from apps script" && git push`

- To push your local changes to the Apps Script project:
  `clasp push`
  then test in the Apps Script editor or the bound sheet.

Optional: CI deploy from GitHub Actions (auto-deploy on push)
- Add a repository secret named `CLASP_CREDENTIALS` whose value is the full JSON contents of your local `~/.clasprc.json` (created after `clasp login`).
  - In repo: Settings → Secrets and variables → Actions → New repository secret
  - Name: `CLASP_CREDENTIALS`
  - Value: paste entire `~/.clasprc.json`

- The included workflow `.github/workflows/deploy.yml` will restore that file and run `clasp push` on pushes to branch `main`.

Security notes
- `~/.clasprc.json` contains refresh tokens — treat it as highly sensitive.
- Do NOT commit `.clasprc.json` into the repo (it's in .gitignore).
- Prefer limiting who can push to main (protect branch, require PR reviews) if using automatic deploy.

If you want, I can:
- Create the GitHub repo for you and push these files (I can prepare the commit details if you want me to run that action).
- Or generate the exact `~/.github/workflows/deploy.yml` file contents (below) ready to commit.  