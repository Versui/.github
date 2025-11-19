<div align="center">
  <img src="../logo.png" alt="Versui Logo" width="300"/>

  # Versui

  **Vercel for Walrus - Deploy static sites with one command**

  [![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg?style=flat-square)](https://github.com/Versui/versui-cli/blob/main/LICENSE)
  [![Powered by Walrus](https://img.shields.io/badge/powered%20by-Walrus%20🦭-00C9FF?style=flat-square)](https://walrus.site)
  [![Built on Sui](https://img.shields.io/badge/built%20on-Sui%20⚡-4DA2FF?style=flat-square)](https://sui.io)
  [![Offline First](https://img.shields.io/badge/offline-first%20📴-success?style=flat-square)](https://github.com/Versui/versui-cli)
  [![No Gateways](https://img.shields.io/badge/no-gateways%20🚫-red?style=flat-square)](https://github.com/Versui/versui-cli)

</div>

---

## What is Versui?

**Versui** is a deployment platform built for **Walrus** (decentralized blob storage) and **Sui** blockchain. Think **Vercel**, but native to the Walrus/Sui ecosystem.

**Why Walrus + Sui?**
- 🦭 **Walrus**: Decentralized storage (100+ nodes, 1/3 fault tolerance, red-stuffing erasure coding)
- ⚡ **Sui**: Lightning-fast finality, low fees, perfect for metadata coordination
- 🚀 **Ecosystem-native**: First-class SuiNS integration, Sui wallet auth, WAL token support

**Two ways to use Versui**:

1. **[versui.app](https://versui.app)** - Managed platform (drag-and-drop, custom domains, analytics)
2. **[versui-cli](https://github.com/Versui/versui-cli)** - Open source CLI (zero lock-in, self-hosting)

**The killer feature**: Service workers make your site work **offline** after the first load. No portals, no gateways—browsers fetch directly from Walrus nodes.

---

## The Problem

**Traditional decentralized hosting** relies on gateway servers:

```
User → Gateway Server → Decentralized Storage
        ↑
   Single point of failure
   Costs money to run
   Can be shut down
```

Gateways defeat the purpose of decentralization.

---

## Our Solution

**Service workers** eliminate the middleman:

```
First visit:  User → Bootstrap (2KB) → Service Worker installed
Second visit: User → Service Worker → Walrus (no gateway!)
```

After the first load:
- ✅ **Works offline** (cached in browser)
- ✅ **Direct fetch** (browser → Walrus nodes)
- ✅ **Self-healing** (retries across 100+ nodes)
- ✅ **Censorship-resistant** (no server to shut down)

---

## How It Works

### Option 1: Managed Platform ([versui.app](https://versui.app))

Like **Vercel**, but decentralized:
- Drag & drop deployment
- Automatic domain hosting (`yoursite.versui.app`)
- Custom domains (bring your own)
- Built-in analytics
- Team collaboration

**Perfect for**: Agencies, startups, anyone who wants convenience

---

### Option 2: Open Source CLI

Use the **[versui-cli](https://github.com/Versui/versui-cli)** for zero lock-in:

```bash
npm install -g @versui/cli
versui deploy ./dist --output ./bootstrap
```

Download the bootstrap, host it anywhere. No platform needed.

**Perfect for**: Privacy advocates, self-hosters, maximum decentralization

---

## Quick Start

```bash
npm install -g @versui/cli
versui deploy ./dist
```

That's it. Your site is on Walrus.

**See full docs**: [versui-cli README](https://github.com/Versui/versui-cli)

---

## Why Versui?

✅ **No gateways needed** - Service workers fetch directly from Walrus nodes

✅ **Works offline** - Site cached in browser after first load

✅ **One command deploy** - `versui deploy ./dist` and you're done

✅ **Zero vendor lock-in** - Download bootstrap, host anywhere

✅ **Walrus-native** - Built specifically for the Walrus/Sui ecosystem

---

## Use Cases

🌐 **dApp Frontends** - No centralized CDN dependency

📄 **Documentation Sites** - Works offline (devs love offline docs)

🎨 **NFT Project Sites** - Truly on-chain (frontend on Walrus, metadata on Sui)

✍️ **Blogs & Publishing** - Censorship-resistant content

🏢 **Corporate Sites** - Disaster recovery (works even if servers fail)

---

## Tech Stack

- **Storage**: Walrus (100+ decentralized nodes)
- **Blockchain**: Sui (metadata, ownership)
- **Magic**: Service Workers (offline-first, direct fetch)
- **CLI**: Open source (Apache 2.0)

---

## Roadmap

### ✅ Phase 1: MVP
- CLI deployment tool
- Service worker auto-injection
- Self-hosting support

### 🚧 Phase 2: Platform Launch
- Managed hosting at versui.app
- Custom domains
- Analytics dashboard

### 🔮 Phase 3: Ecosystem
- Browser extension (native `.sui` resolution)
- Multi-storage fallbacks (IPFS, Arweave)
- On-chain bootstrap registry

---

## Learn More

- **CLI Docs**: [versui-cli README](https://github.com/Versui/versui-cli)
- **Website**: [versui.app](https://versui.app)
- **Walrus**: [walrus.site](https://walrus.site)
- **Sui**: [sui.io](https://sui.io)

---

<div align="center">

### No portals. No gateways. Just service workers.

**Built for the decentralized web 🦭⚡**

[Get Started](https://github.com/Versui/versui-cli) • [Try Platform](https://versui.app)

</div>
