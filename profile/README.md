<div align="center">
  <img src="../logo.png" alt="Versui" width="200"/>

# Versui

**Stateless hosting substrate. No gateways. No servers.**

[![Walrus](https://img.shields.io/badge/storage-Walrus-00C9FF?style=flat)](https://walrus.site)
[![Sui](https://img.shields.io/badge/chain-Sui-4DA2FF?style=flat)](https://sui.io)
[![Offline](https://img.shields.io/badge/offline-first-success?style=flat)](#)

</div>

---

## Axioms

```
Gateway = centralization = defeat
Service Worker = client-side proxy = freedom
Quilt = efficient blob bundling = 1 tx
```

Traditional hosting dies when servers die. Versui sites **self-heal**.

---

## Architecture

```
deploy ./dist → quilt encode → walrus register → sui commit → bootstrap output
```

**Bootstrap (2KB)**:
- Registers SW on first visit
- SW intercepts all fetches
- Direct reads from Walrus aggregators
- Exponential backoff (5s→60s, ∞ retry)
- Multi-aggregator failover
- Works offline after first load

**No portals. No gateways. No middlemen.**

---

## Specs

**Storage layer**: Walrus quilt encoding (multi-file → 1 blob)
**Metadata layer**: Sui blockchain (ownership, epochs, blob refs)
**Delivery layer**: Service Workers (browser-native proxy)
**Bootstrap layer**: 2KB HTML+SW (self-hosting ready)

**Security**: XSS escaping, no secrets in logs, offline-safe
**Resilience**: Aggregator failover, exponential backoff, auto-recovery
**Deployment**: `prepare` (offline signing) → `deploy` (broadcast)

---

## Usage

```bash
npm i -g @versui/cli
versui deploy ./dist
```

Or with offline signing:

```bash
versui prepare ./dist --output blob.json
# Sign tx bytes offline
versui deploy blob.json --signed tx.json
```

Bootstrap outputs to `./bootstrap` - host anywhere (Vercel, S3, IPFS, HTTP server).

---

## Packages

[**versui-cli**](https://github.com/Versui/versui-cli) - Deploy tool
[**versui-sw-plugin**](https://github.com/Versui/versui-sw-plugin) - Custom SW integration

---

## Philosophy

**Gateways are trust assumptions.**
Static sites don't need servers. They need blobs + pointers.

Walrus = blob availability (100+ nodes, 1/3 fault tolerance)
Sui = metadata coordination (sub-second finality)
Service Workers = client-side routing (browsers had this since 2014)

Combine all three. Remove servers. Sites become **indestructible**.

---

<div align="center">

**Built for the sovereign web**

[CLI](https://github.com/Versui/versui-cli) • [Docs](https://versui.app)

</div>
