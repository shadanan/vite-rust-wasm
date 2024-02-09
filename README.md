# Tutorial: Vite + Rust + WebAssembly Dev Environment

This repository is the result of the tutorial from the FriendlyTL about setting up a Vite + Rust + WebAssembly dev environment. In the process you will be able to select between JavaScript and TypeScript as well as your choice of frontend.

## Prerequisites

Ensure you have installed:

- Node.js
- NPM
- Rust

## Running Locally

1. Install wasm-pack.

   ```sh
   cargo install wasm-pack
   ```

1. Clone this repo.

   ```
   git clone https://github.com/shadanan/vite-rust-wasm.git
   cd vite-rust-wasm
   ```

1. Install node dependencies.

   ```sh
   npm install
   ```

1. Build the WebAssembly.

   ```sh
   wasm-pack build
   ```

1. Run the dev server.

   ```sh
   npm run dev
   ```

1. Navigate to http://localhost:5173/

## Steps to Reproduce

If you'd like to recreate this repository, you can follow these instructions:

1. Install wasm-pack.

   ```sh
   cargo install wasm-pack
   ```

1. Initialize a new wasm-pack project.

   ```sh
   wasm-pack new vite-rust-wasm
   ```

1. Initialize a Vite project in the same folder.

   ```sh
   cd vite-rust-wasm
   npm init vite .
   ```

   Make sure to ignore existing files and continue.

   You will also have the opportunity to choose which frontend framework, and whether to use TypeScript or JavaScript. For this repo, we used Svelte.

1. Install additional Node dev dependencies.

   ```sh
   npm install -D vite-plugin-wasm vite-plugin-top-level-await
   ```

1. Update `vite.config.ts`.

   ```typescript
   import { defineConfig } from "vite";
   import { svelte } from "@sveltejs/vite-plugin-svelte";
   import wasm from "vite-plugin-wasm";
   import topLevelAwait from "vite-plugin-top-level-await";

   // https://vitejs.dev/config/
   export default defineConfig({
     plugins: [svelte(), wasm(), topLevelAwait()],
   });
   ```

1. Update `src/lib.rs`.

   ```rust
   mod utils;

   use wasm_bindgen::prelude::*;

   #[wasm_bindgen]
   pub fn greet(name: &str) -> String {
       format!("Hello from Rust, {}!", name)
   }
   ```

1. Update `src/App.svelte`.

   ```svelte
   <script lang="ts">
     import { greet } from "../pkg/vite_rust_wasm";
   </script>

   <main>
     <div>
       <h1>Vite + Svelte + WebAssembly</h1>
       <h2>{greet("The Friendly TL")}</h2>
     </div>
   </main>
   ```

1. Build the WebAssembly.

   ```sh
   wasm-pack build
   ```

1. Run the dev server.

   ```sh
   npm run dev
   ```

1. Navigate to http://localhost:5173/
