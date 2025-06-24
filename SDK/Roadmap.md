# Monopoly SDK Roadmap

> **Version**: 2025 Edition  
> **Last updated**: 24 June 2025

This roadmap outlines our vision for the Monopoly SDK and related tools over the next 12–18 months. While priorities may shift based on user feedback and community contributions, this document captures the current direction of development.

---

## Table of Contents

- [Monopoly SDK Roadmap](#monopoly-sdk-roadmap)
  - [Table of Contents](#table-of-contents)
  - [1. Themes](#1-themes)
  - [2. In Progress](#2-in-progress)
  - [3. Planned (Q3–Q4 2025)](#3-planned-q3q4-2025)
  - [4. Future Ideas (2026+)](#4-future-ideas-2026)
  - [5. Out of Scope](#5-out-of-scope)
    - [Suggestions?](#suggestions)

---

## 1. Themes

These broad themes guide our prioritization:

- **Portability**: Support more platforms and runtimes (Edge, WASM, Native).
- **Replayability**: Deterministic logs, replay files, branching timelines.
- **Customisation**: Plugin hooks, custom board assets, AI strategy control.
- **Offline-first**: Reliable persistence and P2P multiplayer without a server.
- **Security & Integrity**: Cheat detection, signed turns, secure token auth.

---

## 2. In Progress

| Feature                      | Description                                                    | Status                |
| ---------------------------- | -------------------------------------------------------------- | --------------------- |
| **React Native bindings**    | Native gesture and animation support via `@monopoly/ui-native` | 🟡 In development     |
| **New board themes**         | "Metro", "Cyberpunk", and "Minimal" designs                    | 🟢 Asset finalization |
| **AI vs Human sessions**     | Opt-in AI opponents using trained Monte Carlo trees            | 🟢 Beta available     |
| **SDK Telemetry**            | Optional error and usage reporting                             | 🟠 Internal testing   |
| **Improved snapshot schema** | Smaller, binary-compatible game state dumps                    | 🟡 Draft spec         |

---

## 3. Planned (Q3–Q4 2025)

| Feature                    | Description                                                  |
| -------------------------- | ------------------------------------------------------------ |
| **WebAssembly RNG**        | Replace JS RNG with deterministic, performant WASM core      |
| **Edge Function support**  | Run game validation on Cloudflare Workers, Vercel Edge, etc. |
| **Live spectators**        | Join in-progress games as read-only viewers                  |
| **Plugin marketplace**     | Registry of verified themes, AI opponents, UI packs          |
| **Command middleware API** | Add logging, metrics, or access control at command level     |
| **E2E encrypted tokens**   | JWT-like ephemeral access tokens with public key auth        |

---

## 4. Future Ideas (2026+)

These are not yet scheduled but under consideration:

- ✅ CRDT-based peer-to-peer sync (no central server)
- ✅ Alternative transports: GraphQL, MQTT
- ✅ Visual game replay viewer
- ✅ Node.js CLI to simulate headless games
- ✅ Tournament mode (up to 64 players)
- ✅ Plugin-based ruleset engine (e.g. "free parking cash")
- ✅ Portable save files for exporting game states
- ✅ Full rewrite of core engine in Rust (targeting WASI and native)

---

## 5. Out of Scope

Some frequently requested ideas that we’ve chosen not to pursue:

| Idea                                              | Reason                                                 |
| ------------------------------------------------- | ------------------------------------------------------ |
| **Realtime voice chat**                           | Better handled by third-party tools (e.g. Discord SDK) |
| **Support for house rules in SaaS tier**          | Reserved for enterprise licenses due to complexity     |
| **Embedding Monopoly inside iframe game portals** | Violates Hasbro licensing guidelines                   |

---

### Suggestions?

Submit ideas or feature requests via [GitHub Discussions](https://github.com/monopoly/monopoly-sdk/discussions) or contact `roadmap@monopoly.io`.
