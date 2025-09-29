<script>
  import Datum from "./Datum.svelte";

  let { dati, klasse, stufe } = $props();

  function getRandomVibrantColor() {
      // Hue: 0-360 (full color spectrum)
      const hue = Math.floor(Math.random() * 360);

      // Saturation: high for vibrant colors (e.g., 80-100%)
      const saturation = Math.floor(Math.random() * 20) + 80;

      // Lightness: medium range for vibrancy (e.g., 40-60%)
      const lightness = Math.floor(Math.random() * 20) + 40;

      // Return as HSL string
      return `hsl(${hue}, ${saturation}%, ${lightness}%)`;
  }

  let color = getRandomVibrantColor();

  document.documentElement.style.setProperty('--color', color);
</script>

<div class="kachel">
    <div class="klasse container">
      <div class="klasse schild">{stufe}{klasse}</div>
    </div>
    <div class="content container">
      {#each dati as datum}
          <Datum datum={datum} color={color} />
      {/each}
    </div>
</div>

<style>
    .kachel {
      margin: 0.5rem;
      height: fit-content;
      width: 10rem;
    }

    .content.container {
      border-color: var(--color);
      border-style: solid;
      border-width: 0.25rem;
      border-radius: 1rem;
      background-color: white;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 0.5rem;
    }

    .klasse.schild {
      z-index: 2;
      position: absolute;
      left: -0.5rem;
      top: -0.5rem;
      width: 3rem;
      height: 3rem;
      line-height: 3rem;
      font-size: 1.5rem;
      border-radius: 50%;
      background-color: white;
      border-color: var(--color);
      color: var(--color);
      text-align: center;
      border-style: solid;
      border-width: 0.25rem;
    }
    
    .klasse.container {
      height: 0;
      width: 0;
      position: relative;
    }
</style>
