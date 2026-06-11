# Portfolio — Zaid Arshad Tambe

A single-page personal portfolio for **Zaid Arshad Tambe** — Senior Java Developer & Technical Lead.

Light, premium, modern-minimal aesthetic. The entire site is one self-contained `index.html` (HTML + CSS + vanilla JS, no frameworks, no build step). Fonts are loaded from Google Fonts.

## Structure

```
ZaidPortfolio/
├── index.html        # the entire site
├── README.md         # this file
└── .gitignore
```

## Run locally

Just open `index.html` in a browser. No build, no dependencies.

```bash
# optional: serve with a tiny local server
python -m http.server 8000
# then visit http://localhost:8000
```

## Deploy

Any static host works with zero config:

- **GitHub Pages** — Settings → Pages → deploy from `main`
- **Netlify** / **Vercel** — drop the repo in, serve `index.html`

## Push to GitHub

```bash
git init
git add index.html README.md .gitignore
git commit -m "feat: personal portfolio — light premium single-page site"
git branch -M main
git remote add origin <your-repo-url>
git push -u origin main
```

## Sections

Floating pill nav · Hero · About · Experience (timeline) · AI-Augmented Practice · Independent Work (White Orchid) · Skills · Recognition · Contact · Footer.
