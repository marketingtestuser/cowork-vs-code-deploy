# Project Handoff — cowork-vs-code-deploy

**Last updated:** 2026-06-15

This document captures everything set up for the "Claude Code vs. Claude Cowork —
Operator's Field Guide" page: what it is, where it lives, how it's hosted, and
how to edit and deploy it going forward.

---

## 1. What this is

A single-page static site — a long-form guide titled *"Claude Code vs. Claude
Cowork — Operator's Field Guide"* (author: Jonathan Moss). It was originally
captured as a snapshot from a live Vercel deployment and is now owned, version-
controlled, and self-hosted.

---

## 2. The setup at a glance

```
Edit in GitHub ──push to main──▶ GitHub repo (source of truth) ──auto-deploy──▶ Vercel (live hosting)
```

- **GitHub** is the editing area / source of truth.
- Every push to `main` automatically triggers a fresh **Vercel** production deploy.
- No manual deploy step is needed.

---

## 3. Key resources

| Resource | URL |
|---|---|
| GitHub repository (editing area) | https://github.com/marketingtestuser/cowork-vs-code-deploy |
| Live site (Vercel, public) | https://cowork-vs-code-deploy-b2-b-fusion.vercel.app |
| Vercel project dashboard | https://vercel.com/b2-b-fusion/cowork-vs-code-deploy |
| Original source page (snapshot origin) | https://cowork-vs-code-deploy.vercel.app/ |

**Accounts involved**
- GitHub account: `marketingtestuser`
- Vercel account: `jonrusso-7536`, under team **b2-b-fusion**
- Local clone path: `/Users/davidherring/Downloads/cowork-vs-code-deploy`

---

## 4. Repository contents

| File | Purpose |
|---|---|
| `index.html` | The full page — self-contained, all CSS inline |
| `abn-logo-dark.png` | The only local image asset |
| `README.md` | Short project description + local-view instructions |
| `HANDOFF.md` | This document |

> The page also loads the **Inter** and **JetBrains Mono** fonts from the Google
> Fonts CDN at runtime; those are not vendored in the repo.

---

## 5. How to edit and deploy

**Option A — edit in the GitHub web UI (simplest)**
1. Open the repo, click `index.html`, click the pencil (✏️) icon.
2. Make changes, commit to `main`.
3. Vercel auto-deploys within ~seconds. Watch it in the Vercel **Deployments** tab.

**Option B — edit locally**
```bash
cd /Users/davidherring/Downloads/cowork-vs-code-deploy
# ...edit index.html...
git add -A
git commit -m "your message"
git push origin main      # triggers Vercel auto-deploy
```

**Preview locally before pushing**
```bash
python3 -m http.server 8000
# visit http://localhost:8000
```

---

## 6. What was accomplished (chronological)

1. **Captured** the live page (`index.html` + `abn-logo-dark.png`) from
   `cowork-vs-code-deploy.vercel.app` into a local folder.
2. **Created** a private GitHub repo `marketingtestuser/cowork-vs-code-deploy`,
   committed the snapshot + a README, and pushed it.
3. **Made the repo public** (per request).
4. Briefly enabled **GitHub Pages** for hosting, then **disabled it** once Vercel
   was set up — to avoid two live copies. (Repo and code were left intact.)
5. **Set up Vercel hosting:**
   - Installed the Vercel CLI, logged in (account `jonrusso-7536`, team
     `b2-b-fusion`).
   - Linked and deployed the project.
   - Disabled Vercel's default "login required" deployment protection so the page
     is publicly viewable.
6. **Connected the GitHub repo to Vercel** (via the Vercel dashboard → Settings →
   Git) so pushes auto-deploy.
7. **Verified end-to-end:** a test push to `main` triggered an automatic Vercel
   production deploy successfully.

---

## 7. Environment / tooling notes (for this machine)

- `gh` (GitHub CLI) was installed to `~/.local/bin/gh` (not on the default PATH).
- `vercel` (Vercel CLI) was installed to `~/.local/bin/vercel`.
- To use either in a new terminal, prefix or add to PATH:
  ```bash
  export PATH="$HOME/.local/bin:$PATH"
  ```
- Git was configured to use `gh` as its credential helper, so `git push` from the
  local clone works without prompting for a username/password.

---

## 8. Not done / future options

- **Custom domain** — intentionally skipped for now. To add one later: Vercel
  project → **Settings → Domains**, then add one DNS record at your registrar.
- **Original source code** — this repo holds a *rendered snapshot* of the page,
  not the original build project. If the upstream source becomes available, it
  could replace `index.html`.

---

## 9. Quick troubleshooting

- **Vercel didn't redeploy after a push?** Check the Vercel **Deployments** tab,
  and confirm the Git connection is still active under **Settings → Git**.
- **Site returns 401 / asks for login?** Deployment protection got re-enabled —
  disable it under Vercel project **Settings → Deployment Protection**.
- **`git push` asks for a username?** Run `gh auth setup-git` (with
  `~/.local/bin` on PATH) to re-link the credential helper.
