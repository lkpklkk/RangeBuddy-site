# RangeBuddy website

Static pages for RangeBuddy, hosted on GitHub Pages. No build step: the repo root is the site.

| Page | Purpose |
|---|---|
| `/` | Home: links to both apps' pages (the site root 404'd before this existed) |
| `/privacy/` | App Store Connect privacy policy URL |
| `/support/` | App Store Connect support URL |
| `/livetracer/` | LiveTracer support URL |
| `/livetracer/privacy/` | LiveTracer privacy policy URL (camera, microphone, motion, location, add to Photos) |
| `/get/` | Where the QR code on shared videos leads; forwards to the App Store once `TARGET` is set |

## Publish on GitHub Pages

1. Push this folder to a public GitHub repo (the repo name becomes the path:
   `https://<username>.github.io/<repo>/`).
2. Settings → Pages → Deploy from a branch → `main`, folder `/ (root)`.
3. `.nojekyll` makes Pages serve the files as they are.

A custom domain added later redirects the `github.io` URLs to it, so links already in use keep
working.

## Before publishing

- The support address (`keplee99@gmail.com`) appears in every page;
  change them together.
- Check the "Last updated" date on the privacy page.
- `get/index.html`: leave `TARGET` empty until there is somewhere to send people; the page then
  shows "Coming soon". Set it to the App Store link at launch (with App Store Connect campaign
  parameters such as `pt` and `ct=badge` to count installs from shared clips). Query parameters
  on the `/get/` URL are passed through to the target.
- In the app, `UIConfiguration.shareCard.badgeLink` should point at this site's `/get/` URL, and
  `badgeLine` should change with it.
- Re-check the privacy page whenever the app adds a permission, network access or in-app
  purchases. It describes RangeBuddy only (camera, microphone, motion, add to Photos; no network
  code, account or analytics). LiveTracer has its own page at `livetracer/privacy/`, which also covers location.

## Where things come from

- `assets/site.css`: the brand tokens from the app's brand guide (`docs/architecture/brand.md` in
  the GolfApps repo; Original theme, light and dark, Increase Contrast) in an iOS grouped-list
  layout. Text sizes are in rem; on iOS Safari they follow Dynamic Type.
- `assets/*.svg`: copies of the app's `RangeBuddyLogo`, `RangeBuddyWordmark` and
  `RangeBuddyIconMark` assets. Copy them again if the app's assets change; don't edit them here.
- `assets/fonts/`: Merriweather 400 and 700, Latin subset (SIL OFL, `OFL.txt`), served from this
  site so the pages make no third-party requests.

## Preview locally

```bash
python3 -m http.server 8771 --directory .
```

Then open `http://localhost:8771/privacy/`.
