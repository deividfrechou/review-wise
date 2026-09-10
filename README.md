# ReviewWise — Site Documentation

A static, editorial-style review blog built with plain HTML, CSS, and JavaScript — no build tools, no framework, ready to host on GitHub Pages.

The site is branded **ReviewWise** ("Smart Reviews. Better Choices."), focused on healthy aging and cellular energy content, currently built around **Pep Tonic** as the first featured product.

---

## 1. File structure

```
/
├── index.html            Homepage (featured article + latest reviews, paginated)
├── estilo.css             Stylesheet
├── script.js              Interactivity (mobile nav, pagination, footer year)
├── robots.txt             Crawler rules for Google/Bing
├── sitemap.xml             List of indexable pages
├── reviews/                (create this folder) individual article/review pages go here
├── assets/
│   ├── logo.png                  Icon + wordmark, transparent background (header and footer)
│   ├── favicon.png               512×512 favicon generated from the logo icon
│   └── images/
│       ├── why-does-energy-change-with-age.jpg         Featured article cover (hero)
│       ├── 5-ingredients-healthy-aging.jpg               Article cover
│       ├── anti-aging-supplements-vs-wellness-drinks.jpg  Article cover
│       ├── why-people-seek-pep-tonic.jpg                  Article cover
│       └── pep-tonic-thumb.jpg                            Small square crop used for the Pep Tonic sidebar listing
└── CNAME                   (added automatically by GitHub when you set a custom domain)
```

Only `logo.png` and `favicon.png` are kept at the top level of `/assets` — no extra brand image variants, as requested. The four article cover images (1200×630, matching the standard social-share ratio) are in `/assets/images/`, already wired into `index.html` with descriptive filenames and `alt` text.

The homepage links to four article pages that don't exist yet — this is intentional, matching the plan to build them next:

- `reviews/why-does-energy-change-with-age.html` (the featured article)
- `reviews/5-ingredients-healthy-aging.html`
- `reviews/anti-aging-supplements-vs-wellness-drinks.html`
- `reviews/why-people-seek-pep-tonic.html`

Create a `reviews/` folder and add each page there, keeping the exact filenames already referenced in `index.html` — that way you won't need to edit any links once the pages exist. **Don't submit the site to Google Search Console or publish it live until at least these four pages exist**, since right now those links would 404.

---

## 2. How the homepage is organized

- **Featured article** — one large card with an image, title, and short excerpt, pulled out above the rest.
- **Featured Products** — a sidebar box for products you're actively promoting (currently just Pep Tonic). The link goes straight to the affiliate offer page and is marked `rel="sponsored"`, which is what Google asks for on paid/affiliate links.
- **Latest Reviews grid** — every other article as a simple card: photo, title, one-line excerpt. No categories, no ratings, no filters — kept intentionally minimal.
- **Pagination** — the grid shows up to 9 cards (3 rows of 3) per page. `script.js` counts how many `.review-card` elements exist in the HTML and automatically builds page-number buttons if there are more than 9. You don't need to touch the JavaScript when you add new reviews — just add more `<article class="review-card">` blocks in `index.html` and the pagination adjusts itself.

There's no newsletter signup and no Privacy/Terms/Contact footer section right now, per your last round of edits. Add those back later if you decide you want a newsletter or need the legal pages (a live Privacy Policy is required before Google AdSense will approve the site).

---

## 3. What's already built for SEO

- **Unique `<title>` and `<meta description>`** on the homepage — write a new pair for every article page (155–160 characters max for the description).
- **Open Graph and Twitter Card tags** so links look right when shared on Facebook, X, WhatsApp, etc. — using `twitter:card = summary_large_image` and the featured article's 1200×630 cover image.
- **`rel="canonical"`** pointing to the live URL — update the domain once you buy one.
- **JSON-LD structured data**: a `WebSite` schema and an `ItemList` schema listing the four articles. When you build each article page, add a `Review` or `Article` schema block there too — this is what can make rich results appear in Google search.
- **Semantic HTML**: one `<h1>` per page, logical heading order, `<nav>`, `<main>`, `<footer>`.
- **Content is static, not JavaScript-generated** — every title, excerpt, and link lives directly in the HTML. JavaScript only handles pagination (showing/hiding groups of cards) and the mobile menu, so there's nothing for Google or Bing to miss during crawling.
- **`robots.txt`** and **`sitemap.xml`** — both required for Search Console / Bing Webmaster Tools submission.
- **Fully responsive**: the layout adapts at 880px (tablet) and 640px (mobile) — hero and grid stack to a single column, the header switches to a hamburger menu, and touch targets stay large enough to tap comfortably.

### Before you publish, still do this

1. If `reviewwise.com` isn't the domain you end up buying, replace every `https://www.reviewwise.com/` reference in `index.html`, `robots.txt`, and `sitemap.xml` with your real domain — this includes the new `og:image`/`twitter:image` paths pointing at `assets/images/why-does-energy-change-with-age.jpg`.
2. Write the excerpt copy for real once each article exists — the current excerpts are placeholders written from the titles alone, not from the published articles.
3. Add an FTC-compliant affiliate disclosure near the top of any article that reviews or links to Pep Tonic, not just in the footer — standard practice on US review sites and required by the FTC.
4. Submit `sitemap.xml` in both [Google Search Console](https://search.google.com/search-console) and [Bing Webmaster Tools](https://www.bing.com/webmasters) once the domain and the four article pages are live.

---

## 4. Deploying to GitHub Pages

1. Create a new GitHub repository (public).
2. Push these files to the repository root (or to a `/docs` folder — either works, just set it in the next step).
3. In the repo, go to **Settings → Pages**.
4. Under **Build and deployment → Source**, select **Deploy from a branch**, choose `main` and `/ (root)` (or `/docs`), then save.
5. Your site will be live at `https://your-username.github.io/repo-name/` within a few minutes.

### Connecting a custom domain

1. Buy a `.com` domain (Namecheap, Porkbun, Registro.br, etc.).
2. In your domain's DNS settings, add:
   - Four **A records** for the apex domain pointing to GitHub's IPs:
     ```
     185.199.108.153
     185.199.109.153
     185.199.110.153
     185.199.111.153
     ```
   - A **CNAME record** for `www` pointing to `your-username.github.io`.
3. Back in **Settings → Pages**, enter your custom domain in the "Custom domain" field and save — GitHub will create a `CNAME` file in your repo automatically.
4. Check **Enforce HTTPS** once GitHub finishes issuing the SSL certificate (can take up to 24 hours).
5. Update `index.html`, `robots.txt`, and `sitemap.xml` with the final domain, then commit and push again.

---

## 5. Adding a new article/review page

For each new article:

1. Use a descriptive, keyword-relevant filename: `reviews/article-title-here.html`.
2. Write a unique `<title>` and `<meta description>` targeting a real search phrase.
3. Add a `Review` or `Article` schema block with the relevant fields (`itemReviewed`, `reviewRating`, `author`, etc. for a product review).
4. Add the new page's URL to `sitemap.xml`.
5. Add a new `<article class="review-card">` block to the grid in `index.html`, following the same pattern as the three that are already there. Pagination in `script.js` picks it up automatically — no JavaScript changes needed.

---

## 6. Notes on the placeholder content

- The brand — name, tagline, and logo — is final.
- The four article titles and the Pep Tonic listing reflect your real content plan, but the excerpt text under each one is placeholder copy written only from the titles. Rewrite it once the actual articles exist, and be careful with health/anti-aging claims — the FTC and Google both scrutinize this niche, so keep language evidence-based and avoid promising specific results.
- The `Featured Products` link to Pep Tonic points directly to the vendor's page (`https://www.advancedbionutritionals.com/DS24/Pep-Tonic/First-Anti-Aging-Drink/HD.htm`). Swap this for your actual affiliate tracking link once you have one, keeping the `rel="sponsored"` attribute.
