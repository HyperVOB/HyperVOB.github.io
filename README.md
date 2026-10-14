<!--
SPDX-FileCopyrightText: HyperVOB contributors
SPDX-License-Identifier: CC-BY-4.0
-->
# hypervob.media

HyperVOB's website: one page, served by GitHub Pages at <https://hypervob.media>. Static
HTML and CSS, no build step, no JavaScript, nothing loaded from another site; the
Content-Security-Policy in each page's `<head>` allows only this site's own images and
stylesheet.

| File | What |
|---|---|
| `index.html` | The page |
| `404.html` | What GitHub Pages serves for an unknown address |
| `assets/site.css` | The styles: the brand's colours, the system's fonts, the unwound track |
| `assets/wordmark-on-dark.svg`, `assets/wordmark-on-light.svg`, `assets/favicon.svg` | Copies of the HyperVOB brand's files |
| `assets/social-preview.png` | The brand's social preview (1280 × 640), for link previews (`og:image`) |
| `favicon.ico` | 16, 32 and 48 px icons for browsers and crawlers asking for `/favicon.ico`; the pages link it with `sizes="32x32"` before the SVG, which browsers that can use it prefer |
| `apple-touch-icon.png` | 180 px, opaque: iOS home screens round it themselves |
| `manifest.webmanifest` | Name, colours (Pit) and icons for "Add to Home screen"; `display: browser`, so a shortcut opens the page in the browser. The pages' CSP allows it (`manifest-src 'self'`) |
| `assets/icon-192.png`, `assets/icon-512.png`, `assets/icon-maskable-512.png` | The manifest's icons: the tile, shown as it is, and the full-bleed mark, which launchers crop to their shape |
| `robots.txt` | Every crawler welcome, AI ones included; points to the sitemap |
| `sitemap.xml` | The site's one address |
| `.well-known/security.txt` | Where to report a vulnerability (RFC 9116); renew `Expires` before it passes |
| `CNAME` | The custom domain |
| `.nojekyll` | Serve the files as they are, without Jekyll |
| `.github/rulesets/main.json` | `main`'s ruleset, applied by the HyperVOB repository's `scripts/harden-github.sh`: signed commits, linear history, no force-push or deletion. No pull requests or status checks: the site has no CI |

## Brand

The colours, the mark's geometry and the wordmark come from the HyperVOB brand, whose
sources and guidelines live in the HyperVOB repository's `brand/` folder. The copies in
`assets/` are kept in step with it, and the PNGs and `favicon.ico` are copies of its
`brand/renders/`, made by its `scripts/render_brand.py`: re-render there, then copy
here. The track on the page is the mark's spiral and run
at the mark's own stroke (3.5) and spot (r 3.5) in its 48-unit drawing, the run carried on
across the page.

## Publishing

GitHub Pages deploys the `main` branch's root, at the custom domain in `CNAME`. The
domain is verified for the organisation's Pages, so no other account can serve it. In
Cloudflare the domain's Pages records are "DNS only", not proxied: GitHub issues the
certificate only once they resolve to it, and "Enforce HTTPS" is turned on after that.
Should the organisation's Actions policy (selected actions, SHA pinning) stop
GitHub's own Pages build, the fallback is a workflow of SHA-pinned
`actions/upload-pages-artifact` and `actions/deploy-pages`.

Preview locally with a server that sends `.svg` as `image/svg+xml` (Python's on Windows
sends `text/xml`, and browsers then refuse the images).

## Licence

The text, the styles and the marks are licensed [CC BY 4.0](LICENSES/CC-BY-4.0.txt);
credit "HyperVOB contributors". The wordmark is Martian Mono (Roman Shamin, Evil Martians;
SIL Open Font License 1.1), outlined: no font is included. A licence is not a trademark
permission: using the name or the mark for another project, or so as to suggest
endorsement, is a separate matter. The files follow [REUSE](https://reuse.software).
