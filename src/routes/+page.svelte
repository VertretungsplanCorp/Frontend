<script lang="ts">
  import { Server, type Info, type Stufen, type ApiResponse } from "vp-js-compat"; 
  import Container from "$lib/Container.svelte";

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
  let infos = $state();
  server.getInfo().then((r: ApiResponse<Info>) => {
    infos = r.data
  });
</script>

<svelte:head>
	<title>Vertretungsplan</title>
	<meta name="description" content="Besserer Vertretungsplan" />
</svelte:head>

<article>
<section>
  <Container stufen={unterstufe} heading="Unterstufe"></Container>
  <Container stufen={mittelstufe} heading="Mittelstufe"></Container>
  <Container stufen={oberstufe} heading="Oberstufe"></Container>
</section>
<aside>
  <h1>Infos</h1>
  <div>
    {infos}
  </div>
</aside>
</article>

<style>
  article {
    display: flex;
    flex-direction: row;
  }
  aside {
    flex-grow: 1;
    color: white;
    background: linear-gradient(to right, #800, #4b0000);
    display: flex;
    flex-direction: column;
    align-items: left;
    padding: 3rem;
    box-sizing: content-box;
    gap: 2em;
    filter: drop-shadow(0.2rem 0rem 1.1rem #626262);
  }
  aside > h1 {
    font-size: 2rem;
    font-weight: bold;
    margin: 0;
    padding: 0;
  }
	section {
    flex-grow: 5;
    height: 100vh;
    padding: 1rem;
    box-sizing: border-box;
		display: flex;
		flex-direction: row;
		justify-content: space-around;
		align-items: center;
	}
</style>
