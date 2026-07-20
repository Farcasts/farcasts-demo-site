# farcasts demo site

Aster, a fictional single origin coffee brand. A standalone third party site that
embeds the farcasts applier cross origin. It is deployed on its own Vercel domain
(demo.farcasts.com), a different origin from `app.farcasts.com`, so it exercises the
real cross origin path (CORS on `/api/config` and `/api/events`) exactly as a customer
site would.

## Pages

Static, multi page, no build step.

- `index.html`, home. Carries the gated hero, the tested surface.
- `menu.html`, the Field Guide, the season's coffee lots as an almanac.
- `story.html`, the brand story and roastery timeline.
- `visit.html`, hours, address, and a demo note form.
- `aster.css`, the shared design system (tokens, header, footer, gate CSS).

## Embed contract

`index.html` carries the whole contract on its gated hero:

- `<script src="https://app.farcasts.com/farcasts.js" data-cfasync="false" data-farcasts-project="demo-farcasts-com">`
  loads the applier and points it at the project. Onboarding slugs the origin
  hostname, so demo.farcasts.com becomes the project id `demo-farcasts-com`. Do not
  change these values.
- `data-cf-hide` on the `<html>` element plus `data-farcasts-gate` on each testable
  element hold the gated surfaces at opacity 0 until the variant applies, so no control
  flash. The gate CSS lives in `aster.css`.
- The gated hero ids are `hero-headline`, `hero-sub`, `hero-cta`, and `hero-image`.

Every page includes the same applier script so cross navigation keeps it loaded, but
only the home page declares gated surfaces (that is the tested project).

## Deploy

Static site, no build. Deploy to Vercel as its own project on its own domain. The
`CNAME` file pins the custom domain.

## Local preview

Serve the folder with any static server, then open it, e.g.
`python3 -m http.server 8000`.
