<script>
  import KlassenKachel from "./KlassenKachel.svelte";
  let { stufen, heading } = $props();
</script>

<article class="Container {heading}">
  <h1>{heading}</h1>
    <section class="inner">
        {#each stufen as stufe}
          {#each stufe.klassen as klasse}
            <KlassenKachel  stufe={klasse.stufe} klasse={klasse.klasse} dati={klasse.dati} />
          {/each}
        {/each}
      </section>
</article>

<style>
  .Container { 
    height: 100%;
    display: flex;
    margin: 0;
    flex-direction: column;
    align-items: center;
  }
  .Container > h1 {
    font-size: 3rem;
    text-align: center;
  }
  .Container >  .inner {
    height: 80vh;
    width: 80%;
    padding: auto;
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;
    align-items: center;
    box-sizing: content-box;
  }

  .Unterstufe {
    flex-grow: 3; 
  }
  .Mittelstufe {
    flex-grow: 2; 
  }
  .Oberstufe {
    flex-grow: 1; 
  }
</style>

