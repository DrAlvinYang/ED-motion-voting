# Moved — redirect only

The ED tools that used to live in this repo moved on 2026-10-13 to the
**MichaelGarronHospital-ED** GitHub organization, one repo per tool:

| Old address (dralvinyang.github.io/ED-motion-voting/…) | New address |
|---|---|
| `/` | https://michaelgarronhospital-ed.github.io/ (dashboard) |
| `/tools/motion-voting/…` | https://michaelgarronhospital-ed.github.io/mgh-ed-motion-voting/… |
| `/tools/interviews/…` | https://michaelgarronhospital-ed.github.io/mgh-ed-hiring/… |

This repo now only serves redirects so old links and QR codes keep working.
`404.html` does the work: GitHub Pages serves it for every path that no longer
exists here, and it rewrites the path onto the new address (query and `#hash`
kept). `index.html` covers the bare root.

The full history of the old tools is still in this repo's git history.
Current code: https://github.com/MichaelGarronHospital-ED
