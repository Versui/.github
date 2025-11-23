<div align="center">
  <img src="../logo.png" alt="Versui" width="200"/>

# VersUI

**Fully decentralized static site deployment. No gateways. No servers. No trust assumptions.**

[![Walrus](https://img.shields.io/badge/storage-Walrus-00C9FF?style=for-the-badge)](https://walrus.site)
[![Sui](https://img.shields.io/badge/chain-Sui-4DA2FF?style=for-the-badge)](https://sui.io)
[![Offline](https://img.shields.io/badge/offline-first-success?style=for-the-badge)](#)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg?style=for-the-badge)](LICENSE)

</div>

---

## What is VersUI?

VersUI deploys static websites to **Walrus decentralized storage** (100+ nodes) with metadata on **Sui blockchain**. Sites are served via **Service Workers** that fetch directly from Walrus aggregators - no centralized portals, no gateway dependencies.

**After the first load, sites work offline and fetch content peer-to-peer. Traditional hosting dies when servers die. VersUI sites self-heal.**

### The Stack

```
Storage Layer      → Walrus (100+ nodes, Byzantine fault-tolerant, erasure coding)
Coordination Layer → Sui blockchain (metadata, ownership, routing)
Access Layer       → Service Workers (browser-native, offline-first, direct fetch)
Privacy Layer      → Seal (encrypted private previews, team-only access)
```

**Result:** Censorship-resistant, offline-capable sites that survive infrastructure failures.

---

## Architecture

```
┌─────────────────────────────────────────────────────┐
│  deploy ./dist → walrus store → sui commit          │
│       ↓                                              │
│  bootstrap (< 3KB) → SW registers → direct fetch    │
│       ↓                                              │
│  offline-first · multi-aggregator · ∞ retry         │
└─────────────────────────────────────────────────────┘
```

**Bootstrap (< 3KB)**:
- Registers Service Worker on first visit
- SW intercepts all fetch requests
- Reads directly from Walrus aggregators (no middlemen)
- Exponential backoff retry (5s → 60s, infinite retry)
- Multi-aggregator failover for resilience
- Works completely offline after initial load

**No portals. No gateways. Pure decentralization.**

---

## Components

**Production Ready** ✅

- **[versui-cli](https://github.com/Versui/versui-cli)** - Deploy tool (v0.1.5, 85 tests, 84% coverage)
- **[versui-sw-plugin](https://github.com/Versui/versui-sw-plugin)** - Service Worker plugin (v0.1.0, 22 tests, 100% coverage)
- **[versui-move](https://github.com/Versui/versui-move)** - Sui Move contracts

---

## Technical Specs

- **Storage**: Walrus (100+ nodes, Byzantine fault-tolerant, erasure coding)
- **Metadata**: Sui blockchain (ownership, epochs, blob references)
- **Delivery**: Service Workers (browser-native proxy, no plugins required)
- **Bootstrap**: < 3KB HTML+SW (host anywhere - Vercel, S3, IPFS, HTTP server)
- **Security**: XSS escaping, SHA-256 content verification, offline-safe
- **Resilience**: Multi-aggregator failover, exponential backoff, auto-recovery
- **Privacy**: Seal encryption for private previews (team-only access with decrypt keys)
- **Decentralization**: Fully decentralized across all layers (storage, metadata, access)

---

## Usage

```bash
npm i -g @versui/cli
versui deploy ./dist
```

Bootstrap files output to `./bootstrap/` - host anywhere or use provided subdomain.

**Custom Service Worker integration:**

```js
import { create_versui_handler } from '@versui/sw-plugin'

const versui = create_versui_handler()
versui.load({ '/index.html': 'blob-id' })
self.addEventListener('fetch', e => versui.handle(e))
```

---

## Philosophy

**Centralized gateways are single points of failure and trust assumptions. Static sites don't need servers - they need blobs and pointers.**

VersUI combines four existing technologies:

- **Walrus** - Decentralized blob storage (100+ nodes, 1/3 fault tolerance, erasure coding)
- **Sui** - Fast blockchain (sub-second finality, on-chain metadata, ownership)
- **Service Workers** - Browser-native proxy (client-side routing, offline-first, since 2014)
- **Seal** - Privacy layer (encrypted storage for private previews, team-only access with decrypt keys)

**Remove centralized infrastructure. Sites become indestructible.**

The web was meant to be decentralized. VersUI brings it back.

---

<div align="center">

**Built for the sovereign web**

[![FOR THE BADGE](https://forthebadge.com/images/badges/made-with-javascript.svg)](https://forthebadge.com)
[![FOR THE BADGE](https://forthebadge.com/images/badges/open-source.svg)](https://forthebadge.com)

[CLI](https://github.com/Versui/versui-cli) • [SW Plugin](https://github.com/Versui/versui-sw-plugin) • [Move Contracts](https://github.com/Versui/versui-move)

</div>
