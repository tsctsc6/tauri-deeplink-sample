<script lang="ts">
  import svelteLogo from "./assets/svelte.svg";
  import viteLogo from "/vite.svg";
  import Counter from "./lib/Counter.svelte";
  import { onOpenUrl, getCurrent } from "@tauri-apps/plugin-deep-link";
  import { onMount } from "svelte";

  let deepLink: string[] | string | null = $state(null);

  onMount(async () => {
    // tauri-deeplink-sample://test?p=1
    // src-tauri/capabilities/default.json: 添加 deep-link 权限
    deepLink = await getCurrent();
    await onOpenUrl((urls) => {
      deepLink = urls;
    });
  });
</script>

<main>
  <div>
    <a href="https://vite.dev" target="_blank" rel="noreferrer">
      <img src={viteLogo} class="logo" alt="Vite Logo" />
    </a>
    <a href="https://svelte.dev" target="_blank" rel="noreferrer">
      <img src={svelteLogo} class="logo svelte" alt="Svelte Logo" />
    </a>
  </div>
  <h1>Vite + Svelte</h1>

  <p>
    deep link:
    {#if deepLink}
      {#if Array.isArray(deepLink)}
        {deepLink.join(", ")}
      {:else}
        {deepLink}
      {/if}
    {:else}
      (none)
    {/if}
  </p>

  <div class="card">
    <Counter />
  </div>

  <p>
    Check out <a
      href="https://github.com/sveltejs/kit#readme"
      target="_blank"
      rel="noreferrer">SvelteKit</a
    >, the official Svelte app framework powered by Vite!
  </p>

  <p class="read-the-docs">Click on the Vite and Svelte logos to learn more</p>
</main>

<style>
  .logo {
    height: 6em;
    padding: 1.5em;
    will-change: filter;
    transition: filter 300ms;
  }
  .logo:hover {
    filter: drop-shadow(0 0 2em #646cffaa);
  }
  .logo.svelte:hover {
    filter: drop-shadow(0 0 2em #ff3e00aa);
  }
  .read-the-docs {
    color: #888;
  }
</style>
