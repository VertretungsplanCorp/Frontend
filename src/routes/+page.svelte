<script lang="ts">
  import { Server, type Klasse, type Stufen, type ApiResponse, type ApiPromise } from "vp-js-compat"; 
  import KlassenKachel from "$lib/KlassenKachel.svelte";
    import Container from "$lib/Container.svelte";

  let stufen: Array<Stufen> = $state(new Array);

  let url = 'http://vpapi.josewa.com'
  let server: Server = new Server(url); 
  let oberstufe = $state();
  server.getOberstufe().then((r: ApiResponse<Stufen>) => {
      oberstufe = r.data.stufen  
  });
  let unterstufe = $state();
  server.getUnterstufe().then((r: ApiResponse<Stufen>) => {
      unterstufe = r.data.stufen  
  });
  let mittelstufe = $state();
  server.getMittelstufe().then((r: ApiResponse<Stufen>) => {
      mittelstufe = r.data.stufen  
  });
  
</script>

<svelte:head>
	<title>Vertretungsplan</title>
	<meta name="description" content="Besserer Vertretungsplan" />
</svelte:head>

<section>
  <Container stufen={unterstufe} heading="Unterstufe"></Container>
  <Container stufen={mittelstufe} heading="Mittelstufe"></Container>
  <Container stufen={oberstufe} heading="Oberstufe"></Container>
</section>

<style>
	section {
    height: 100vh;
    width: 100vw;
    padding: 1rem;
    box-sizing: border-box;
		display: flex;
		flex-direction: row;
		justify-content: space-around;
		align-items: center;
	}
</style>
