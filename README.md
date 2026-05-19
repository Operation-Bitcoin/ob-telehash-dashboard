# OB Telehash Dashboard

Real-time hashrate visualizer and mining dashboard for the **Operation Bitcoin Telehash** — a group mining event where participants donate hashrate to the mission.

Built on top of [Hashdash](https://github.com/dplusplus1024/hashdash) by [D++](https://github.com/dplusplus1024).

---

## What Is a Telehash?

A Telehash is a coordinated Bitcoin mining event hosted by Operation Bitcoin. Participants point their mining hardware at the OB pool for the duration of the event. Every hash mined is a direct contribution to the mission — educating veterans, service members, and their families about financial sovereignty through Bitcoin.

---

## Views

| File | Purpose |
|---|---|
| `index.html` | Main dashboard — full operator breakdown, hashrate charts, top contributors |
| `teledash.html` | Alternate live view |
| `jumbotron.html` | Large-screen display for events |
| `monitor.html` | Compact/pocket view |
| `overlay.html` | 1920×1080 stream overlay |
| `telehash-card-md26.html` | Print card template (Memorial Day 2026) |

---

## Setup

Static HTML — no build step required. Open any file directly in a browser, or serve with any static file server:

```bash
npx serve .
# or
python3 -m http.server 8080
```

### Configuration

Three values need to be updated when connecting to a live pool:

```js
// In index.html
const HYDRAPOOL_API = 'https://your-pool-endpoint/api';   // HydraPool API base URL
const HYDRAPOOL_WS  = 'wss://your-pool-endpoint/ws';      // HydraPool WebSocket URL
const OB_POOL_PUBKEY = 'npub1...';                         // Operation Bitcoin Nostr pubkey
```

---

## Pool Connection

During a Telehash event, miners connect to:

| Protocol | Endpoint |
|---|---|
| Stratum V1 | `stratum+tcp://YOUR-POOL-DOMAIN:23334` |

Worker format: `npub1yourid.minername`

---

## Stack

- Pure HTML/CSS/JS — no framework, no build tools
- [nostr-tools](https://github.com/nbd-wtf/nostr-tools) — Nostr profile resolution
- [Primal API](https://primal.net) — fast Nostr profile caching
- jQuery + Chart.js — UI + charts
- PWA-ready (service worker + manifest)
- Deployable on Vercel, GitHub Pages, or any static host

---

## Credits

- Original [Hashdash](https://github.com/dplusplus1024/hashdash) by [D++](https://github.com/dplusplus1024)
- [256 Foundation](https://256foundation.org) — HydraPool and open-source mining infrastructure
- [SHC](https://shc.io) — server infrastructure sponsor

---

## License

MIT — see [LICENSE](./LICENSE)
