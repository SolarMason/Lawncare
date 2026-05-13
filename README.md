# NEPA-PRO Lawn Care — PWA Deployment Package

A self-contained Progressive Web App for **lawncare.nepa-pro.com**. Native iOS UI/UX feel, full SEO/AI search optimization, Stripe-wired pricing for 16 recurring tiers + 4 seasonal add-ons.

## File layout

```
/
├── index.html              # Main app (single-file SPA, no build step)
├── manifest.json           # PWA manifest
├── service-worker.js       # Offline shell + cache strategy
├── sitemap.xml             # Search engine sitemap
├── robots.txt              # Bots + AI crawlers allowed
├── llms.txt                # AI/LLM-readable summary
├── PRICING_LOGIC.md        # Profit math reference (NOT deployed)
└── assets/
    ├── icon-180.png
    ├── icon-192.png
    ├── icon-512.png
    ├── icon-maskable-512.png
    ├── apple-touch-icon.png
    ├── favicon-16.png
    ├── favicon-32.png
    ├── og-image.png        # 1200×630 social card with embedded QR
    ├── og-image.jpg        # JPEG fallback
    ├── qr.svg              # Vector QR (lawncare.nepa-pro.com)
    └── qr.png              # Raster QR
```

## Deploy

This is plain static HTML — drop it on any host that supports HTTPS:

**Option A — Cloudflare Pages** (recommended, free, fast)
1. New project → Direct Upload
2. Drag the folder
3. Custom domain → `lawncare.nepa-pro.com` → follow CNAME instructions
4. Done

**Option B — GitHub Pages**
1. Push this folder to a repo, set Pages source to `main`
2. Add `lawncare.nepa-pro.com` as custom domain
3. Add a CNAME record `lawncare` → `<username>.github.io`

**Option C — Any static host** (Netlify, Vercel, S3+CloudFront, Wix Static)
- Required headers: `Content-Type: text/html` for `.html`, `application/json` for `manifest.json`
- Service worker MUST be served from `/service-worker.js` at the root (not under a path)

## DNS

Add this record at the `nepa-pro.com` DNS panel:

```
CNAME   lawncare   <host-target>
```

## Verify after deploy

1. **HTTPS active** — required for PWA + service worker
2. **PWA score** — Chrome DevTools → Lighthouse → "Installable" check
3. **Stripe links work** — click "Book →" on any tier; you should land on the Stripe checkout page
4. **OG card** — paste `https://lawncare.nepa-pro.com/` into iMessage / Facebook / LinkedIn debugger → the 1200×630 card should appear with QR code
5. **QR code** — scan the QR with iPhone/Android camera → opens lawncare.nepa-pro.com
6. **Schema.org** — run `https://lawncare.nepa-pro.com/` through Google's [Rich Results Test](https://search.google.com/test/rich-results) — should detect `HomeAndConstructionBusiness`, `Service`, `FAQPage`

## Stripe reference

All products, prices, and payment links live in your Stripe account. Live mode confirmed (URLs use `secure.nepa-pro.com` — your branded checkout domain).

### Products

| Product | ID |
|---|---|
| Small Yard | `prod_UViwAm4h7FOuOs` |
| Medium Yard | `prod_UViwsWQqEgbrEJ` |
| Large Yard | `prod_UViwGfwMGMt8C3` |
| XL Yard | `prod_UViwXQXtICAtRO` |
| Spring Cleanup | `prod_UVixUcFmTZclfV` |
| Fall Cleanup | `prod_UVixibG7dCuo13` |
| Aeration & Overseed | `prod_UVix2qDSPOUH6d` |
| Hedge Trimming | `prod_UVixgw4g40UtsT` |

### Payment links

Small Yard:
- Weekly $40 — https://secure.nepa-pro.com/b/4gM5kD6W1b1N2tLd0h2cg2A
- Bi-Weekly $45 — https://secure.nepa-pro.com/b/dRmbJ1805d9V2tL9O52cg2B
- Monthly $55 — https://secure.nepa-pro.com/b/eVqcN5bch0n92tLbWd2cg2C
- One-Time $70 — https://secure.nepa-pro.com/b/bJeaEX8051rd0lDbWd2cg2D

Medium Yard:
- Weekly $60 — https://secure.nepa-pro.com/b/28E28r6W19XJ8S90dv2cg2E
- Bi-Weekly $70 — https://secure.nepa-pro.com/b/00weVd0xD4Dpect2lD2cg2F
- Monthly $85 — https://secure.nepa-pro.com/b/dRm14n805edZ9Wd7FX2cg2G
- One-Time $105 — https://secure.nepa-pro.com/b/eVqcN51BH0n96K18K12cg2H

Large Yard:
- Weekly $85 — https://secure.nepa-pro.com/b/aFafZhfsxedZfgx6BT2cg2I
- Bi-Weekly $100 — https://secure.nepa-pro.com/b/cNicN52FLb1N0lD7FX2cg2J
- Monthly $120 — https://secure.nepa-pro.com/b/9B628r0xD7PBgkBgct2cg2K
- One-Time $145 — https://secure.nepa-pro.com/b/7sY3cv5RX3zl2tL6BT2cg2L

XL Yard:
- Weekly $115 — https://secure.nepa-pro.com/b/8x24gza8d8TFc4ld0h2cg2M
- Bi-Weekly $130 — https://secure.nepa-pro.com/b/5kQ28r3JP8TF7O5gct2cg2N
- Monthly $160 — https://secure.nepa-pro.com/b/14AbJ13JP4Dp0lD4tL2cg2O
- One-Time $195 — https://secure.nepa-pro.com/b/bJe4gz6W19XJb0haS92cg2P

Add-ons:
- Spring Cleanup $295 — https://secure.nepa-pro.com/b/fZucN5gwB3zl3xP9O52cg2Q
- Fall Cleanup $295 — https://secure.nepa-pro.com/b/5kQfZh6W1c5R4BT0dv2cg2R
- Aeration & Overseed $225 — https://secure.nepa-pro.com/b/00weVd4NT2vh2tL4tL2cg2S
- Hedge Trimming $95 — https://secure.nepa-pro.com/b/6oU5kDcgl9XJect8K12cg2T

## Editing prices later

The HTML keeps all pricing in one JS object at the top of the script block (`const PACKAGES = [...]`). To change a price:

1. Update the price in Stripe (create new Price → archive old one; or just update the link)
2. Update the `amount` and `url` in the `PACKAGES` array
3. Re-deploy (`index.html` is the only file that needs to change)

The JSON-LD `Offer` block near the top of `<head>` should also be updated to match (it's what Google reads for product rich results).

## What this scores

- **SEO**: Comprehensive meta tags, canonical, og:*, twitter:*, JSON-LD LocalBusiness + Service + FAQPage, sitemap.xml, robots.txt with all major bots whitelisted, semantic HTML5, alt text everywhere, mobile-first viewport with safe-area handling, fast (single file, inline CSS, no blocking JS).
- **AI/LLM search**: llms.txt summary, FAQ structured data, plain-language Q&A copy, ClaudeBot/GPTBot/PerplexityBot all explicitly allowed.
- **PWA**: Standalone display, maskable icons, theme color, shortcuts, install prompt UI, service worker with offline shell, beforeinstallprompt handled.
- **iOS native feel**: SF Pro font stack (`-apple-system`), backdrop-blur top bar, segmented control for frequency picker, safe-area-inset padding, pill buttons, accordion FAQ, tap haptic-style press states.
- **Profit**: every pricing cell verified to net ≥$65/hr after overhead (lowest is $70.41/hr — see `PRICING_LOGIC.md`).

## Customer support flow

The Stripe checkout you generate sends each customer a billing portal link in every email — they self-serve to update card, change plan, or cancel. No support burden on you for those.

For service questions (rescheduling, gate codes, complaints) the customer texts 570-677-7971. That's it.
