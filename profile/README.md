<p align="center">
  <img src="../logo.png" alt="Versui logo" width="200">
</p>
<h1 align=center>Versui</h1>
<p align=center>
  <img src="https://img.shields.io/badge/Walrus-00C9FF?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48cmVjdCB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIGZpbGw9IndoaXRlIi8+PC9zdmc+&logoColor=white" />
  <img src="https://img.shields.io/badge/Sui-4DA2FF?style=for-the-badge&logo=sui&logoColor=white" />
  <img src="https://img.shields.io/badge/Service_Workers-000000?style=for-the-badge&logo=javascript&logoColor=white" />
  <img src="https://img.shields.io/badge/License-Apache_2.0-blue?style=for-the-badge" />
</p>
<h3 align=center>Decentralized static site hosting on Walrus + Sui with zero infrastructure dependencies</h3>

---

## What It Does

Versui deploys static websites to decentralized infrastructure with no gateways, no servers, and no trust assumptions. Content lives on Walrus (100+ node storage network), metadata on Sui blockchain, and sites load via browser-native Service Workers.

- Zero-config deployment with interactive CLI
- Non-custodial (your keys never leave your machine)
- Service Worker bootstrap for self-hosting
- Deterministic Site IDs with derived objects (no RPC lookups)
- Immutable site names with transferrable ownership

## Architecture

```
┌───────────────────────────────────────────────────┐
│  CLI: versui deploy ./dist                        │
│    ↓                                               │
│  Walrus: Store files (100+ nodes, erasure coded)  │
│    ↓                                               │
│  Sui: Commit metadata (Site + AdminCap objects)   │
│    ↓                                               │
│  Bootstrap: 3KB HTML + Service Worker              │
│    ↓                                               │
│  Browser: SW fetches directly from Walrus          │
│    → Multi-aggregator failover                     │
│    → Exponential backoff + infinite retry          │
│    → Works offline after first load                │
└───────────────────────────────────────────────────┘
```

**No portals. No gateways. Pure decentralization.**

## Components

### Production Ready

| Package | Version | Purpose | Repository |
|---------|---------|---------|------------|
| **versui-cli** | v1.6.2 | Deploy static sites to Walrus + Sui | [GitHub](https://github.com/Versui/versui-cli) |
| **versui-sw-plugin** | v0.1.3 | Service Worker plugin for Walrus fetch | [GitHub](https://github.com/Versui/versui-sw-plugin) |
| **versui-move** | testnet | Sui Move smart contracts | [GitHub](https://github.com/Versui/versui-move) |

### Smart Contracts (Testnet)

**Package ID:** `0x2489609d5e6b754634d4ca892ab259222482f31596a13530fcc8110b5b2461cb`

**Features:**
- Derived objects for deterministic Site IDs (zero RPC lookups)
- Immutable site names with transferrable ownership (AdminCap pattern)
- Resource management with Blake2b content verification
- Custom domain mapping with security protections (cooldown, punycode blocking)
- No treasury, no favicon_url (removed in latest refactor)

## Quick Start

```bash
# Install CLI
npm install -g @versui/cli

# Deploy your site
versui deploy ./dist

# Output: bootstrap/ folder (host anywhere)
```

Bootstrap files can be hosted on any static host (Vercel, S3, IPFS, HTTP server). The Service Worker handles all content fetching from Walrus.

### Custom Service Worker Integration

```javascript
import { create_versui_handler } from '@versui/sw-plugin'

const versui = create_versui_handler()
versui.load({ '/index.html': 'blob-id' })
self.addEventListener('fetch', e => versui.handle(e))
```

## Technical Specs

| Layer | Technology | Details |
|-------|-----------|---------|
| **Storage** | Walrus | 100+ nodes, Byzantine fault-tolerant, erasure coding |
| **Coordination** | Sui | Sub-second finality, on-chain metadata, ownership via capabilities |
| **Delivery** | Service Workers | Browser-native proxy, offline-first, no plugins required |
| **Bootstrap** | Static HTML + SW | < 3KB, host anywhere |
| **Security** | XSS escaping, SHA-256 verification | Content integrity guaranteed |
| **Resilience** | Multi-aggregator failover | Exponential backoff, auto-recovery on renewal |

## Philosophy

**Centralized gateways are single points of failure and trust assumptions.**

Versui combines battle-tested technologies:
- **Walrus** - Decentralized blob storage (1/3 fault tolerance)
- **Sui** - Fast blockchain (ownership + metadata)
- **Service Workers** - Browser-native routing (since 2014)

**Result:** Sites that survive infrastructure failures, censorship attempts, and service outages. The web was meant to be decentralized - Versui brings it back.

## Documentation

- [CLI Usage Guide](https://github.com/Versui/versui-cli#readme)
- [Service Worker Plugin API](https://github.com/Versui/versui-sw-plugin#readme)
- [Smart Contract Reference](https://github.com/Versui/versui-move#readme)

## License

[Apache 2.0](LICENSE)

---

<div align="center">

**Built for the sovereign web**

[CLI](https://github.com/Versui/versui-cli) • [SW Plugin](https://github.com/Versui/versui-sw-plugin) • [Move Contracts](https://github.com/Versui/versui-move)

</div>
