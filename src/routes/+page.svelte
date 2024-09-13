<script lang="ts">
  import icebreakerFile from "$lib/icebreakers.txt?raw";
  import { onMount } from "svelte";
  import Header from "./header.svelte";

  const icebreakers = icebreakerFile.split("\n").filter(Boolean);
  const warnings: string[] = [];

  $: icebreaker = "";
  function randomIcebreaker() {
    icebreaker = icebreakers[Math.floor(Math.random() * icebreakers.length)];
  }

  function shareJoke() {
    if (navigator.share) {
      navigator
        .share({
          title: icebreaker,
          text: icebreaker,
          url: window.location.href,
        })
        .then(() => console.log("Successful share"))
        .catch((error) => warnings.push("Error sharing: " + error));
    } else {
      warnings.push("Web Share API not supported");
    }
  }

  onMount(randomIcebreaker);
</script>

<Header />
<h1>{icebreaker}</h1>
<button on:click={randomIcebreaker}>Get Question</button>
<button on:click={shareJoke}>Share</button>

<p class="footer">-- pool has {icebreakers.length} ice breakers --</p>

{#if warnings.length > 0}
  <h2>Warnings</h2>
  <ul>
    {#each warnings as warning}
      <li>{warning}</li>
    {/each}
  </ul>
{/if}

<style>
  button {
    display: inline;
  }
  .footer {
    color: var(--neutral-3);
    font-size: smaller;
    text-align: center;
  }
</style>
