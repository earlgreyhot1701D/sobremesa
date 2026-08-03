# Design source

These files are **not deployed**. The deployed site is `../index.html`, which is fully self-contained.

- `Sobremesa.dc.html` — the Claude Design component the page was authored in
- `support.js` — the Claude Design runtime this component depends on. Third-party framework code, not authored here. It uses `innerHTML` and `fetch` internally; `index.html` has no such dependency and neither pattern appears in it.
- `_title-ref.png` — a lettering reference used while designing the wordmark

Kept for provenance. Nothing here is served in production.
