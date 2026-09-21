# ED Tools

A monorepo of small, independent web tools for the Emergency Department. Each
tool is a self-contained static site under `tools/<tool-name>/`, served by
GitHub Pages straight from `main`. No build step, no framework — plain
HTML/CSS/JS (ES modules), with Firebase/Firestore for any live data.

## Layout

```
/index.html            Landing page linking to every tool
/tools/<tool>/         One folder per tool — fully self-contained
  index.html           Public entry point (relative asset paths only)
  js/  css/            Tool-local code and styles
  firestore.rules      Firestore rules for this tool's Firebase project
  CLAUDE.md            Tool-specific context and gotchas
/.claude/              Shared Claude Code settings & permissions
/_redirect-old-repo/   Not a tool — source for the legacy-URL redirect repo
```

## Naming

- **Repo: `mgh-ed-tools`** (renamed from `ED-motion-voting` once it outgrew one
  tool). Live at `https://dralvinyang.github.io/mgh-ed-tools/tools/<tool>/`.
- **Tool folders are lowercase-kebab-case** (`motion-voting`, `interviews`) and
  become the public URL segment, so treat a folder name as a published API:
  renaming one breaks every shared link and QR code for that tool.
- **Nothing in the repo hardcodes the repo name** except docs and the landing
  page. Tools use relative paths only, so the repo could be renamed again
  without touching tool code.
- **Firebase project ids are immutable and deliberately per-tool**
  (`ed-motion-voting-99b96`, `mgh-ed-hiring`). They do *not* track the repo
  name — don't "fix" them to match.

## How to work here

- **One tool per folder.** A tool never reaches into another tool's folder.
  Keep all of a tool's assets under `tools/<tool>/` with **relative paths** so
  GitHub Pages serves it at `…/tools/<tool>/`.
- **Branches are for work-in-progress, not for tools.** All shipped tools live
  together on `main`. Use a feature branch while building/changing a tool, then
  merge to `main`. Do not give a tool its own long-lived branch — that would
  stop them from being deployed side by side.
- **Read the tool's own `CLAUDE.md` first** when working inside a tool folder;
  it carries the specifics this file deliberately leaves out.
- **Firebase is decided per tool.** Whether a new tool shares an existing
  Firebase project (namespaced collections + one `firestore.rules`) or gets its
  own project is decided when that tool is built. Don't assume a shared project.

## Adding a new tool

1. `mkdir tools/<new-tool>/`, build it as a self-contained static site.
2. Add a `tools/<new-tool>/CLAUDE.md` and (optionally) a `README.md`.
3. Add a link to it in the root `index.html`.
4. Decide its Firebase approach and add a `firestore.rules` if it needs one.
