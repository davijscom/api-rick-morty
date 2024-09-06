<script>
  import Cards from './lib/Cards.svelte';

  let caracteres = [];
  let pagina = 1;

  async function loadCharacters() {
    const response = await fetch('https://rickandmortyapi.com/api/character?page=' + pagina);
    const data = await response.json();
    caracteres = data.results;
  }

  // Corrección: Llamada a la función correcta
  loadCharacters();
  function siguiente() {
    pagina++;
    loadCharacters();
  }

  function anterior() {
    if (pagina > 1) {
      pagina--;
      loadCharacters();
    }
  }
</script>

<h1 class="title">Rick and Morty Svelte</h1>
<h2 class="title">Página: {pagina}</h2>

<div class="botones">
  <button class="boton" on:click={anterior} disabled={pagina === 1}>Anterior</button>
  <button class="boton" on:click={siguiente}>Siguiente</button>
</div>

<div class="grid">
  {#each caracteres as caracter}
    <!-- Pasar el caracter individual al componente Cards -->
    <Cards {caracter} />
  {/each}
</div>

<style>
  /* Agrega tus estilos aquí */
</style>
