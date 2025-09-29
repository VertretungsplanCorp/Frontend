<script lang="ts">
  import { Server, type Klasse, type Stufen, type ApiResponse, type ApiPromise } from "vp-js-compat"; 
  import KlassenKachel from "$lib/KlassenKachel.svelte";

  let stufen: Array<Stufen> = $state(new Array);

  let url = 'http://vpapi.josewa.com'
  let server: Server = new Server(url); 
  server.getOberstufe().then((r: ApiResponse<Stufen>) => {
      let s: Stufen = r.data;  
      console.log("Stufen: ", s);
      stufen = s.stufen;
  });
  
</script>

<svelte:head>
	<title>Vertretungsplan</title>
	<meta name="description" content="Besserer Vertretungsplan" />
</svelte:head>

<section>
  <article class="stufen-container">
    {#each stufen as stufe}
      {#each stufe.klassen as klasse}
        <KlassenKachel  stufe={klasse.stufe} klasse={klasse.klasse} dati={klasse.dati} />
      {/each}
    {/each}
  </article>
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}

  .stufen-container {
    height: 50vh;
    width: 93.5vw;
    display: grid;
    grid-template-columns: repeat(
      auto-fit,
      12rem
    );
    grid-template-rows: masonry;
    overflow-y: scroll;
    border-radius: 2rem;
    border-width: 0.2rem;
    border-style: dashed;
    margin: 2rem;
    padding: 1rem;
  }

	h1 {
		width: 100%;
	}
</style>
