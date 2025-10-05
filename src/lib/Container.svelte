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
    padding: 1rem;
    box-sizing: content-box;
    margin: 0;
    flex-direction: column;
    align-items: center;
  }
  .Container > h1 {
    width: calc(100% - 4rem);
    border-style: solid;
    border-color: orange;
    border-width: 0.4rem;
    border-radius: 1rem;
    padding: 1rem;
    font-size: 2rem;
    text-align: center;
  }
  .Container > .inner {
    flex-grow: 1;
    width: 100%;
    display: flex;
    flex-direction: column;
    overflow: hidden;
    flex-wrap: wrap;
    box-sizing: content-box;
  }


  .Unterstufe {
    flex-grow: 3; 
  }
  .Mittelstufe {
    flex-grow: 3; 
  }
  .Oberstufe {
    flex-grow: 3; 
  }
</style>

