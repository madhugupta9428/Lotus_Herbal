# Lotus_Herbal

A small static website demo for "Lotus Herbals" — a fictional brand showcasing herbal and Ayurvedic beauty & wellness products. This repository contains plain HTML pages styled with Tailwind CSS (via CDN by default) for quick prototyping.

This README explains how the site works, how to run it locally, how to replace the CDN Tailwind with a local build (recommended for production), examples for adding screenshots, deployment options, and contribution guidelines.

---

Table of contents
- Overview
- How it works (technical explanation)
- Files & structure
- Screenshots
- Run locally (quick preview)
- Build with Tailwind (production-ready)
- Deployment (GitHub Pages + others)
- How to add screenshots to the README
- Accessibility, SEO & performance tips
- Contributing
- Troubleshooting
- License

---

Overview
--------
Lotus_Herbal is a static front-end demo showing a main landing page and category pages:
- lotus.html — the landing page with hero, categories, trending products, about and footer.
- skincare.html, haircare.html, makeup.html, wellness.html — per-category product listing pages.

The project uses Tailwind utility classes (via CDN) to speed up prototyping and simple inline/custom CSS for brand colors.

How it works (technical explanation)
-----------------------------------
- Static HTML: Each page is a standalone HTML file that a browser can render directly — there is no backend.
- Styling:
  - Tailwind CSS is included from the CDN in each page using:
    ```html
    <script src="https://cdn.tailwindcss.com"></script>
    ```
  - A few custom CSS rules (brand green classes) are defined inline in each page for quick theming:
    - `.bg-lotus-green` — brand background
    - `.text-lotus-green` — brand text color
    - `.hover-lotus-green` — hover states
- Images: All product and hero images are currently referenced from remote URLs. For production, host optimized images in the repo or a CDN.
- Navigation: Each category tile links to its respective HTML file (e.g., skincare.html).

Files & structure
-----------------
- lotus.html — Main landing / home page.
- skincare.html — Skincare category page.
- haircare.html — Haircare category page.
- makeup.html — Makeup category page.
- wellness.html — Wellness category page.
- (Optional) README.md — this document.

Screenshots
-----------
Add screenshots to illustrate the design and UX. Example images embedded below are placeholders; replace with actual repo screenshots.

Home / Hero section
![Home hero screenshot](https://images.pexels.com/photos/2533266/pexels-photo-2533266.jpeg?auto=compress&cs=tinysrgb&h=750&w=1260)

Products grid example
![Product cards screenshot](https://images.pexels.com/photos/461428/pexels-photo-461428.jpeg?auto=compress&cs=tinysrgb&h=750&w=1260)

How to run locally (quick preview)
----------------------------------
No build step is required for basic preview — just open the files in your browser or run a lightweight server.

1) Open directly (quick & dirty)
- On most OSes, double-click `lotus.html` to open in your default browser.
- Note: Some features may be restricted when using the file:// protocol, but most static pages render fine.

2) Recommended: run a local HTTP server
- Python 3:
  ```bash
  # from the project root
  python -m http.server 8000
  # open http://localhost:8000/lotus.html
  ```
- Node (http-server):
  ```bash
  npm install -g http-server
  http-server -p 8000
  # open http://localhost:8000/lotus.html
  ```
- VS Code: use the Live Server extension to preview pages with auto-reload.

Build with Tailwind (production-ready)
-------------------------------------
Using Tailwind CDN is fine for demos. For production, build a minimized Tailwind CSS file and include only used utilities.

1) Initialize project and install build tools (Node.js required)
```bash
# in project root
npm init -y
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

2) Create a CSS entry file (e.g., src/styles/tailwind-input.css)
```css
/* src/styles/tailwind-input.css */
@tailwind base;
@tailwind components;
@tailwind utilities;

/* Add your custom utilities or import a small custom stylesheet here */
```

3) Configure tailwind.config.js — add content paths so unused CSS is purged:
```js
module.exports = {
  content: [
    "./*.html"
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

4) Build CSS (development)
```bash
npx tailwindcss -i ./src/styles/tailwind-input.css -o ./dist/styles.css --watch
```

5) Build CSS (production)
```bash
npx tailwindcss -i ./src/styles/tailwind-input.css -o ./dist/styles.css --minify
```

6) Link the generated CSS in your HTML pages (replace CDN):
```html
<link rel="stylesheet" href="dist/styles.css">
```

Deployment
----------
- GitHub Pages
  1. Push repository to GitHub.
  2. In repository Settings → Pages, choose the branch (usually main) and the root (/) as the publishing source.
  3. Your static pages will be available at: https://<username>.github.io/<repo>/lotus.html (or the root URL for user/organization pages).
- Netlify / Vercel
  - Connect the repository, set the publish directory to the repository root. These providers auto-detect static sites and will deploy on push.
- S3 + CloudFront
  - Upload static files to S3 and configure CloudFront for CDN distribution.

How to add screenshots to this README
------------------------------------
1. Create a folder in your repo for screenshots (e.g., `/screenshots`) and add PNG/JPEG files.
2. Reference them in the README using relative path:
```md
![Home page screenshot](screenshots/home-hero.png)
```
3. Commit and push — the image will display on GitHub automatically.

Accessibility, SEO & performance tips
-------------------------------------
- Accessibility:
  - Add descriptive alt attributes to every `<img>` tag.
  - Ensure color contrast for text on backgrounds meets WCAG AA.
  - Use semantic HTML (main, nav, header, footer, button).
- SEO:
  - Add meta description, title tags, and Open Graph tags for previews.
  - Use meaningful heading hierarchy (one H1 per page).
- Performance:
  - Optimize and compress images (WebP where possible).
  - Lazy-load offscreen images (loading="lazy").
  - Build Tailwind CSS locally and purge unused classes.

Contributing
------------
Thanks for wanting to contribute! Simple steps:
1. Fork the repo.
2. Create a branch (e.g., feature/add-screenshots).
3. Make changes and commit.
4. Open a pull request describing the change.

Ideas for improvements:
- Add a small JSON file listing products and generate pages from it (or convert to a static site generator).
- Add a search/filter UI for products.
- Add a simple cart demo (client-side only).
- Replace CDN Tailwind with a local build and minified CSS.

Troubleshooting
---------------
- Tailwind not applying styles?
  - Ensure the CDN script or built CSS is referenced in the page head.
  - If building locally, make sure your HTML paths are included in tailwind.config.js content array so purge works.
- Images not showing?
  - Verify the image URL/path is accessible and correct. For local images, use relative paths and commit them to the repo.

License
-------
Add a LICENSE file to choose a license. For small demos, MIT is common:

```
MIT License
```

Credits
-------
- Tailwind CSS (for rapid UI prototyping)
- Placeholder images from Pexels in README examples

---

Thank you —
