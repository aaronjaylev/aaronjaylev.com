# aaronjaylev.com

The source for [aaronjaylev.com](https://aaronjaylev.com), my personal site and online resume. It is a fully static, single-page site built with Astro and Tailwind CSS, with SEO and structured data for search engines and AI crawlers.

## Tech stack

- **[Astro](https://astro.build)** (static output, zero client-side JavaScript by default)
- **[Tailwind CSS v4](https://tailwindcss.com)** via the official Vite plugin
- **GitHub Actions** for CI and FTPS deployment
- **Node.js 22**

## What's included

- **Responsive single-page resume site** with hero, featured projects, skills, and contact sections
- **SEO basics:** per-page `<title>` and meta description, Open Graph and Twitter card tags, canonical URL, and an XML sitemap
- **Structured data:** `schema.org` `Person` JSON-LD markup
- **Crawler policy:** `robots.txt` pointing to the sitemap, plus an `llms.txt` file for AI crawlers
- **Icons and manifest:** favicons, Apple touch icon, and a web app manifest
- **Analytics:** Google Analytics (gtag.js) loaded from the shared layout

## Project structure

```text
.
├── .github/workflows/
│   ├── ci.yaml          # Build check on every pull request
│   └── deploy.yaml      # Build and deploy to hosting on push to main
├── public/              # Static assets: images, resume PDF, robots.txt, sitemap.xml
├── src/
│   ├── layouts/
│   │   └── Layout.astro # <head> metadata, structured data, analytics
│   ├── pages/
│   │   └── index.astro  # Landing page
│   └── styles/
│       └── global.css   # Tailwind entry point
├── astro.config.mjs
└── package.json
```

## Local development

Requires Node.js 20 or newer (22 is used in CI).

```sh
npm install
npm run dev       # Dev server at http://localhost:4321
npm run build     # Production build to ./dist/
npm run preview   # Serve the production build locally
```

## Deployment

Pushing to `main` runs the **Deploy website** workflow, which installs dependencies with `npm ci`, runs `npm run build`, and uploads `dist/` over FTPS. The workflow reads its server credentials from the repository secrets `FTP_SERVER`, `FTP_USERNAME`, and `FTP_PASSWORD`.

Pull requests run the **CI** workflow, which performs the same clean install and build so that broken changes are caught before they merge.
