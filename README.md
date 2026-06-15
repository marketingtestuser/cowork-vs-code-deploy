# Claude Code vs. Claude Cowork — Operator's Field Guide

A captured snapshot of the live page at <https://cowork-vs-code-deploy.vercel.app/>.

"The tool that says 'for engineers' is actually the biggest unlock for business
leaders. A field guide for GTM operators, revenue leaders, and anyone who's been
told they don't need Claude Code." — *Jonathan Moss*

## Contents

- `index.html` — the full page (self-contained; all CSS is inline)
- `abn-logo-dark.png` — the only local image asset

The page also loads the Inter and JetBrains Mono fonts from the Google Fonts CDN
at runtime; those are not vendored here.

## Viewing locally

Open `index.html` in any browser, or serve the folder:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Note

This is a snapshot of the rendered/deployed page captured on 2026-06-15, not the
original project source.
