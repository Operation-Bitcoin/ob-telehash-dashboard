# Configuration Guide

This dashboard is designed to run against a [HydraPool](https://github.com/256foundation/hydrapool) instance (or any Prometheus-compatible mining pool API). Before deploying, replace the following placeholders throughout the HTML files.

---

## Placeholders Reference

### Pool / Infrastructure

| Placeholder | Where | Description |
|---|---|---|
| `YOUR-POOL-DOMAIN` | All files | Your pool's public domain (e.g., `pool.yourdomain.io`) |

This appears in:
- API and WebSocket endpoint vars (`HYDRAPOOL_API`, `HYDRAPOOL_WS`, `PROM_BASE`)
- Stratum connection strings shown to miners
- OG/Twitter meta URL tags

### Donation Addresses

| Placeholder | Where | Description |
|---|---|---|
| `YOUR_ONCHAIN_DONATION_ADDRESS` | `index.html`, `overlay.html` | Bitcoin on-chain donation address (bc1q...) |
| `your-lightning-address@provider.com` | `index.html`, `overlay.html`, `monitor.html` | Lightning address for donations |

### External API Endpoints

The `overlay.html`, `teledash.html`, `jumbotron.html`, and `monitor.html` views use a set of external API endpoints for reading donation balances and delivering QR code images. These were built against a custom cache/proxy layer. You'll need to provide your own equivalents or remove these features.

| Placeholder | Description |
|---|---|
| `YOUR_LIGHTNING_API_ENDPOINT` | REST endpoint returning Lightning balance + payment list. Expected response: `{ total_money: <sats>, payments: [{ memo, date, amount }] }` |
| `YOUR_TELECACHE_API_ENDPOINT` | Endpoint returning combined chat + balance cache. Expected response: `{ users: [...], ... }` |
| `YOUR_TELEHASH_CACHE_API_ENDPOINT` | POST endpoint for telehash event donation data. Params: `{ address, dateStart }` |
| `YOUR_LIGHTNING_INV_CHECK_ENDPOINT` | POST endpoint to check invoice/payment status. Params: `{ address }` |

### QR Code / Image Endpoints

These views load QR code images and logos from remote endpoints (served as base64 text files). Replace with your own hosted assets or inline the base64 directly.

| Placeholder | Description |
|---|---|
| `YOUR_LIGHTNING_QR_ENDPOINT` | URL returning a base64-encoded WebP QR code for your Lightning address |
| `YOUR_ONCHAIN_QR_ENDPOINT` | URL returning a base64-encoded WebP QR code for your on-chain address |
| `YOUR_LOGO_ENDPOINT` | URL returning a base64-encoded WebP of your pool/org logo |
| `YOUR_VIDEO_PLACEHOLDER_ENDPOINT` | URL returning a base64-encoded WebP for the video placeholder image |

---

## Quick Start Checklist

- [ ] Set `HYDRAPOOL_API` and `HYDRAPOOL_WS` in `index.html`
- [ ] Set `PROM_BASE` in `teledash.html`, `jumbotron.html`, `monitor.html`
- [ ] Replace `YOUR_ONCHAIN_DONATION_ADDRESS` with your Bitcoin address
- [ ] Replace `your-lightning-address@provider.com` with your Lightning address
- [ ] Replace or remove the external API endpoint calls in the overlay views
- [ ] Replace the QR code image endpoints with your own
- [ ] Update `telehash-card-md26.html` stratum URLs and event details for your event
- [ ] Update `og:url` / `twitter:url` meta tags with your deployed URL
- [ ] Update the `manifest.json` name if desired

---

## Nostr Pool Identity

The dashboard resolves miner identities via Nostr npub. Set the pool's Nostr pubkey here:

```js
// index.html
const OB_POOL_PUBKEY = 'npub1...'; // your pool's Nostr public key
```

Miner worker format: `npub1yourid.workername`
