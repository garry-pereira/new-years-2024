<script>
  import { onMount } from "svelte"

  const newYears = Math.floor((new Date(2024, 0, 1, 0, 0, 0).getTime() / 1000))
  let dateSeconds = Math.floor(new Date().getTime() / 1000)

  let dateMinutes = Math.floor(dateSeconds / 60)

  let newSeconds = newYears - dateSeconds
  let newMinutes = Math.floor(newYears / 60) - dateMinutes

  const syncDate = () => {
    setInterval(() => {
      dateSeconds = Math.floor(new Date().getTime() / 1000)
      dateMinutes = Math.floor(dateSeconds / 60)

      newSeconds = newYears - dateSeconds
      newMinutes = Math.floor(newYears / 60) - dateMinutes
    }, 500)
  }

  onMount(() => {
    syncDate()
  })
</script>

{#if dateSeconds < newYears}
  <div class="contain">
    <h1>{newSeconds}</h1>
    <button on:click={syncDate}>
      sync
    </button>
  </div>
{:else}
  <div class="contain">
    <h1>2024</h1>
    <h2>🎉 happy new years 🥳</h2>
    <p>🍾 champagne time 🥂</p>
  </div>
{/if}

<style>
  .contain {
    margin-top: 5em;
    display: flex;
    flex-direction: column;
    gap: 2em;
  }
</style>