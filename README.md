# p2p_rust

A **desktop application** built with **Tauri** (Rust backend) and a **Vite** web frontend, using **libp2p** for peer-to-peer networking.

> Branch: `master`

## Tech stack

- **Tauri** (`src-tauri/`) — Rust application backend + desktop packaging
- **Vite** frontend — app UI (see `src/`, `index.html`, `vite.config.js`)
- **libp2p (Rust)** — P2P networking layer

## Repository layout

- `src-tauri/` — Tauri (Rust) project (backend, commands, app config)
- `src/` — frontend source (Vite app)
  - `src/App.vue` — main UI component
  - `src/main.js` — frontend entrypoint
- `public/` — frontend static assets
- `RUN_APP.sh` — helper script to run the app
- `package.json` / `package-lock.json` — frontend dependencies & scripts
- `index.html` / `vite.config.js` — Vite configuration

## Prerequisites

- **Node.js + npm** (for the frontend)
- **Rust toolchain** (stable) + `cargo`
- **Tauri prerequisites** for your OS  
  (system dependencies like a C compiler, platform webview, etc.)

## Install

Frontend dependencies:

```bash
npm install
```

Rust dependencies are handled by Cargo during the Tauri build.

## Run (development)

### Option 1: use the provided script

```bash
bash RUN_APP.sh
```

### Option 2: run with Tauri directly

Most Tauri + Vite apps use:

```bash
npm run tauri dev
```

If your `package.json` uses different script names, run:

```bash
npm run
```

…and choose the appropriate dev command.

## Build (release)

Typical Tauri release build:

```bash
npm run tauri build
```

This produces an installable application bundle for your OS.

## What it does (high level)

This app combines a desktop UI with a Rust backend that participates in a **libp2p-based peer-to-peer network**. Depending on the implemented libp2p behaviours (e.g., pubsub, request/response, mDNS discovery), it can discover peers, exchange messages, and/or transfer data directly between nodes without a central server.

## Notes / configuration

- App behaviour and networking settings (listen addresses, peer discovery, protocol IDs, etc.) are typically configured in the Rust backend under `src-tauri/`.
- The frontend UI lives in `src/App.vue` and interacts with the backend via Tauri commands/events.
