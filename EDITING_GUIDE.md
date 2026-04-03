# Portfolio Editing Guide

> **Rule #1 — Never edit `index.html` for content.**  
> Edit `data.json` instead. Push to GitHub. The site updates in ~60 seconds.

---

## How the system works

```
data.json  ──────────────────────────────►  fetched by browser at page load
                                             ↓ renders all content dynamically

GitHub API (github.com/users/Srihh21/repos)  ──►  Projects section auto-synced
                                                    new repos appear automatically

Push any change to main  ──►  GitHub Pages rebuilds  ──►  live in ~60s
```

---

## Editing `data.json` — Field Reference

### `personal` — Contact & identity
Edit this to change your name, title, location, email, LinkedIn, phone, or GitHub username.

```json
"personal": {
  "name":              "Srihitha Reddy Betelly",   ← full name shown in hero
  "initials":          "SRB",                       ← nav logo
  "title":             "Senior Data Engineer",      ← subtitle in hero
  "location":          "Chicago, Illinois",
  "email":             "rsrihitha248@gmail.com",    ← contact section + mailto link
  "phone":             "+1 (508) 542-5641",
  "linkedin_url":      "https://www.linkedin.com/in/srihitha-reddy21/",
  "linkedin_label":    "Srihtha Reddy",  ← display text
  "github_username":   "Srihh21",                  ← used for GitHub API project sync
  "available":         true,                        ← shows/hides the "Available" badge
  "availability_text": "Available for new opportunities"
}
```

---

### `summary` — Hero paragraph
One sentence describing you. Shown below your name in the hero section.

---

### `stats` — Hero metrics row
Four numbers shown prominently in the hero. Change value or label freely.

```json
"stats": [
  { "value": "5+",    "label": "Years Exp."  },
  { "value": "12M+",  "label": "Records/Day" }
]
```

---

### `highlights` — Impact cards
Cards shown in the "What I Deliver" section. Add, remove, or edit freely.

```json
"highlights": [
  { "icon": "⚡", "value": "40%", "label": "Faster pipeline runtimes via dbt" }
]
```

---

### `experience` — Work history
Add a new job, change titles, update bullets — all here.

```json
"experience": [
  {
    "title":    "Senior Data Engineer",
    "company":  "ZS",
    "period":   "Nov 2024 – Present",
    "location": "Chicago, Illinois",
    "bullets": [
      "First bullet point.",
      "Second bullet point."
    ]
  }
]
```

**To add a new role:** copy one block, paste it at the top of the array (most recent first), and fill in the details.  
**To update responsibilities:** edit the `bullets` array. Add or remove items freely.

---

### `skills` — Tech stack categories
Each block is one card on the Skills section.

```json
"skills": [
  {
    "category": "Languages",
    "icon":     "🐍",
    "tags":     ["Python", "SQL"]
  }
]
```

**To add a new skill tag:** append it to the relevant `tags` array.  
**To add a new category:** add a new object to the `skills` array.

---

### `education` — Academic history

```json
"education": [
  {
    "icon":     "🎓",
    "degree":   "Master of Science",
    "field":    "Computers and Information Sciences",
    "school":   "University of Massachusetts, Dartmouth",
    "period":   "Jan 2022 – Aug 2023",
    "location": "North Dartmouth, MA"
  }
]
```

---

### `projects` — GitHub project configuration

#### `exclude_repos`
Repos to hide from the Projects section (e.g. the portfolio repo itself).

```json
"exclude_repos": ["Srihh21.github.io"]
```

#### `repo_overrides`
Extra metadata for specific repos. The key is the **exact GitHub repo name**.

```json
"repo_overrides": {
  "my-new-project": {
    "icon":               "🚀",           ← emoji shown in card header
    "pinned":             true,            ← pin to top of projects grid
    "pin_order":          1,              ← lower = higher (1 is first)
    "status":             "active",       ← "active" | "wip"
    "custom_description": "A short description shown on the card.",
    "highlights": [                        ← bullet points on the card
      "Key feature one",
      "Key feature two"
    ],
    "architecture": ["Kafka","Spark","S3"], ← pipeline flow diagram
    "tech_tags":    ["Python","Docker"]    ← tech stack tags on card
  }
}
```

**If a repo has no override entry:** it still appears automatically on the site using its GitHub description, language, stars, and forks. You only need an override if you want richer card content.

---

## Auto-trigger from project repos

When you push to a project repo (e.g. `fraud-detection-system`), the portfolio already shows the update automatically because it fetches the GitHub API live on every page load. But if you also want the GitHub Pages cache to refresh immediately, you can add this one-time setup:

### Step 1 — Create a fine-grained Personal Access Token
Go to **GitHub → Settings → Developer settings → Personal access tokens → Fine-grained tokens** and create a token with:
- Repository access: `Srihh21.github.io` only
- Permissions: **Actions** → Read and write

### Step 2 — Add the token as a secret in each project repo
In each project repo go to **Settings → Secrets and variables → Actions → New repository secret**:
- Name: `PORTFOLIO_TOKEN`
- Value: the token from Step 1

### Step 3 — Add this workflow to each project repo
Create `.github/workflows/notify-portfolio.yml`:

```yaml
name: Notify Portfolio

on:
  push:
    branches: [main]
  release:
    types: [published]

jobs:
  notify:
    runs-on: ubuntu-latest
    steps:
      - name: Trigger portfolio rebuild
        uses: peter-evans/repository-dispatch@v3
        with:
          token: ${{ secrets.PORTFOLIO_TOKEN }}
          repository: Srihh21/Srihh21.github.io
          event-type: project-updated
          client-payload: '{"repo":"${{ github.repository }}","ref":"${{ github.ref }}"}'
```

Once set up, any push to that project repo will also trigger a portfolio rebuild within seconds.

---

## Quick-reference: common edits

| What you want to change | Where to edit |
|---|---|
| Email / phone / LinkedIn | `personal` section in `data.json` |
| "Available for opportunities" badge | `personal.available` (true/false) |
| Hero summary paragraph | `summary` field |
| Metrics (5+, 12M+, etc.) | `stats` array |
| Impact cards | `highlights` array |
| Job title or company | `experience[n].title` / `.company` |
| Role responsibilities | `experience[n].bullets` array |
| Add a new job | Add object to top of `experience` array |
| Add/remove a skill tag | `skills[n].tags` array |
| Add a skill category | Add object to `skills` array |
| Show/hide a GitHub repo | `projects.exclude_repos` |
| Customize a project card | `projects.repo_overrides["repo-name"]` |
| Pin a project to the top | `repo_overrides.pinned: true` + `pin_order` |
| Mark a project as "In Progress" | `repo_overrides.status: "wip"` |

---

## Deploying changes

```bash
# 1. Edit data.json locally
# 2. Commit and push
git add data.json
git commit -m "Update experience at ZS"
git push origin main

# GitHub Pages rebuilds automatically — live in ~60 seconds
```

---

*Questions? Open an issue on [github.com/Srihh21/Srihh21.github.io](https://github.com/Srihh21/Srihh21.github.io)*
