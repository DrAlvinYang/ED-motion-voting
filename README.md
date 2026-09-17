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

GitHub Pages serves the whole repo from `main` / root. Each tool is live at
`https://<user>.github.io/<repo>/tools/<tool>/`. The root URL shows the landing
page. Per-tool setup (Firebase, passcodes, roster) lives in each tool's own
`README.md` — e.g. [`tools/motion-voting/README.md`](tools/motion-voting/README.md).
