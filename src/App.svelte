<script>
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

<h1>Rick and Morty Svelte</h1>

<div>
  <button on:click={prevPage} disabled={page === 1}>Previous</button>
  <button on:click={nextPage} disabled={page === 42}>Next</button>
</div>

<div>
  {#each characters as character}
    <div>
      <img src={character.image} alt={character.name} />
      <h2>{character.name}</h2>
      <h3>{character.species}</h3>
    </div>
  {/each}
</div>
