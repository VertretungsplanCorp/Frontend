<script>
  import Datum from "./Datum.svelte";

  let { dati, klasse, stufe } = $props();

  function getRandomVibrantColor() {
      console.log(stufe);
      let rand = 1/Math.pow(stufe, 2)*1000
      console.log(rand);

      // Hue: 0-360 (full color spectrum)
      const hue = Math.floor(rand * 360);

      // Saturation: high for vibrant colors (e.g., 80-100%)
      const saturation = 80;

      // Lightness: medium range for vibrancy (e.g., 40-60%)
      const lightness = 50;

      // Return as HSL string
      return `hsl(${hue}, ${saturation}%, ${lightness}%)`;
  }

  let color = getRandomVibrantColor();
  console.log(color);

</script>

<div class="kachel" style="--color: {color}">
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
      height: max-content;
      margin: 1rem;
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
      font-size: 1em;
      border-radius: 50%;
      background-color: white;
      font-weight: bold;
      border-color: var(--color);
      color: var(--color);
      text-align: center;
      border-style: solid;
      border-width: 0.25rem;
    }
    
    .klasse.container {
      border-style: solid;
      border-color: yellow;
      border-width: 0.3rem;
      height: 0;
      width: 0;
      position: relative;
    }
</style>
