<script>
  import Character from "./lib/Character.svelte";

  let characters = [];
  let page = 1;
  const loadCharacters = async () => {
    const response = await fetch(
      "https://rickandmortyapi.com/api/character?page=" + page
    );
    const data = await response.json();
    characters = data.results;
  };

  loadCharacters();

  const nextPage = () => {
    page++;
    loadCharacters();
  };

  const prevPage = () => {
    page--;
    loadCharacters();
  };
</script>

<h1 class="title">Rick and Morty Svelte</h1>


<div class="container">
  <div class="btns">
    <button on:click={prevPage} disabled={page === 1}>Previous</button>
    <button on:click={nextPage} disabled={page === 42}>Next</button>
  </div>
  <div class="grid">
    {#each characters as character}
      <Character {character} />
    {/each}
  </div>
</div>
