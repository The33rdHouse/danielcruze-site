# danielcruze.com — Domain recovery runbook (2026-10-08)

## Verified scope
- GitHub contains a standalone static HTML website with a `main` branch and `wrangler.toml` configured for Cloudflare Pages.
- The GitHub repository is **not evidence of a live deployment**; the repository tree contains no GitHub Actions workflow.
- Public web fetch of `https://danielcruze.com/` redirected into a Shopify customer-account authentication flow at inspection; `www` and `shop` were not reliably accessible to the browser tool. Exact DNS records and hosting ownership are not verified.
- Canonical business architecture in Google Drive: `danielcruze.com` = public authority website, `shop.danielcruze.com` = commerce, 33rd House = separate teaching ecosystem.

## Preflight — capture before changing anything
1. Export current DNS zone, registrar nameservers, all existing A/AAAA/CNAME/TXT/MX/CAA records and TTLs. **Preserve email MX/SPF/DKIM/DMARC records.**
2. Verify the existing Cloudflare Pages project `danielcruze-site` and its deployed URL in the correct account. Check a live preview with `/`, `/books/`, `/social.html`, `/contact/`, mobile navigation and HTTPS.
3. Check Shopify Settings → Domains and record the active store's primary domain and any redirects. Identify which storefront owns existing buyers, accounts and checkout. Do not remove a domain until the commerce subdomain is tested.
4. Back up production configuration and capture the previous deployment ID for rollback.

## Ordered production cutover — only after preflight verification
1. Attach `danielcruze.com` and `www.danielcruze.com` to the **existing** Cloudflare Pages project through Pages → Custom domains; follow exactly the ownership validation and DNS targets shown by the provider. Do not invent IP or CNAME targets.
2. Connect `shop.danielcruze.com` to the existing Shopify store (Settings → Domains), using Shopify's current verification/DNS requirements, and confirm storefront checkout and customer sign-in.
3. Once the shop subdomain works and a backup exists, move the public apex/www routing away from Shopify to Pages without disturbing mail records. Confirm domain ownership and HTTPS certificates.
4. Redirect www → apex (or select one consistent canonical host); verify no login redirect on the homepage. Test deep links, buttons, mobile menu, static assets, search metadata and payment URLs with approved test methods.
5. Publish social links only after exact destination URLs respond successfully. Do not send visitors to absent /journal, /for-men, /for-women or /for-couples pages.

## Rollback
Restore recorded DNS and Shopify domain state from the preflight exports if TLS, store access or primary website fail. Keep prior deployment available, and do not change or rotate credentials as a troubleshooting shortcut.

## Out of scope for this code PR
Live DNS changes, Cloudflare or Shopify settings, payments, membership activation and the separate Expo app. Those changes require platform access and direct verification.
