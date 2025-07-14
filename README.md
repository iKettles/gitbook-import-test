# Introduction

Monopoly SDK is the foundation for building multiplayer Monopoly experiences across web, mobile, desktop, and beyond. Whether you're embedding a simple game into your platform or crafting a fully custom UI with advanced automation, Monopoly SDK provides everything you need to build with Monopoly at scale.

***

## What is Monopoly SDK?

Monopoly SDK is a developer toolkit and game engine that powers Monopoly-as-a-Service. It's designed to be **modular**, **extensible**, and **portable**, letting you:

* Launch real-time Monopoly sessions with 2–8 players
* Control game flow programmatically (start, roll, trade, buy, etc.)
* Integrate AI players, spectators, or analytics
* Customize appearance with themes, skins, and tokens
* Persist and restore sessions across devices

***

## Who is it for?

* **Game developers** embedding Monopoly in apps and platforms
* **EdTech tools** simulating economics or finance with turn-based play
* **Hackers and hobbyists** building game night bots or tools
* **Teams building UIs** for custom game dashboards

***

## How it works

Monopoly SDK consists of three main parts:

1. **Client SDK** (`@monopoly/sdk`)\
   A lightweight TypeScript library to create, manage, and interact with game sessions.
2. **REST API**\
   A secure, scalable backend that handles authentication, session persistence, and server-authoritative state.
3. **Optional UI kits**\
   Pre-built headless UI libraries for React, Vue, and others to speed up development.

***

## Key Features

* 🎲 Deterministic Game Engine (turns, rolls, trades, events)
* 🔒 Secure by Design (JWT, API key support, token lifetimes)
* 🔄 Session Snapshots & Replay
* 🌍 Localization & Currency Config
* 📊 Real-time State Sync
* 🤖 AI Strategy Plugins
* 💅 Custom Themes and Boards

***

## Supported Environments

| Environment                 | Supported? |
| --------------------------- | ---------- |
| Browser                     | ✅          |
| Node.js                     | ✅          |
| React Native                | ✅ (beta)   |
| Edge Functions (Vercel, CF) | ✅          |
| WASM                        | 🚧 Planned |

***

## Getting Started

To start integrating Monopoly SDK:

1.  **Install the SDK** in your frontend or backend app:

    ```bash
    npm install @monopoly/sdk
    ```
2. **Create a session** with your tenant credentials.
3. **Subscribe to game events** and call actions (e.g. `rollDice`, `buyProperty`).
4. Optionally, **customize** the UI or integrate AI players.

***

## Explore the Docs

* [SDK Installation](monopoly-sdk-installation-guide.md)
* [Architecture Overview](monopoly-sdk-architecture-overview.md)
* [REST API Introduction](monopoly-sdk-rest-intro.md)
* [Contribution Guide](monopoly-sdk-contribution-guide.md)
* [Full OpenAPI Spec](monopoly-sdk-openapi.yaml)
* [Roadmap](monopoly-sdk-roadmap.md)

***

## License & Legal

Monopoly SDK is licensed under [MIT](https://opensource.org/licenses/MIT), but the use of "Monopoly" and visual likenesses is governed by the Hasbro® licensing agreement. Redistribution or public-facing games may require separate licensing.

***

## Need Help?

* 🧾 Read the docs: [https://docs.monopoly.io](https://docs.monopoly.io)
* 🐞 Report bugs: [https://github.com/monopoly/monopoly-sdk/issues](https://github.com/monopoly/monopoly-sdk/issues)
* 💬 Join Discord: [https://discord.gg/monopoly-sdk](https://discord.gg/monopoly-sdk)
* ✉️ Email us: [support@monopoly.io](mailto:support@monopoly.io)

Happy building! 🎲
