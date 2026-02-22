# Pumpfun Bundler

Pumpfun Bundler is a Solana token bundler script for launching and buying on pump.fun using coordinated wallets and bundle submission.

If you are searching for:
- pumpfun bundler
- pump.fun bundler
- solana token bundler for pumpfun
- pumpfun multi wallet bundler script

this repository provides a TypeScript implementation with Jito and Lil Jito execution paths.

## What This Pumpfun Bundler Does

This project automates a full pump.fun launch flow:
1. Creates a new token (with metadata fields from `.env`).
2. Optionally generates a vanity mint that ends with `pump`.
3. Distributes SOL from the main wallet across multiple generated wallets.
4. Builds and extends an Address Lookup Table (LUT) to reduce transaction size.
5. Creates coordinated buy instructions.
6. Submits a bundle using Jito endpoints or a configured Lil Jito endpoint.

## Key Features

- Pump.fun bundler workflow in TypeScript
- Multi-wallet buy bundling
- Optional vanity mint generation (`...pump`)
- Jito bundle execution (NY/Tokyo endpoints in current code)
- Lil Jito bundle execution mode
- LUT creation and extension
- Utility scripts for gather/close/status

## Project Scripts

From `package.json`:

- `npm start`: run main multi-wallet pumpfun bundler (`index.ts`)
- `npm run single`: run single-wallet bundle flow (`oneWalletBundle.ts`)
- `npm run close`: close LUT (`closeLut.ts`)
- `npm run gather`: gather funds/tokens from generated wallets (`gather.ts`)
- `npm run status`: check bundle/transaction status helper (`status.ts`)

## Requirements

- Node.js 16+
- npm
- Solana mainnet RPC + WebSocket endpoints
- Funded main wallet (SOL for creation, buys, fees, and tips)

## Installation

```bash
npm install
```

## Environment Configuration

Copy `.env.example` to `.env` and fill values.

Required core fields:

```env
PRIVATE_KEY=
RPC_ENDPOINT=
RPC_WEBSOCKET_ENDPOINT=

LIL_JIT_ENDPOINT=https://blue-bitter-mountain.solana-mainnet.quiknode.pro/
LIL_JIT_WEBSOCKET_ENDPOINT=wss://blue-bitter-mountain.solana-mainnet.quiknode.pro/

LIL_JIT_MODE=false

SWAP_AMOUNT=1
DISTRIBUTION_WALLETNUM=16

SIMULATE_ONLY=false
JITO_FEE=0.001
MINIMUM_JITO_TIP=0.0005

TOKEN_NAME=DummyToken
TOKEN_SYMBOL=DUMMY
DESCRIPTION=Dummy token for local testing
TOKEN_SHOW_NAME=DUM
TOKEN_CREATE_ON=https://bonk.fun
TWITTER=https://x.com/dummy
TELEGRAM=https://t.me/dummy
WEBSITE=https://example.com
FILE=./image/2.jpg
VANITY_MODE=false
BUYER_WALLET=
BUYER_AMOUNT=0.1

```

## How To Run This Pump.fun Bundler

### Multi-Wallet Mode

```bash
npm start
```

Use this mode for coordinated wallet buys on pump.fun.

### Single-Wallet Mode

```bash
npm run single
```

Use this mode when you want a smaller flow with one buyer wallet.

## Execution Mode: Jito vs Lil Jito

- `LIL_JIT_MODE=false`: use Jito bundle endpoint flow.
- `LIL_JIT_MODE=true`: use Lil Jito endpoint from `.env`.

Choose based on your endpoint reliability and infrastructure.

## Wallet and Balance Notes

The main script checks balance before execution.
A rough threshold used in code is:

`(SWAP_AMOUNT + 0.01) * DISTRIBUTION_WALLETNUM + 0.04`

Keep extra SOL for congestion and retries.

## Repository Structure

- `index.ts`: main multi-wallet pumpfun bundler flow
- `oneWalletBundle.ts`: single-wallet flow
- `src/main.ts`: token creation, distribution, LUT, buy instruction building
- `executor/jito.ts`: Jito submission path
- `executor/liljito.ts`: Lil Jito submission path
- `gather.ts`: gather tokens/SOL back to main wallet
- `closeLut.ts`: LUT cleanup
- `status.ts`: status utilities

## SEO Keywords Covered By This README

This README intentionally targets practical search phrases users use when looking for this kind of project:
- pumpfun bundler
- pump.fun bundler script
- solana pumpfun token bundler
- jito pumpfun bundler
- multi wallet pumpfun bot

## Security and Risk

- Never commit private keys.
- Use a dedicated wallet for testing.
- Start with small amounts.
- This tool interacts with real funds on Solana.

## Disclaimer

This repository is for development, research, and educational use. You are responsible for legal, tax, and operational risk in your jurisdiction.
