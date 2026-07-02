# farcasts demo site

A standalone third party site (Aster, a fictional coffee brand) that embeds the
farcasts applier cross origin. It is deployed on its own Vercel domain, a
different origin from `exp.farcasts.com`, so it exercises the real cross origin
path (CORS on `/api/config` and `/api/events`) exactly as a customer site would.

## Embed contract

`index.html` carries the whole contract:

- `window.__FARCASTS__ = { projectId, endpoint }` points the applier at the
  dashboard origin. Set `projectId` to a project you have authored in the
  dashboard.
- `document.documentElement.setAttribute("data-cf-hide", "")` plus
  `data-farcasts-gate` on each testable element hold the gated surfaces at
  opacity 0 until the variant applies, so no control flash.
- `<script src="https://exp.farcasts.com/farcasts.js">` loads the applier.

## Deploy

Static site, no build. Deploy to Vercel as its own project on its own domain.

## Local preview

Serve the folder with any static server, then open it, e.g.
`python3 -m http.server 8000`.
