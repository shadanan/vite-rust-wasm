<script lang="ts">
  import { greet } from "../pkg/vite_rust_wasm";
</script>

<main>
  <div>
    <h1>Vite + Svelte + WebAssembly</h1>
    <h2>{greet("The Friendly TL")}</h2>
  </div>
</main>
