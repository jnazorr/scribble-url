# scribble.url

Handwritten notes that live entirely inside the URL.

Draw with a Windows stylus → strokes are fit to cubic Béziers (Schneider 1990) → encoded into the URL fragment. Share the link, the recipient sees the same drawing. No server, no account, no database.

**Live:** https://jnazorr.github.io/scribble-url/

## How it works

- Pen input via `PointerEvent` (Windows Ink supported; mouse/touch rejected).
- Each stroke is fit to a chain of cubic Béziers via Schneider's `FitCurve` algorithm — typically 5–15 cubics per stroke vs. hundreds of raw samples.
- Cubics are delta-encoded against the previous endpoint, palette-indexed (≤16 colors), 4-bit pressure-flagged.
- Payload is compressed with brotli (fallback deflate) and base64url'd into `location.hash`.

A 200-point handwritten stroke fits in ≈40 bytes after the pipeline.

## Local dev

It's a single `index.html`. Open it directly (`file://`) and it works, except:
- the "Copy link" button is blocked by Chrome's clipboard-on-file:// restriction
- the URL has no host that anyone else can fetch from

To share, host as a top-level document. GitHub Pages, Cloudflare Pages, Netlify Drop, anywhere static.

## License

MIT
