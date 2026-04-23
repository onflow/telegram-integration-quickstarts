# AGENTS.md

This file provides guidance to AI coding agents (Claude Code, Codex, Cursor, Copilot, and others)
working in this repository. It is loaded into agent context automatically — keep edits concise.

## Overview

`telegram-integration-quickstarts` is a collection of five beginner-oriented courses that teach
how to build Telegram Web Apps (TWAs) on Flow. Each course is a self-contained folder with a
tutorial `README.md`, an `example/` reference implementation, and a `solution/` folder where
learners submit their deeplink. The repository is a learning resource, not a shipped product —
there is no root build system, no root `package.json`, no `LICENSE`, no `CONTRIBUTING.md`, and
no CI workflows.

## Repository Layout

```
Course_1_Deploy_A_Telegram_Web_App/          BotFather walkthrough (no code)
Course_2_Authenticate_Users_With_TWA_SDK/    Next.js + @twa-dev/sdk
Course_3_Connect_OKX_Wallet_Flow_EVM/        Next.js + @okxconnect/ui (Flow EVM)
Course_4_Connect_Flow_Wallet_Flow_Cadence/   Next.js + @onflow/fcl (Flow Cadence)
Course_5_Connect_Privy_Wallet_Flow_EVM/      Next.js + @privy-io/react-auth (Flow EVM)
assets/images/                               Screenshots/GIFs referenced by course READMEs
README.md                                    Repo intro and folder map
```

Each course folder contains:
- `README.md` — step-by-step tutorial
- `example/` — reference implementation (code in Courses 2–5; link-only in Course 1)
- `solution/README.md` — placeholder for learner submission

## Build and Test Commands

There is no repo-root build system. Course 1 has no code. Courses 2–5 each contain an
independent Next.js app under `example/<app-name>/` with identical npm scripts
(from each `package.json`):

```bash
cd Course_<N>_.../example/<app-name>/
npm install            # install deps (Course 2 uses --legacy-peer-deps per its tutorial)
npm run dev            # next dev
npm run build          # next build
npm run start          # next start
npm run lint           # next lint
```

App directories:
- Course 2: `Course_2_Authenticate_Users_With_TWA_SDK/example/web-app-to-twa-main/`
- Course 3: `Course_3_Connect_OKX_Wallet_Flow_EVM/example/okx-wallet-telegram-flow-evm-main/`
- Course 4: `Course_4_Connect_Flow_Wallet_Flow_Cadence/example/fcl-wallet-discovery-main/`
- Course 5: `Course_5_Connect_Privy_Wallet_Flow_EVM/example/privy-flow-evm-main/`

No test scripts are defined in any `package.json`. No formatter beyond `next lint`.

## Example App Stack

All four code examples share the same baseline (see each `package.json`):
- Next.js `15.0.3` with App Router, TypeScript 5, Tailwind 3.4, ESLint 8 + `eslint-config-next`.
- Courses 3–5 use React `19.0.0-rc-66855b96-20241106`; Course 2 uses React `^18.3.1`.

Course-specific dependencies:
- Course 2: `@twa-dev/sdk`, `@telegram-apps/init-data-node`
- Course 3: `@okxconnect/ui`, `@okxconnect/universal-provider`
- Course 4: `@onflow/fcl`, `@onflow/types` — configured for Flow **mainnet** in
  `example/fcl-wallet-discovery-main/flow-config.ts` (`accessNode.api` =
  `https://rest-mainnet.onflow.org`, `discovery.wallet` =
  `https://fcl-discovery.onflow.org/authn`)
- Course 5: `@privy-io/react-auth`, `@solana/web3.js`

Flow EVM mainnet chain id used in Course 3 (`AuthContext.tsx` tutorial snippet): `eip155:747`.

## Conventions and Gotchas

- **Course 1 has no buildable code.** `example/` and `solution/` contain only `README.md`
  files. Do not attempt to scaffold a project there unless asked.
- **Course 2 ships two lockfiles** (`package-lock.json` and `pnpm-lock.yaml` in
  `example/web-app-to-twa-main/`). Pick one package manager and stick with it; the tutorial
  uses npm with `--legacy-peer-deps`.
- **Hard-coded demo values in tutorials.** Course 2's `AuthContext.tsx` contains
  `const botId = 7210667871;` as a placeholder — any copy of that code needs the learner's
  own bot id before it will validate real Telegram `initData`.
- **Course 4 targets Flow mainnet by default** via `flow-config.ts`. Switching to testnet
  requires changing both `accessNode.api` and `flow.network`, and usually `discovery.wallet`.
- **Solution folders are intentionally empty.** `solution/README.md` is a submission
  placeholder (e.g., Course 1's is literally "Add the deeplink to your Telegram Web App
  here:"). Do not treat them as missing content.
- **Course naming uses underscores and is position-sensitive.** Folder names like
  `Course_3_Connect_OKX_Wallet_Flow_EVM` are referenced from the root `README.md`; renaming
  breaks the folder map.
- **Assets are shared.** Course READMEs reference `../assets/images/imageN.{png,webp,gif}`;
  moving an image will break multiple tutorials.

## Files Not to Modify

- `assets/images/*` — referenced by every course `README.md` via relative paths.
- `**/package-lock.json`, `**/pnpm-lock.yaml` — regenerate by running the package manager,
  not by hand-editing.
- `solution/README.md` in each course — owned by learners, not maintainers.
