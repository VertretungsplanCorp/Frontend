<script>
    let { vertretung, color } = $props();
    let ausfall = $state(vertretung.fach_neu === null || vertretung.raum_neu === null);
    document.documentElement.style.setProperty('--color', color);
</script>

<table class:ausfall={ausfall}>
    <tbody>
    <tr>
        <td class="stunde">
          {#if ausfall}
            <del>{vertretung.stunde}</del>
          {:else}
            <strong>{vertretung.stunde}</strong>
          {/if}
        </td>
        <td class="fach">
          <del>{vertretung.fach}</del>
          <strong>{vertretung.fach_neu}</strong>
        </td>
        {#if vertretung.lehrer}
          <td class="lehrer">
            <del>{vertretung.lehrer}</del>
            <strong>{vertretung.lehrer_neu}</strong>
          </td>
        {/if}
        {#if vertretung.raum || vertretung.raum_neu}
          <td class="raum">
            <del>{vertretung.raum}</del>
            <strong>{vertretung.raum_neu}</strong>
          </td>
        {/if}
    </tr>
    {#if vertretung.text}
        <tr class="info">
            <td colspan="4">{vertretung.text}</td>
        </tr>
    {/if}
    </tbody>
</table>

<style>
    * {
        margin: 0;
        padding: 0;
        border-collapse: collapse;
    }

    td {
        border-width: 0.1rem;
        color: black;
        border-color: var(--color);
        font-size: 0.75rem;
        border-style: solid;
        border-bottom: none;
        border-top: none;
        padding: 0.3rem;
    }
  
    table, tbody, tr {
      width: 100%;
    }

    table {
        border-width: 0.15rem;
        border-color: var(--color);
        border-style: solid;
    }

    table.ausfall {
        background-color: rgba(244, 0, 0, 0.2);
    }

    .info {
        border-width: 0.1rem;
        border-color: var(--color);
        border-top-style: dashed;
    }

    .stunde {
      width: 1rem;
    }
    .fach {
      width: 2rem;
    }
</style>
