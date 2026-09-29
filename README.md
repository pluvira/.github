# Pluvira

An open-core, high-performance live media aggregator, EPG schedule guide, and stream failover engine built for self-hosted NAS, home servers, and edge environments.

[![License](https://img.shields.io/badge/license-BSL--1.1-blue.svg)](https://mariadb.com/bsl11/)
[![Website](https://img.shields.io/badge/website-pluvira.com-emerald.svg)](https://pluvira.com)
[![Documentation](https://img.shields.io/badge/docs-pluvira.com%2Fdocs-purple.svg)](https://pluvira.com/docs)
[![Portal](https://img.shields.io/badge/portal-pluvira.com%2Fportal-cyan.svg)](https://pluvira.com/portal)

---

## The Pluvira Ecosystem

Pluvira combines local self-hosted autonomy with native acceleration and privacy-preserving cloud services:

* **[Pluvira Core](https://github.com/pluvira/pluvira)**: Open-core self-hosted application engine with FastAPI, dual-database SQLite WAL pipeline, RAM disk (`tmpfs`) storage optimization, and reactive Svelte 5 SPA WebUI.
* **Pro Native Engine**: High-performance multithreaded Rust engine. Delivers parallel duplicate clustering, high-throughput concurrent stream testing, and streaming XMLTV guide ingestion running directly in native OS threads.
* **Pluvira Cloud Services**: Zero-PII cloud services providing Ed25519 cryptographic licensing, RFC 8628 device pairing, end-to-end encrypted (E2EE) WebRTC blind signaling, and opaque client-side encrypted backup vaults.

---

## Interface Tour

### Live TV & Synchronized EPG Timeline Grid

Seamless 16:9 streaming player with synchronized 24-hour horizontal EPG timeline grid, live broadcast progress indicator, and height-matched channel guide:

![Pluvira Live TV & EPG Guide](https://raw.githubusercontent.com/pluvira/pluvira/main/docs/assets/screenshots/hero-live-tv.webp)

### Multi-View Floating Stream Engine

Simultaneous live monitoring across multiple feeds with independent floating players, real-time health scoring, and automatic backup stream failover:

![Multi-View Floating Stream Engine](https://raw.githubusercontent.com/pluvira/pluvira/main/docs/assets/screenshots/feature-multiview.webp)

### Intelligent Content Discovery & EPG Search

Instant catalog search featuring relevance scoring, multilingual stop-word tokenization, diacritic normalization, and live broadcast highlighting:

![Intelligent EPG Search](https://raw.githubusercontent.com/pluvira/pluvira/main/docs/assets/screenshots/feature-search-epg.webp)

### Zero-PII Customer Portal & Cloud Vault

Zero-PII Crockford Base32 identities, RFC 8628 device pairing, active IP lease diagnostics, and client-side AES-256-GCM encrypted backup vault:

![Zero-PII Customer Portal](https://raw.githubusercontent.com/pluvira/pluvira/main/docs/assets/screenshots/portal-zeropii-vault.webp)

---

## Key Technical Pillars

1. **Hardware & Flash Protection**: Heavy decompression, temporary databases, and regex evaluation run inside RAM disk (`/dev/shm`), eliminating write wear on SSDs and SMR disks.
2. **Crash Resilience & Non-Blocking Pipeline**: CPU-intensive operations execute inside compiled Rust OS threads outside Python GIL, keeping the WebUI responsive.
3. **Slot-Pool Failover**: Up to 7 backup streams per channel ranked by dynamic health scores (0–100) with automatic 3-retry player recovery.
4. **Zero-PII Security**: Zero user tracking, zero cleartext IP logging, HMAC-SHA256 blind indices, and $k \ge 50$ anonymity thresholds on public metrics.

---

## Quickstart (Docker Compose)

Deploy the unified container on your local NAS or server:

```yaml
services:
  pluvira:
    image: ghcr.io/pluvira/app:latest
    container_name: pluvira
    restart: unless-stopped
    ports:
      - "8585:8585"
    tmpfs:
      - /dev/shm/pluvira:rw,size=512m,mode=1777
    volumes:
      - ./config:/app/config
      - ./data:/app/data
```

Access the WebUI at `http://<NAS_OR_SERVER_IP>:8585` (or `http://localhost:8585` if running locally).

---

## Licensing & Business Source License 1.1 (BSL)

Pluvira Core is licensed under the **Business Source License 1.1 (BSL 1.1)**:

* **Personal Free Tier (Self-Hosted)**: Free for non-commercial, personal home use:
  * Maximum 2 Active M3U Playlists
  * Maximum 1 Curated Personal Playlist ("My List")
  * Maximum 2,500 Ingest Channels in local database
  * Maximum 25 Curated Channels in "My List"
  * Maximum 2 Failover Stream Slots per channel (Slot 0 Primary + Slot 1 Backup)
  * Maximum 2 Concurrent Stream Views
* **Pro & Commercial Tier**: Removes resource ceilings, unlocks the Rust native optimizer, WebRTC remote access, and 5 automated E2EE cloud backup slots.
* **Change License**: Converts automatically to the **Apache License 2.0** exactly 60 months (5 years) after each release.

---

## Official Links

* **Documentation**: [https://pluvira.com/docs](https://pluvira.com/docs)
* **Customer Portal**: [https://pluvira.com/portal](https://pluvira.com/portal)
* **Website**: [https://pluvira.com](https://pluvira.com)
* **Issue Tracker**: [github.com/pluvira/pluvira/issues](https://github.com/pluvira/pluvira/issues)
