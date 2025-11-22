<div align="center">
  <img src="../logo.png" alt="Versui" width="200"/>

# VersUI

**Stateless hosting substrate. No gateways. No servers.**

[![FOR THE BADGE](https://forthebadge.com/images/badges/built-with-love.svg)](https://forthebadge.com)
[![FOR THE BADGE](https://forthebadge.com/images/badges/powered-by-black-magic.svg)](https://forthebadge.com)

[![Walrus](https://img.shields.io/badge/storage-Walrus-00C9FF?style=for-the-badge)](https://walrus.site)
[![Sui](https://img.shields.io/badge/chain-Sui-4DA2FF?style=for-the-badge)](https://sui.io)
[![Offline](https://img.shields.io/badge/offline-first-success?style=for-the-badge)](#)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg?style=for-the-badge)](LICENSE)

</div>

---

## Axioms

```
Gateway = centralization = defeat
Service Worker = client-side proxy = freedom
Walrus (100+ nodes) + Sui (sub-second finality) + Service Workers = indestructible
```

Traditional hosting dies when servers die. VersUI sites **self-heal**.

---

## Architecture

```
┌─────────────────────────────────────────────────────┐
│  deploy ./dist → walrus store → sui commit          │
│       ↓                                              │
│  bootstrap (2KB) → SW registers → direct fetch      │
│       ↓                                              │
│  offline-first · multi-aggregator · ∞ retry         │
└─────────────────────────────────────────────────────┘
```

**Bootstrap (< 3KB)**:
- Registers SW on first visit
- SW intercepts all fetches
- Direct reads from Walrus aggregators (no middlemen)
- Exponential backoff (5s→60s, ∞ retry)
- Multi-aggregator failover
- Works offline after first load

**No portals. No gateways. No trust assumptions.**

---

## Components

**Production Ready** ✅

- **[versui-cli](https://github.com/Versui/versui-cli)** - Deploy tool (v0.1.5, 85 tests, 84% coverage)
- **[versui-sw-plugin](https://github.com/Versui/versui-sw-plugin)** - Custom SW integration (v0.1.0, 22 tests, 100% coverage)
- **[versui-move](https://github.com/Versui/versui-move)** - Sui Move contracts (deployed on testnet)

**Planned** 📝

- **[versui-platform](https://github.com/Versui/versui-platform)** - Managed dashboard & API (docs only, not implemented)

---

## Specs

- **Storage**: Walrus (100+ nodes, Byzantine fault-tolerant, erasure coding)
- **Metadata**: Sui blockchain (ownership, epochs, blob refs)
- **Delivery**: Service Workers (browser-native proxy, no plugins)
- **Bootstrap**: < 3KB HTML+SW (self-hosting ready)
- **Security**: XSS escaping, SHA-256 verification, offline-safe
- **Resilience**: Multi-aggregator failover, exponential backoff, auto-recovery
- **Decentralization**: Fully decentralized (storage + metadata + access layer)

---

## Usage

```bash
npm i -g @versui/cli
versui deploy ./dist
```

Output:
```
✅ Site deployed!
🌐 URL: https://abc123.versui.app
📦 Object ID: 0xdef456...
```

Bootstrap outputs to `./bootstrap/` - host anywhere (Vercel, S3, IPFS, HTTP server, or use versui.app subdomain).

**Custom Service Worker integration:**

```js
import { create_versui_handler } from '@versui/sw-plugin'

const versui = create_versui_handler()
versui.load({ '/index.html': 'blob-id' })
self.addEventListener('fetch', e => versui.handle(e))
```

---

## Philosophy

**Gateways are trust assumptions. Static sites don't need servers. They need blobs + pointers.**

```
Walrus = blob availability (100+ nodes, 1/3 fault tolerance, erasure coding)
Sui = metadata coordination (sub-second finality, on-chain ownership)
Service Workers = client-side routing (browsers had this since 2014)
```

Combine all three. Remove servers. Remove gateways. Sites become **indestructible**.

**The web was meant to be decentralized. VersUI brings it back.**

---

<div align="center">

**Built for the sovereign web**

[![FOR THE BADGE](https://forthebadge.com/images/badges/made-with-javascript.svg)](https://forthebadge.com)
[![FOR THE BADGE](https://forthebadge.com/images/badges/open-source.svg)](https://forthebadge.com)

[CLI](https://github.com/Versui/versui-cli) • [SW Plugin](https://github.com/Versui/versui-sw-plugin) • [Move Contracts](https://github.com/Versui/versui-move) • [Platform](https://github.com/Versui/versui-platform)

</div>
