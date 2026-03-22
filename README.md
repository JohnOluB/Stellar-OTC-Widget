# stellar-otc-widget

> An embeddable React widget for peer-to-peer stablecoin trading on Stellar —
> add USDC, NGNX, EURC, and BRLT OTC swap flows to any web app in under 10 minutes.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)
[![Drips Wave Program](https://img.shields.io/badge/Drips-Wave%20Program-8B5CF6)](https://drips.network)

---

## Overview

`stellar-otc-widget` is a drop-in React component that brings Stellar DEX-powered
stablecoin swaps to any web application. Pass in asset pairs and a wallet signer,
and the widget handles rate discovery, slippage calculation, path payment construction,
and transaction submission — with a clean, customizable UI that matches your brand.

Designed for fintech apps, remittance platforms, crypto exchanges, and any product
that needs a fast, non-custodial FX or stablecoin swap layer.

---

## Technical Architecture

- **Widget Core:** React 18 + TypeScript component built with Tailwind CSS and
  `class-variance-authority` — fully themeable via CSS variables, embeds in any
  React or Next.js app with a single import
- **Rate Engine:** Real-time swap rate fetching from Stellar Horizon `/paths/strict-send`
  and `/paths/strict-receive` endpoints, with automatic best-path selection and
  slippage tolerance configuration
- **DEX Integration:** `@stellar/stellar-sdk` path payment operations — supports
  strict send, strict receive, and multi-hop routes across Stellar's native order book
- **Soroban OTC Contract:** Optional Rust/Soroban contract in `contracts/src/` for
  non-custodial limit order matching when DEX liquidity is thin — supports order
  creation, cancellation, and expiry
- **Wallet Agnostic:** Accepts any `SignerFunction` — Freighter, xBull, server keypair,
  or any `@creit.tech/stellar-wallets-kit` adapter

---

## 💧 Drips Wave Program

This repository is an active participant in the
**[Drips Wave Program](https://drips.network)** — a funding mechanism that rewards
open-source contributors for resolving scoped GitHub issues with on-chain streaming
payments.

### How to Contribute & Earn

**Step 1 — Register on Drips**
Visit [drips.network](https://drips.network) and connect your Ethereum-compatible wallet.
Your wallet address is where reward streams will be sent.

**Step 2 — Browse Open Issues**
Head to the [Issues tab](../../issues). Issues are labeled by complexity tier:

| Label           | Complexity | Typical Scope                                                              |
|-----------------|------------|----------------------------------------------------------------------------|
| `drips:trivial` | Trivial    | Add a Storybook story, fix a UI bug, improve token logo resolution         |
| `drips:medium`  | Medium     | New asset pair support, slippage UI, mobile responsive improvements        |
| `drips:high`    | High       | Limit order UI, Soroban OTC contract integration, multi-wallet support     |

**Step 3 — Claim an Issue**
Comment `/claim` on the issue you want. The maintainer will assign it.
One claim per issue at a time.

**Step 4 — Submit Your Work**
Open a Pull Request with `Closes #XX`. Ensure CI passes and include Storybook
stories for any new UI changes.

**Step 5 — Get Paid**
Merged PRs trigger your Drips payment stream. Continuous, no invoices needed.

---

## Project Structure
```
stellar-otc-widget/
├── src/
│   ├── widget/
│   │   ├── components/       # OTCWidget, AssetSelector, RateDisplay, ConfirmModal
│   │   ├── hooks/            # useSwapRate, usePathPayment, useWallet
│   │   └── context/          # OTCWidgetProvider, config context
│   ├── api/                  # Horizon path payment API client, rate fetcher
│   ├── utils/                # Amount formatters, slippage calculators, asset helpers
│   └── styles/               # Tailwind config, CSS variable theming
├── contracts/
│   ├── src/                  # Rust/Soroban OTC limit order contract
│   └── tests/                # Rust unit tests
├── examples/
│   ├── vite-app/             # Minimal Vite + React integration demo
│   └── nextjs-app/           # Next.js App Router integration demo
├── tests/
│   ├── unit/                 # Hook logic, rate engine, slippage utils
│   └── integration/          # Full swap flow against Stellar testnet
├── docs/                     # Integration guide, theming reference
├── public/                   # Token logos, static assets
├── package.json
├── tsconfig.json
└── README.md
```

---

## Quick Start
```bash
npm install stellar-otc-widget
```
```tsx
import { OTCWidget } from 'stellar-otc-widget';
import { Networks } from '@stellar/stellar-sdk';

export default function SwapPage() {
  return (
    <OTCWidget
      fromAsset={{ code: 'USDC', issuer: 'G...' }}
      toAsset={{ code: 'NGNX', issuer: 'G...' }}
      network={Networks.PUBLIC}
      signer={freighterSignerFn}
      theme={{ primary: '#6366f1', borderRadius: '12px' }}
    />
  );
}
```

---

## License

MIT © stellar-otc-widget contributors
