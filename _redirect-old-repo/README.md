# Legacy URL redirect

**Not a tool.** This folder is the *source* for a separate, redirect-only GitHub
repo that keeps the old published links working.

## Why

This repo was renamed `ED-motion-voting` → `mgh-ed-tools`, which changes the
GitHub Pages path for every tool:

```
old:  https://dralvinyang.github.io/ED-motion-voting/tools/motion-voting/
new:  https://dralvinyang.github.io/mgh-ed-tools/tools/motion-voting/
```

GitHub redirects the *repository* URL after a rename, but don't count on it
redirecting the *Pages* site. Links already shared with the ED group — meeting
QR codes, the interviews mock link emailed to Kyle and Amanda — point at the
old path. This folder makes those keep working permanently.

## How to set it up (once, after renaming)

1. Rename this repo to `mgh-ed-tools` first, which frees the old name.
2. Create a **new, empty public repo** named exactly `ED-motion-voting`.
3. Upload **only** `index.html` and `404.html` from this folder to its root.
   Do not copy this README — it isn't needed there.
4. In that repo: **Settings → Pages → Deploy from a branch → `main` / root**.
5. Wait ~1 minute, then test both:
   - `https://dralvinyang.github.io/ED-motion-voting/` → landing page
   - `https://dralvinyang.github.io/ED-motion-voting/tools/motion-voting/`
     → the voting tool

## How it works

`404.html` does the real work. GitHub Pages serves it for **any** path that
doesn't exist in the redirect repo, so every old deep link hits it. The script
strips the `/ED-motion-voting` prefix, re-attaches the rest of the path onto
`/mgh-ed-tools`, and preserves the query string and hash fragment.

`index.html` covers the bare root, where a real file *is* found and `404.html`
never fires. It uses both a `<meta http-equiv="refresh">` and a script, so it
still works with JavaScript disabled.

## Keeping it in sync

If the repo is ever renamed again, update `NEW_BASE` in `404.html` and the
three hardcoded URLs in `index.html`, then re-upload both to the redirect repo.
