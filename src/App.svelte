<script>
  import Character from "./lib/character.svelte";
  let character = [];
  let page = 1;

  async function Loadcharacter() {
    const response = await fetch(
      "https://rickandmortyapi.com/api/character?page=" + page
    );
    const data = await response.json();
    console.log(data);
    character = data.results;
  }
  Loadcharacter();

  function NextPage() {
    page++;
    Loadcharacter();
  }

  function PreviusPage() {
    page--;
    Loadcharacter();
  }
</script>

<h1 class="title">Rick and morty Svelte</h1>

<div class="container">
  <div class="btns">
    <button class="btn" on:click={PreviusPage} disabled={page === 1}>Previus</button>
    <button class="btn" on:click={NextPage}>Next</button>
  </div>
  <div class="grip">
    {#each character as character}
      <Character {character}></Character>
    {/each}
  </div>
</div>
