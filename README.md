# ED Tools

Small internal web tools for the Emergency Department. Each tool is a
self-contained static site under [`tools/`](tools/), deployed together via
**GitHub Pages** from `main`. No build step — plain HTML/CSS/JS, with Firebase
Firestore for any live data.

## Tools

| Tool | What it does | Folder |
|------|--------------|--------|
| **Motion Voting** | Live weighted voting for meeting motions | [`tools/motion-voting/`](tools/motion-voting/) |
| **Physician Hiring** | Screen applicants, collect availability, auto-build interview panels, score & rank | [`tools/interviews/`](tools/interviews/) |

_New tools get added here as they ship._

## Structure

```
index.html            Landing page linking to every tool
tools/<tool>/         One self-contained tool per folder (relative paths)
CLAUDE.md             Shared conventions for working in this repo
.claude/              Shared Claude Code settings & permissions
```

## Adding a new tool

1. Create `tools/<new-tool>/` and build it as a self-contained static site
   (relative asset paths only).
2. Add a `tools/<new-tool>/CLAUDE.md` (and optional `README.md`).
3. Link it from the root `index.html` and the table above.
4. Decide its Firebase approach (shared project + namespaced collections, or its
   own project) and add a `firestore.rules` if it needs one.

See [`CLAUDE.md`](CLAUDE.md) for the full conventions, including why tools live
side by side on `main` rather than on per-tool branches.

## Deployment

GitHub Pages serves the whole repo from `main` / root, so every tool ships
together. The live URLs:

| Page | URL |
|------|-----|
| Landing page | https://dralvinyang.github.io/ED-motion-voting/ |
| Motion Voting | https://dralvinyang.github.io/ED-motion-voting/tools/motion-voting/ |
| Physician Hiring | https://dralvinyang.github.io/ED-motion-voting/tools/interviews/ |

New tools follow the same shape:
`https://dralvinyang.github.io/ED-motion-voting/tools/<tool>/`.

Per-tool setup (Firebase, passcodes, roster) lives in each tool's own
`README.md` — e.g. [`tools/motion-voting/README.md`](tools/motion-voting/README.md).

### The repo name — rename still pending

The GitHub repo is still called **`ED-motion-voting`**, from when it held only
that one tool, so that name is in every live URL above. The working directory
and these docs use `mgh-ed-tools`, which is the name it is *going* to get.

**Don't rename it casually.** GitHub forwards the repository URL and git remotes
after a rename, but **not the Pages site** — so the moment the repo is renamed,
every published link 404s. Two are already out with the ED group:

- the interviews mock link emailed to Kyle and Amanda (Sept 16)
- `tools/motion-voting/voter-qr.png`, the meeting QR code, which encodes
  `https://dralvinyang.github.io/ED-motion-voting/`

[`_redirect-old-repo/`](_redirect-old-repo/) is the prepared fix: a separate
redirect-only repo that takes over the old name and forwards every old path.
Follow its README **immediately** after renaming — old links are dead in the gap
between the two steps.

Best done when nothing is mid-flight: after the Oct 2026 hiring round closes.
