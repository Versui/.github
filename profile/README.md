<div align="center">

# VersUI

**Vercel for Web3 - Deploy static sites to decentralized storage**

[![FOR THE BADGE](https://forthebadge.com/images/badges/built-with-love.svg)](https://forthebadge.com)
[![FOR THE BADGE](https://forthebadge.com/images/badges/powered-by-black-magic.svg)](https://forthebadge.com)
[![FOR THE BADGE](https://forthebadge.com/images/badges/uses-badges.svg)](https://forthebadge.com)

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg?style=for-the-badge)](LICENSE)
[![Node.js](https://img.shields.io/badge/Node.js-18+-339933.svg?style=for-the-badge&logo=node.js&logoColor=white)](https://nodejs.org)
[![Sui](https://img.shields.io/badge/Sui-Blockchain-4DA9FF?style=for-the-badge&logo=sui&logoColor=white)](https://sui.io)
[![Walrus](https://img.shields.io/badge/Walrus-Storage-FF6B6B?style=for-the-badge)](https://walrus.site)

**Censorship-resistant · Offline-capable · Zero vendor lock-in**

</div>

---

## 🚀 What is VersUI?

VersUI is a **fully decentralized deployment platform** for static websites, combining the simplicity of Vercel with the resilience of Web3.

**Deploy once. Live forever. Control always.**

### The Stack

```
┌─────────────────────────────────────────────────┐
│                    VersUI                        │
├─────────────────────────────────────────────────┤
│                                                  │
│  🔷 Walrus Storage (100+ nodes)                 │
│     └─ Decentralized blob storage                │
│     └─ Byzantine fault-tolerant                  │
│     └─ Erasure coded redundancy                  │
│                                                  │
│  ⛓️  Sui Blockchain                              │
│     └─ On-chain metadata coordination            │
│     └─ Ownership & routing                       │
│     └─ Permissionless updates                    │
│                                                  │
│  ⚙️  Service Workers                             │
│     └─ Direct Walrus fetching (no gateway)       │
│     └─ Offline-first architecture                │
│     └─ Multi-aggregator failover                 │
│                                                  │
└─────────────────────────────────────────────────┘
```

### Why VersUI?

| **Feature**              | **Vercel**      | **IPFS**        | **VersUI**     |
|--------------------------|-----------------|-----------------|----------------|
| Deployment               | ✅ One command  | ❌ Complex      | ✅ One command |
| Censorship Resistance    | ❌ Centralized  | ✅ Decentralized| ✅ Decentralized|
| Offline Support          | ❌ No           | ⚠️ Gateway-dependent | ✅ Service Worker cache |
| Vendor Lock-in           | ❌ Locked       | ✅ Portable     | ✅ Portable    |
| Direct Content Fetching  | ❌ Via Vercel   | ⚠️ Via Gateway  | ✅ Direct from storage |
| Domain Management        | ✅ Built-in     | ⚠️ Manual/ENS   | ✅ SuiNS + Custom |
| Cost (per month)         | $20+            | $5-20           | **$2-5**       |

---

## 📦 Components

VersUI is composed of **4 open-source packages**:

### 🖥️ [`versui-cli`](./versui-cli)

**Interactive CLI for deploying static sites**

```bash
npm install -g @versui/cli

versui deploy ./dist
```

**Features:**
- 🎨 Beautiful interactive prompts
- 🔐 Non-custodial wallet support
- 📊 Delta detection (only upload changed files)
- ⚡ Auto-generated service worker bootstrap
- 🌐 Multi-network support (testnet/mainnet)

**Status:** ✅ **Production Ready** (v0.1.5)

---

### 🔌 [`versui-sw-plugin`](./versui-sw-plugin)

**Service Worker plugin for fetching from Walrus**

```js
import { create_versui_handler } from '@versui/sw-plugin'

const versui = create_versui_handler()
versui.load({ '/index.html': 'blob-id' })
self.addEventListener('fetch', e => versui.handle(e))
```

**Features:**
- 🔄 Multi-aggregator failover
- 💾 Optional caching layer
- 🔁 Exponential backoff retry
- 🎯 MIME type detection
- 📱 Offline-first architecture

**Status:** ✅ **Production Ready** (v0.1.0)

---

### ⛓️ [`versui-move`](./versui-move)

**Sui Move smart contracts for on-chain metadata**

```move
module versui::site {
    struct Site has key, store {
        id: UID,
        name: String,
        resource_count: u64,
    }

    struct Resource has key, store {
        id: UID,
        site_id: ID,
        path: String,
        blob_id: u256,
        blob_hash: vector<u8>,
        content_type: String,
        size: u64,
    }
}
```

**Deployed:**
- **Testnet:** `0x467c6f31d1aa8ff0ad6460f60b5733605683bbef47bf148d9b7b37967f4b4b46`

**Status:** ✅ **Production Ready**

---

### 🌐 [`versui-platform`](./versui-platform) *(Future)*

**Managed platform with dashboard, API, and premium features**

**Planned features:**
- 🎨 Drag & drop deployment UI
- 🔐 Sui wallet authentication
- 📈 Advanced analytics
- 🌍 Custom domain management
- 👥 Team collaboration
- 💳 On-chain subscriptions

**Status:** 📝 **Documentation Phase** (Architecture defined, not implemented)

---

## 🎯 How It Works

### 1️⃣ **Deploy** (One Command)

```bash
versui deploy ./dist
```

**What happens:**
- Files are hashed (SHA-256) and deduplicated
- Changed files uploaded to Walrus (100+ nodes)
- Site metadata stored on Sui blockchain
- Bootstrap HTML generated (< 3KB)

---

### 2️⃣ **First Visit** (Bootstrap Load)

```
User → visits mysite.versui.app
  ↓
Bootstrap HTML loads
  ↓
Service Worker registers
  ↓
Fetches metadata from Sui
  ↓
Fetches blobs from Walrus
  ↓
Caches in browser
  ↓
Site renders
```

**Load time:** ~2-3 seconds

---

### 3️⃣ **Subsequent Visits** (Instant)

```
User → visits mysite.versui.app
  ↓
Service Worker intercepts
  ↓
Serves from cache
  ↓
Site renders
```

**Load time:** ~50-100ms

---

### 4️⃣ **Offline Mode** (Resilient)

```
User → offline, visits site
  ↓
Service Worker serves from cache
  ↓
Site works perfectly
```

**No internet? No problem.**

---

## 🔒 Fully Decentralized Architecture

### **Storage Layer: Walrus**
- 100+ independent nodes (no single point of failure)
- Byzantine fault-tolerant consensus
- Erasure coding (data survives node failures)
- Content-addressed deduplication

### **Coordination Layer: Sui**
- On-chain metadata (immutable record)
- Ownership via NFT-like objects
- Permissionless updates (your keys, your control)
- Query via RPC (no centralized API)

### **Access Layer: Service Workers**
- Browser-native (no plugins, no extensions)
- Direct Walrus fetching (no gateway dependency)
- Offline-first (works without internet after first load)
- Multi-aggregator failover (resilient to aggregator outages)

---

## ⚡ Quick Start

### Prerequisites

```bash
# Install Walrus CLI
# https://docs.walrus.site/walrus-sites/tutorial-install.html

# Install Sui CLI
# https://docs.sui.io/guides/developer/getting-started/sui-install

# Verify installation
walrus --version
sui --version
```

### Deploy Your First Site

```bash
# Install VersUI CLI
npm install -g @versui/cli

# Deploy static site
cd my-static-site
versui deploy ./dist

# Output:
# ✅ Site deployed!
# 🌐 URL: https://abc123.versui.app
# 📦 Object ID: 0xdef456...
```

### Custom Service Worker Integration

```bash
# Install plugin
npm install @versui/sw-plugin

# Add to your sw.js
import { create_versui_handler } from '@versui/sw-plugin'

const versui = create_versui_handler({
  cache_name: 'my-app-v1',
  aggregators: ['https://my-aggregator.com']
})

versui.load({
  '/index.html': 'blob-id-1',
  '/app.js': 'blob-id-2'
})

self.addEventListener('fetch', e => versui.handle(e))
```

---

## 🗂️ Repository Structure

```
versui/
├── versui-cli/              # CLI tool (Apache 2.0)
│   ├── src/
│   │   ├── commands/        # deploy, list, delete
│   │   └── lib/             # walrus, sui, hash, delta, sw
│   ├── test/                # 85 tests (84% coverage)
│   └── README.md
│
├── versui-sw-plugin/        # Service Worker plugin (Apache 2.0)
│   ├── src/
│   │   └── index.js         # Walrus fetch handler
│   ├── test/                # 22 tests (100% coverage)
│   └── README.md
│
├── versui-move/             # Sui Move contracts (Apache 2.0)
│   ├── sources/
│   │   └── versui.move      # Site & Resource structs
│   └── README.md
│
└── versui-platform/         # Platform (planned, docs only)
    ├── docs/                # VitePress documentation
    ├── landing/             # Vue 3 landing page
    └── README.md
```

---

## 🛠️ Development

### CLI Development

```bash
cd versui-cli
npm install
npm run lint
npm test                     # 85 tests
npm run coverage             # 84% coverage
```

### SW Plugin Development

```bash
cd versui-sw-plugin
npm install
npm test                     # 22 tests
```

### Move Contract Development

```bash
cd versui-move
sui move build
sui move test
sui client publish --gas-budget 100000000
```

---

## 🎯 Roadmap

### ✅ **Phase 1: MVP** (Completed)

- [x] CLI deployment
- [x] Service worker plugin
- [x] Move contracts (deployed on testnet)
- [x] Delta detection
- [x] Multi-network support

### 🚧 **Phase 2: Platform** (In Progress)

- [ ] Dashboard UI (drag & drop)
- [ ] Backend API
- [ ] Domain management (SuiNS + custom)
- [ ] Analytics
- [ ] Team accounts

### 🔮 **Phase 3: Advanced** (Future)

- [ ] Mainnet deployment
- [ ] On-chain subscriptions
- [ ] Browser extension (`.sui` resolution)
- [ ] Edge functions integration
- [ ] Multi-chain support (IPFS, Arweave)

---

## 📊 Status

| Component          | Status                | Version | Tests    | Coverage |
|--------------------|----------------------|---------|----------|----------|
| `versui-cli`       | ✅ Production Ready   | v0.1.5  | 85/85 ✅  | 84% ✅    |
| `versui-sw-plugin` | ✅ Production Ready   | v0.1.0  | 22/22 ✅  | 100% ✅   |
| `versui-move`      | ✅ Deployed (Testnet) | v1.0.0  | N/A      | N/A      |
| `versui-platform`  | 📝 Docs Only          | N/A     | N/A      | N/A      |

---

## 🤝 Contributing

VersUI is **fully open source** under Apache 2.0.

**Want to contribute?**

1. Fork the repo
2. Create a feature branch (`git checkout -b feat/awesome-feature`)
3. Write tests (TDD required)
4. Commit changes (`git commit -m 'feat: add awesome feature'`)
5. Push to branch (`git push origin feat/awesome-feature`)
6. Open a Pull Request

---

## 📄 License

All VersUI components are licensed under **Apache 2.0**.

- **versui-cli:** Apache 2.0
- **versui-sw-plugin:** Apache 2.0
- **versui-move:** Apache 2.0
- **versui-platform:** Apache 2.0 (when released)

---

## 🔗 Links

- **Documentation:** [versui.app/docs](https://versui.app/docs) *(coming soon)*
- **CLI:** [npmjs.com/package/@versui/cli](https://www.npmjs.com/package/@versui/cli)
- **SW Plugin:** [npmjs.com/package/@versui/sw-plugin](https://www.npmjs.com/package/@versui/sw-plugin)
- **Walrus:** [walrus.site](https://walrus.site)
- **Sui:** [sui.io](https://sui.io)

---

<div align="center">

**Built with ❤️ by the VersUI team**

**Decentralized. Unstoppable. Yours.**

[![FOR THE BADGE](https://forthebadge.com/images/badges/made-with-javascript.svg)](https://forthebadge.com)
[![FOR THE BADGE](https://forthebadge.com/images/badges/open-source.svg)](https://forthebadge.com)
[![FOR THE BADGE](https://forthebadge.com/images/badges/check-it-out.svg)](https://forthebadge.com)

</div>
