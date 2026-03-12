# Google Search Console – Indexing Notes

Your sitemap and canonicals are correct (all URLs use `https://serenemindspsychotherapy.com/` with **no www**). The remaining indexing issues are fixed by **server/hosting configuration** and GSC actions.

---

## 1. Not found (404) – 2 pages

**URLs:**  
`http://www.serenemindspsychotherapy.com/`  
`https://www.serenemindspsychotherapy.com/`

**Cause:** The **www** version of the site is not set up (or not redirecting), so Google gets a 404 when it tries those URLs.

**Fix (on your host/server):**

- Add **301 redirects** so that:
  - `http://www.serenemindspsychotherapy.com/*` → `https://serenemindspsychotherapy.com/*`
  - `https://www.serenemindspsychotherapy.com/*` → `https://serenemindspsychotherapy.com/*`
- Or configure the **www** host so it serves the same site and then redirect to the non-www URL.

Do this in your hosting control panel (cPanel, Plesk, Netlify, Vercel, etc.) or via `.htaccess` / Nginx config. After it’s live, in GSC use **Validate fix** for the “Not found (404)” report.

---

## 2. Crawled – currently not indexed (1 page)

**URL:**  
`http://serenemindspsychotherapy.com/` (HTTP, no www)

**Cause:** Google crawled the **HTTP** URL. Your pages already have a canonical to `https://serenemindspsychotherapy.com/`, which is correct.

**Fix:**

- On the server, add a **301 redirect**: `http://serenemindspsychotherapy.com/*` → `https://serenemindspsychotherapy.com/*`.
- After that, you can click **Validate fix** in GSC for “Crawled - currently not indexed” if it’s still shown.

---

## 3. Discovered – currently not indexed (13 pages)

**Cause:** Google knows about these URLs (from sitemap or links) but hasn’t indexed them yet. One of the examples was the old URL `insurance-pricing.html`, which no longer exists (replaced by `pricing.html`).

**Fixes:**

1. **Old URL `insurance-pricing.html`**  
   On the server, add a **301 redirect**:  
   `https://serenemindspsychotherapy.com/insurance-pricing.html` → `https://serenemindspsychotherapy.com/pricing.html`  
   So any old links or sitemap cache point to the correct page.

2. **Other “Discovered - currently not indexed” URLs**  
   - In GSC, open **URL Inspection**, enter the important URLs (e.g. homepage, about, contact, pricing), and use **Request indexing**.
   - Re-submit the sitemap: **Sitemaps** → submit `sitemap.xml` (or `https://serenemindspsychotherapy.com/sitemap.xml`).
   - Indexing can take days or weeks; “Discovered - currently not indexed” often means Google will index when it recrawls.

---

## Checklist

- [ ] 301 redirect: **www** → **non-www** (http and https).
- [ ] 301 redirect: **http** → **https** (non-www).
- [ ] 301 redirect: **insurance-pricing.html** → **pricing.html**.
- [ ] In GSC, confirm the **property** is `https://serenemindspsychotherapy.com` (no www).
- [ ] Resubmit **sitemap**: `https://serenemindspsychotherapy.com/sitemap.xml`.
- [ ] Use **URL Inspection** + **Request indexing** for key pages (home, about, contact, services, pricing, blog).
- [ ] After redirects are live, use **Validate fix** for the 404 and “Crawled - currently not indexed” issues.

Your sitemap already uses only **https** and **no www**; no sitemap changes are required for the 404 or redirect issues.
