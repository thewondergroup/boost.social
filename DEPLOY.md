# Boost Social — deploy to GitHub Pages (public repo)

The whole folder **is** the live site — 14 pages. Put it in a public GitHub repo and turn on Pages. Nothing in a static marketing site is sensitive (the HTML is public on the live site regardless), so public + free is the simplest route.

## The site — keep the folder structure intact

```
index.html                          the homepage (static, crawlable, schema baked in)
og-image.png                        link-preview image (1200×630)
robots.txt                          opens the site to Google + all major AI crawlers
sitemap.xml                         lists all 14 pages
llms.txt                            summary + page list for AI models
CNAME                               your custom domain (boostsocial.agency)
.nojekyll                           stops GitHub reprocessing the files

social-media-management/  social-media-advertising/  email-newsletters/
get-found-by-ai/  website-design/                    ← 5 service pages
social-media-for-restaurants/  social-media-for-cafes/
social-media-for-hotels/  social-media-for-bars/     ← 4 hospitality pages
pricing/  about/  faq/  contact/                      ← 4 company pages
```

Each folder has its own `index.html` and serves at a clean URL (e.g. `boostsocial.agency/pricing/`). **Don't flatten the folders** or the URLs break.

## Steps

1. **Create a public repo** under `thewondergroup`, e.g. `boost-social`.
2. **Upload the whole unzipped folder**, preserving the subfolders (drag-and-drop in the GitHub web UI works; make sure `.nojekyll` and the page subfolders come across).
3. **Settings → Pages → Build and deployment → Source: Deploy from a branch → `main` / `/root` → Save.**
4. GitHub reads the `CNAME` file and sets the custom domain automatically. Tick **Enforce HTTPS** once it appears (a few minutes).
5. **Point your DNS** at GitHub (at your `.agency` registrar):

   **Apex** (`boostsocial.agency`) — four A + four AAAA records:
   ```
   A     @   185.199.108.153
   A     @   185.199.109.153
   A     @   185.199.110.153
   A     @   185.199.111.153
   AAAA  @   2606:50c0:8000::153
   AAAA  @   2606:50c0:8001::153
   AAAA  @   2606:50c0:8002::153
   AAAA  @   2606:50c0:8003::153
   ```
   **www** — a CNAME record:
   ```
   CNAME  www   thewondergroup.github.io
   ```

DNS takes a few minutes to a few hours. Then `https://boostsocial.agency` is live.

## The moment it's live — do these (this is what actually gets you found)

1. **Google Search Console** (search.google.com/search-console) → add `boostsocial.agency` → submit `sitemap.xml`.
2. **Bing Webmaster Tools** (bing.com/webmasters) → add the site → submit the sitemap. **Bing powers ChatGPT search**, so this one matters for AI visibility.
3. **Rich Results test** ([search.google.com/test/rich-results](https://search.google.com/test/rich-results)) → paste a few URLs (home, a service page, `/faq/`). You should see Organization, Service and FAQ detected.
4. Set up a **Google Business Profile** for local presence.

## What's already handled

- **14 fully-crawlable pages** — all content renders with JavaScript off, so AI crawlers (which mostly don't run JS) read everything.
- **Per-page SEO** — unique title, meta description, Open Graph/Twitter cards and schema.org structured data (Service + Offer, FAQPage, Breadcrumbs) on every page.
- **All cross-linked** — homepage → every page, pages → each other; sitemap + `llms.txt` list all 14 URLs. (390 internal links checked, zero broken.)
- **AI crawlers welcomed** — `robots.txt` allows GPTBot, ClaudeBot, PerplexityBot, Google-Extended, Applebot and more.

## Still to wire (next step, not blocking launch)

- **Real checkout** — the "Get started" / "Choose…" buttons currently open a pre-filled email to `hello@boostsocial.agency` so you capture leads. Next step is Stripe Payment Links so people can subscribe directly.
- **Real testimonials & case studies** — swap the sample quotes for real ones; add case-study pages when you have results (strongest trust + SEO asset).

## If you ever want it private later
Keep the repo private and publish via **Cloudflare Pages** or **Netlify** (both free from a private repo, custom domain included) — or upgrade to **GitHub Pro** to keep private repos on GitHub Pages. Worth doing only once there's something in the repo you don't want public (unpublished pages, internal notes, API keys).
