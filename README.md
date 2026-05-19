# OB Telehash Dashboard

Real-time hashrate visualizer and mining dashboard built for coordinated Bitcoin mining events (Telehashes). Tracks connected operators, live hashrate, and pool stats in real time.

Built on top of [Hashdash](https://github.com/dplusplus1024/hashdash) by [D++](https://github.com/dplusplus1024).

---

## What Is a Telehash?

A Telehash is a coordinated group mining event where participants point their hardware at a shared pool for a set period of time. Anyone can run one. The idea is simple: instead of mining solo or with a private pool, participants voluntarily redirect their hashrate to a common cause for the duration of the event. The dashboard tracks who is connected, how much hashrate they are contributing, and displays live stats for the group as a whole.

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

Dashboard: `https://YOUR-POOL-DOMAIN`

---

## Stack

- Pure HTML/CSS/JS with no framework and no build tools
- [nostr-tools](https://github.com/nbd-wtf/nostr-tools) for Nostr profile resolution
- [Primal API](https://primal.net) for fast Nostr profile caching
- jQuery and Chart.js for UI and charts
- PWA ready with service worker and manifest
- Deployable on Vercel, GitHub Pages, or any static host

---

## Credits

- Original [Hashdash](https://github.com/dplusplus1024/hashdash) by [D++](https://github.com/dplusplus1024)
- [256 Foundation](https://256foundation.org) — HydraPool and open-source mining infrastructure
- [SHC](https://shc.io) — server infrastructure sponsor

---

## License

MIT — see [LICENSE](./LICENSE)
