# Monopoly SDK Installation & Integration Guide

> **Version**: 1.4.0  
> **Last updated**: 24 June 2025  
> **Applies to**: `@monopoly/sdk` **v1.x**

Welcome to the **Monopoly® SDK**!  
This guide walks you through installing the SDK in a JavaScript/TypeScript project, wiring up an end‑to‑end Monopoly game session, and integrating it into your own application UI.  
If you run into trouble, jump to [Troubleshooting](#troubleshooting) or [FAQ](#faq).

---

## Table of Contents

- [Monopoly SDK Installation \& Integration Guide](#monopoly-sdk-installation--integration-guide)
  - [Table of Contents](#table-of-contents)
  - [1. Prerequisites](#1-prerequisites)
  - [2. Getting the Package](#2-getting-the-package)
    - [2.1. Installing with npm](#21-installing-with-npm)
    - [2.2. Installing with Yarn](#22-installing-with-yarn)
    - [2.3. Installing with pnpm](#23-installing-with-pnpm)
    - [2.4. Using a CDN (browser‑only)](#24-using-a-cdn-browseronly)
  - [3. Post‑Install Checklist](#3-postinstall-checklist)
  - [4. Basic Usage (Vanilla JS)](#4-basic-usage-vanilla-js)
  - [5. Basic Usage (TypeScript)](#5-basic-usage-typescript)
  - [6. React Quick‑Start](#6-react-quickstart)
  - [7. Configuration Options](#7-configuration-options)
  - [8. Authentication \& Security](#8-authentication--security)
  - [9. Event Lifecycle](#9-event-lifecycle)
  - [10. Saving \& Restoring Game State](#10-saving--restoring-game-state)
  - [11. Advanced Topics](#11-advanced-topics)
  - [12. Troubleshooting](#12-troubleshooting)
  - [13. FAQ](#13-faq)
    - [Why does the package size look huge in `webpack-bundle-analyzer`?](#why-does-the-package-size-look-huge-in-webpack-bundle-analyzer)
    - [Is self‑hosting possible?](#is-selfhosting-possible)
    - [How can I support more than 8 players?](#how-can-i-support-more-than-8-players)
  - [14. Uninstalling](#14-uninstalling)
  - [15. Appendix A: Full Type Definitions](#15-appendix-a-full-type-definitions)
    - [That’s it!](#thats-it)

---

## 1. Prerequisites

| Requirement           | Minimum                              | Recommended              |
| --------------------- | ------------------------------------ | ------------------------ |
| **Node.js**           | 16 LTS                               | 20 LTS                   |
| **Package manager**   | npm 8                                | npm 10 / Yarn 4 / pnpm 9 |
| **ECMAScript target** | ES2020                               | ES2022                   |
| **TypeScript**        | 4.7                                  | 5.5                      |
| **Browser**           | Chromium 102, Firefox 100, Safari 16 | Latest stable            |

Make sure you have a Monopoly SaaS **tenant ID** and an **API secret**. You receive these in the dashboard when you create an account.

```bash
# Verify Node version
node --version
```

---

## 2. Getting the Package

### 2.1. Installing with npm

```bash
npm install @monopoly/sdk --save
```

Add the `--save-exact` flag in CI pipelines to avoid soft upgrades.

### 2.2. Installing with Yarn

```bash
yarn add @monopoly/sdk
```

### 2.3. Installing with pnpm

```bash
pnpm add @monopoly/sdk
```

### 2.4. Using a CDN (browser‑only)

```html
<script
  type="module"
  src="https://cdn.monopoly.io/sdk/1.x/monopoly.min.js"
></script>
```

This exposes `window.MonopolySdk` and is NOT tree‑shakable.

---

## 3. Post‑Install Checklist

- ✅ `node_modules/@monopoly/sdk` exists
- ✅ A `package-lock.json`, `yarn.lock`, or `pnpm-lock.yaml` was updated
- ✅ Your bundler (Vite, Webpack, etc.) resolves `module` & `types` fields
- ✅ TypeScript picks up `@types/monopoly__sdk` (bundled)

> **Tip**: If IntelliSense fails, restart your TS server (VS Code: `Ctrl+Shift+P → TypeScript: Restart TS Server`).

---

## 4. Basic Usage (Vanilla JS)

```js
// index.js
import { Monopoly } from "@monopoly/sdk";

/** @type {import('@monopoly/sdk').SessionOptions} */
const opts = {
  tenantId: "TENANT_123",
  secret: "sk_test_51J...",
  locale: "en-US",
  players: [
    { id: "p1", name: "Alice" },
    { id: "p2", name: "Bob" },
  ],
};

(async () => {
  const session = await Monopoly.createSession(opts);
  session.on("diceRolled", (ev) => console.log(ev));
  await session.start();
})();
```

---

## 5. Basic Usage (TypeScript)

```typescript
// game.ts
import {
  Monopoly,
  SessionOptions,
  DiceRolledEvent,
  TradeOfferEvent,
} from "@monopoly/sdk";

const options: SessionOptions = {
  tenantId: process.env.MONOPOLY_TENANT!,
  secret: process.env.MONOPOLY_SECRET!,
  currency: "USD",
  boardTheme: "classic",
  players: [
    { id: "u1", name: "Carol" },
    { id: "u2", name: "Dave" },
  ],
};

async function main() {
  const session = await Monopoly.createSession(options);

  session.on<DiceRolledEvent>("diceRolled", ({ playerId, amount }) => {
    console.log(`${playerId} rolled a ${amount}`);
  });

  session.on<TradeOfferEvent>("tradeOffer", (offer) => {
    console.info("Trade offered:", offer);
  });

  await session.start();
}

main().catch(console.error);
```

Compile with:

```bash
ts-node game.ts
```

---

## 6. React Quick‑Start

Below is a minimal React component that shows the current turn and allows rolling dice.

```typescript
// MonopolyBoard.tsx
import React from "react";
import { Monopoly, Session } from "@monopoly/sdk";

export default function MonopolyBoard() {
  const [session, setSession] = React.useState<Session>();
  const [currentTurn, setCurrentTurn] = React.useState<string>();

  React.useEffect(() => {
    (async () => {
      const s = await Monopoly.createSession({
        tenantId: "TENANT_123",
        secret: "sk_live_abc",
        players: [
          { id: "1", name: "Alice" },
          { id: "2", name: "Bob" },
        ],
      });
      s.on("turnChanged", (ev) => setCurrentTurn(ev.playerId));
      await s.start();
      setSession(s);
    })();
  }, []);

  if (!session) return <p>Loading Monopoly…</p>;

  return (
    <div className="flex flex-col gap-4">
      <h2>It’s {currentTurn ?? "…"}’s turn</h2>
      <button
        className="rounded bg-indigo-600 px-4 py-2 text-white"
        onClick={() => session.rollDice()}
      >
        Roll Dice
      </button>
    </div>
  );
}
```

> **Note**: The SDK is framework‑agnostic. You can use the same API in Vue, Svelte, Angular, or vanilla DOM.

---

## 7. Configuration Options

```typescript
interface SessionOptions {
  /** Your tenant ID provided in the Monopoly dashboard. */
  tenantId: string;

  /** Server secret (never expose in the browser!). */
  secret: string;

  /** ISO currency code, defaults to "USD". */
  currency?: string;

  /** Player list (2–8 players). */
  players: { id: string; name: string }[];

  /** Localisation tag (e.g. "fr-FR"). */
  locale?: string;

  /** Pick one of the built‑in board themes. */
  boardTheme?: "classic" | "neon" | "dark";

  /** Hook to override networking (SSR friendly). */
  fetch?: typeof fetch;
}
```

Set global defaults once per app:

```typescript
import { Monopoly } from "@monopoly/sdk";

Monopoly.defaults.baseUrl = "https://eu.monopoly.cloud";
Monopoly.defaults.logLevel = "debug";
```

---

## 8. Authentication & Security

1. **Server‑side token exchange** – never embed your secret in client bundles.
2. Use the [token endpoint](https://docs.monopoly.io/auth/token) to get a short‑lived JWT.
3. Pass `authToken` **instead of** `secret` in the browser:

```typescript
const session = await Monopoly.createSession({
  tenantId: "TENANT_123",
  authToken: await getJwt(),
  players,
});
```

Set the JWT lifetime ≤ 30 minutes and refresh on the `tokenExpiring` event.

---

## 9. Event Lifecycle

| Event            | Payload               | When it fires                             |
| ---------------- | --------------------- | ----------------------------------------- |
| `sessionCreated` | `SessionCreatedEvent` | Immediately after server ACK              |
| `turnChanged`    | `TurnChangedEvent`    | When the active player changes            |
| `diceRolled`     | `DiceRolledEvent`     | After a player rolls                      |
| `propertyBought` | `PropertyBoughtEvent` | After a successful purchase               |
| `tradeOffer`     | `TradeOfferEvent`     | When a player proposes a trade            |
| `bankrupt`       | `BankruptEvent`       | When a player goes bankrupt               |
| `sessionEnded`   | `SessionEndedEvent`   | When someone wins or all but one bankrupt |

Attach listeners _before_ calling `start()` to avoid missing early events:

```typescript
session.on("sessionCreated", () => console.log("Ready!"));
await session.start();
```

---

## 10. Saving & Restoring Game State

```typescript
// At any point during play
const snapshot = await session.saveState();
localStorage.setItem("monopolySave", JSON.stringify(snapshot));

// …later
const saved = JSON.parse(localStorage.getItem("monopolySave")!);
const resumed = await Monopoly.resumeSession(saved);
```

Snapshots are idempotent JSON blobs (< 5 KB) containing RNG seeds, transactions, and board state.

---

## 11. Advanced Topics

- **Custom dice algorithms** (e.g. weighted dice for tutorials)
- **Serverless edge workers** integration
- **Spectator mode** for streaming
- **White‑label UI kit** (`@monopoly/ui`)
- **AI opponents** using the [`@monopoly/ai`] package
- **Offline play** via Web Transport fall‑back

---

## 12. Troubleshooting

| Symptom                 | Cause                              | Fix                                                        |
| ----------------------- | ---------------------------------- | ---------------------------------------------------------- |
| `ERR_INVALID_SECRET`    | Wrong secret or token expired      | Refresh JWT; check dashboard                               |
| Empty board tiles       | CSS isolation conflict             | Import base styles: `@monopoly/sdk/styles.css`             |
| Events never fire       | Listeners attached after `start()` | Attach before, or call `await session.ready`               |
| Freeze on mobile Safari | IndexedDB quota exceeded           | Disable persistence: `Monopoly.defaults.persistence=false` |

Enable verbose logs:

```typescript
Monopoly.defaults.logLevel = "trace";
```

Logs appear in dev‑tools prefixed with `[Monopoly]`.

---

## 13. FAQ

### Why does the package size look huge in `webpack-bundle-analyzer`?

Tree‑shaking removes unused game assets. The raw tarball contains multiple board skins; only referenced skins are included in the final bundle.

### Is self‑hosting possible?

Yes. Purchase an enterprise licence and deploy the game engine in your VPC.

### How can I support more than 8 players?

The Hasbro® licence caps sessions at 8 players. Contact sales for tournament mode.

---

## 14. Uninstalling

```bash
npm uninstall @monopoly/sdk
```

Remove leftover config:

```bash
# package.json
"monopoly": {
  "tenant": "…",
  "baseUrl": "…"
}
```

---

## 15. Appendix A: Full Type Definitions

Below is a _condensed_ excerpt of the public typings. For the complete up‑to‑date API, `npm run docs` or visit https://docs.monopoly.io.

```typescript
// index.d.ts
export interface MonopolyStatic {
  createSession(options: SessionOptions): Promise<Session>;
  resumeSession(snapshot: SessionSnapshot): Promise<Session>;
  defaults: MonopolyDefaults;
}

export interface Session {
  id: string;
  start(): Promise<void>;
  rollDice(): Promise<DiceRolledEvent>;
  buyProperty(propertyId: string): Promise<PropertyBoughtEvent>;
  on<E>(event: EventName<E>, listener: (e: E) => void): void;
  saveState(): Promise<SessionSnapshot>;
}

export interface SessionOptions { /* see section 7 */ }
export interface SessionSnapshot { /* opaque */ }
export type EventName<E> = /* mapped type */;
export interface MonopolyDefaults {
  baseUrl: string;
  logLevel: "silent" | "error" | "warn" | "info" | "debug" | "trace";
  persistence: boolean;
}
```

---

### That’s it!

You’re ready to roll the dice.  
Found an issue? Open one at <https://github.com/monopoly/monopoly-sdk/issues>.
