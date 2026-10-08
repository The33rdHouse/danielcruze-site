# Cloudflare + Wrangler GitHub Deploy

Account ID: `6a44e3cb01797044f56d2bfd68550463`

## GitHub secrets (this repo)
- `CLOUDFLARE_ACCOUNT_ID` — account id above
- `CLOUDFLARE_API_TOKEN` — Account API Token with:
  - Account → Cloudflare Pages → Edit
  - Account → Workers Scripts → Edit
  - User → User Details → Read (optional; for verify)
  - Zone → DNS → Edit (only after zones are on Cloudflare)

Create at: https://dash.cloudflare.com/profile/api-tokens → **Create Token** → **Edit Cloudflare Workers** template → scope to this account → copy the token **once** (raw string only).

## Domains (planned)
| Domain | Current DNS | Target |
|--------|-------------|--------|
| danielcruze.com | Namecheap / hosting IP | Cloudflare zone → Pages custom domain |
| www.danielcruze.com | NXDOMAIN | CNAME → Pages |
| 33rdhouse.com / the33rdhouse.com | NXDOMAIN | Add zones when ready |
| aibhubofficial.com | Squarespace IPs | Cloudflare + Pages or redirect Worker |
| digitalcompanionship.com | parking/misc | Cloudflare + Pages or redirect Worker |
| danielcruze.store | 404 app | Optional redirect Worker → /books or Beacons |

## Workflow
The workflow `.github/workflows/cloudflare-pages.yml` is **not committed in this repository**. The Wrangler configuration does not itself deploy anything. Confirm the live Cloudflare Pages project, its Git integration, account permissions and custom domains before changing DNS. See `DOMAIN-RECOVERY.md`.
