# Boost Social — deploy to GitHub Pages (public repo)

Live domain for now: **boostsocial.marketing** (you'll switch to **boostsocial.agency** later — steps for that are at the bottom). Site URLs are on `.marketing`; the brand email stays `hello@boostsocial.agency` throughout.

The whole folder **is** the live site — 14 pages. Put it in a public GitHub repo and turn on Pages.

## The site — keep the folder structure intact

```
index.html                          the homepage (static, crawlable, schema baked in)
og-image.png                        link-preview image (1200×630)
robots.txt                          opens the site to Google + all major AI crawlers
sitemap.xml                         lists all 14 pages
llms.txt                            summary + page list for AI models
CNAME                               your custom domain (boostsocial.marketing)
.nojekyll                           stops GitHub reprocessing the files

social-media-management/  social-media-advertising/  email-newsletters/
get-found-by-ai/  website-design/                    ← 5 service pages
social-media-for-restaurants/  social-media-for-cafes/
social-media-for-hotels/  social-media-for-bars/     ← 4 hospitality pages
pricing/  about/  faq/  contact/                      ← 4 company pages
```

Each folder has its own `index.html` and serves at a clean URL (e.g. `boostsocial.marketing/pricing/`). **Don't flatten the folders** or the URLs break.

## Steps

1. **Create a public repo** under `thewondergroup`, e.g. `boost-social`.
2. **Upload the whole unzipped folder**, preserving the subfolders (drag-and-drop in the GitHub web UI works; make sure `.nojekyll` and the page subfolders come across).
3. **Settings → Pages → Source: Deploy from a branch → `main` / `/root` → Save.**
4. GitHub reads the `CNAME` file and sets `boostsocial.marketing` automatically. Tick **Enforce HTTPS** once it appears.
5. **Point your DNS** at GitHub (at your `.marketing` registrar):

   **Apex** (`boostsocial.marketing`) — four A + four AAAA records:
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

DNS takes a few minutes to a few hours. Then `https://boostsocial.marketing` is live.

## The moment it's live

1. **Google Search Console** → add `boostsocial.marketing` → submit `sitemap.xml`.
2. **Bing Webmaster Tools** → add the site → submit the sitemap. (Bing powers ChatGPT search.)
3. **Rich Results test** ([search.google.com/test/rich-results](https://search.google.com/test/rich-results)) → paste home, a service page, `/faq/`.
4. Set up a **Google Business Profile**.

## What's already handled

- 14 fully-crawlable pages (all content renders with JavaScript off).
- Per-page SEO: unique title, meta description, Open Graph/Twitter cards, schema.org structured data (Service + Offer, FAQPage, Breadcrumbs).
- All cross-linked; sitemap + `llms.txt` list all 14 URLs. 390 internal links checked, zero broken.
- `robots.txt` welcomes GPTBot, ClaudeBot, PerplexityBot, Google-Extended, Applebot and more.

---

## ⭐ When you switch to boostsocial.agency later

Moving domains is straightforward but you must do it properly, or you lose the search ranking you've built on `.marketing`. The key is telling Google the site **moved** (301 redirects), rather than just letting `.marketing` go dark.

1. **Regenerate the site on `.agency`.** Send me the word and I'll rebuild the whole package on `boostsocial.agency` in one pass (canonical tags, OG, sitemap, `CNAME`, `llms.txt` — all of it). Deploy that to the repo.
2. **Keep `.marketing` alive and redirect it.** Don't cancel the `.marketing` domain. Point it at the `.agency` site with **301 (permanent) redirects**, path-for-path — `boostsocial.marketing/pricing/` → `boostsocial.agency/pricing/`, and so on. On GitHub Pages the simplest way is a second small repo for `.marketing` that redirects; I can generate that for you.
3. **Search Console "Change of Address."** In Google Search Console, add `boostsocial.agency`, verify it, then use **Settings → Change of address** on the `.marketing` property to point Google to the new domain. Do the equivalent in Bing.
4. **Resubmit** the `.agency` sitemap in both, and update the domain anywhere you've listed it (Google Business Profile, social bios, ads).
5. **Leave the redirects up for at least a year** so every old link and crawler follows through to `.agency`.

Because the email is already `hello@boostsocial.agency`, nothing on that side changes when you switch.

> If avoiding this migration appeals, the alternative is to launch on `.agency` from the start and simply redirect `.marketing` → `.agency` from day one. Either works — just say which and I'll build it.
