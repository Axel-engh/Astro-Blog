# GitHub Copilot Instructions for "short-shell" (Astro Starter)

Summary
- Minimal Astro site (Astro ^5.16) scaffold created from the `basics` template.
- Static site: pages live in `src/pages`, reusable UI in `src/components` and `src/layouts`, static assets in `src/assets` and `public/`.

Quick workflows (commands)
- Install dependencies: `npm install` (run from project root)
- Run dev server: `npm run dev` (default `astro dev`, serves at `http://localhost:4321`)
- Build production site: `npm run build` → output to `dist/`
- Preview build: `npm run preview`

Architecture & important files
- `package.json` — single dependency: `astro`. Use provided npm scripts.
- `astro.config.mjs` — default empty config; expect features to be added here when integrations are required.
- `src/pages/` — route-driven pages (`index.astro`, `about.astro`, `blog.astro`). Pages here use plain HTML and minimal frontmatter.
- `src/layouts/Layout.astro` — top-level layout with a `<slot />` the project can optionally import/use in pages.
- `src/components/Welcome.astro` — example component showing asset imports (`import astroLogo from '../assets/astro.svg'`) and component-scoped styles.
- `src/assets/` — image assets imported directly into components (important: components import assets via JS import, not via absolute path).
- `public/` — static files served at site root (e.g., `favicon.svg`). Prefer `public` for files required at runtime without bundling.

Project-specific conventions & patterns
- Pages are simple `.astro` files that often contain only static HTML content. Follow the current pattern when adding pages: simple frontmatter block (`---`) then HTML template.
- Components import static assets from `src/assets` (see `Welcome.astro`), so prefer ES module imports when bundling or referencing image sizes/optimization.
- Layouts are provided but not enforced; decide per new page whether to `import Layout from '../layouts/Layout.astro'` and wrap content with it to ensure consistent head/meta structure.
- Title and meta tags are currently in individual pages; when centralizing SEO, move meta to `Layout.astro` and use props/slots for per-page overrides.

Integration points & external dependencies
- Only external dependency is `astro` (no CI, database, or serverless functions configured). Expect to add integrations through `astro.config.mjs` when necessary (e.g., adapter-static, MDX, content collections).

Developer notes & debugging
- Dev server logs errors/warnings to terminal; use `npm run dev` to reproduce issues locally.
- Since site is static, inspect generated output in `dist/` after `npm run build` to verify production artifacts.
- There are unresolved merge markers in `short-shell/README.md` — watch for repo cleanliness and resolve git conflicts before major changes.

What an agent should do first
1. Run `npm ci` / `npm install` to verify environment and that `astro` works locally. ⚠️ Node 18+ is recommended for recent Astro versions.
2. Run `npm run dev` to confirm dev server behavior and that pages render (check `/`, `/about`, `/blog`).
3. Inspect `src/pages` to see how new pages should be structured; mirror the existing pattern when adding pages.

Useful examples (copyable snippets)
- Importing an asset in a component:
  import logo from '../assets/astro.svg';
  <img src={logo.src} alt="Astro Logo" />

- Using the layout (recommended convention):
  ---
  import Layout from '../layouts/Layout.astro';
  ---
  <Layout>
    <h1>Page content</h1>
  </Layout>

Guidance for pull requests
- Keep changes scoped to a single purpose (content, style, or config).
- If adding third-party integrations, update `astro.config.mjs` and add an explanation in `README.md`.
- Resolve merge conflicts (seen in README) before merging.

If anything seems unclear or you want me to expand a section (e.g., add example tests, CI, or a standardized layout/SEO pattern), tell me which area and I'll iterate. ✅