# Guitar Bracing — Modal Analysis

An in-browser tool for designing acoustic guitar top-plate bracing and
seeing how it affects the plate's vibrational mode shapes — trace a
soundboard outline, draw braces, run a finite-difference modal solver, and
view the results as 2D displacement plots or a navigable, animated 3D
surface.

**No install, no build step, no server.** It's a single self-contained
`index.html` file. Open it directly in a browser, or host it as a static
website — both work identically.

## Features

- **Soundboard tracing** — upload a photo or plan drawing, scale it against
  real-world dimensions, and trace the body outline and sound hole.
- **Brace editor** — draw straight or curved braces with per-brace width,
  height, density, and modulus; live mass/stiffness summary.
- **Modal analysis** — a finite-difference thin-plate solver (simply
  supported or elastically restrained edges) computes the first six mode
  shapes and natural frequencies.
- **Hybrid solver engine** — runs on a hand-written JavaScript solver by
  default (always available, works fully offline), and automatically
  upgrades to a Python engine (numpy + scipy, via
  [PyScript](https://pyscript.net)) running entirely in the browser once it
  finishes loading in the background — no server-side Python involved.
- **3D mode-shape viewer** — a navigable, animated Three.js surface for each
  mode, with adjustable exaggeration, animation speed, and an independent
  wireframe-density overlay.
- **Save/export** — mode-shape PNGs, a composite sheet, the bracing pattern,
  and a project JSON you can reload later.

## Running it

Just open `index.html` in Chrome or Edge. That's the entire setup.

A few things work better once it's served over `https://` (e.g. via GitHub
Pages) rather than opened as a local `file://` path:

- The **"Save" folder picker** (native "choose a folder to save into")
  requires a secure context. Over `file://` it silently falls back to
  downloading a `.zip` instead — both work, the folder picker is just nicer.
- The **Python solver engine** and the **3D viewer** load Three.js and
  PyScript from a CDN, so they need internet access the first time,
  regardless of how the page itself is served.

If neither of those apply to you, `file://` is perfectly fine.

## Deploying to GitHub Pages

1. Push this repo to GitHub (public, unless you're on a paid plan that
   supports Pages on private repos).
2. Repo → **Settings → Pages** → under "Build and deployment", set
   **Source** to "Deploy from a branch", **Branch** to `main` (or
   `master`), folder `/ (root)` → **Save**.
3. GitHub builds and publishes the site within a minute or two, at:
   `https://<your-username>.github.io/<repo-name>/`
4. Any time you push changes to `index.html`, the live site updates
   automatically — no rebuild step.

No repo secrets, environment variables, or GitHub Actions workflow are
needed — Pages serves the static file as-is.

## Tech stack

- Vanilla JavaScript + HTML5 Canvas 2D for the editor, tracing, and 2D mode
  plots — no framework, no bundler.
- [Three.js](https://threejs.org) (loaded from a CDN) for the 3D mode-shape
  viewer.
- [PyScript](https://pyscript.net) / [Pyodide](https://pyodide.org)
  (loaded from a CDN) for the optional in-browser Python/numpy/scipy
  solver engine.

## License

Add a `LICENSE` file if you want to specify usage terms — none is included
by default.
