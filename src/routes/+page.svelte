<script>
  import SuperHeroes from "$lib/components/SuperHeroes.svelte";
  import FancyBtn from "../lib/components/FancyBtn.svelte";

  const description = "Here's my description!";
  async function update(value) {
    if (value && value.length > 0) {
      items = [];
      input = "waiting...";
      items = await fetch(`/heroes?q=${value.trim()}`).then((v) => v.json());
      input = "";
    }
    //http://localhost:5173/heroes?q=
  }
  let items = [];
  let value;
  $: update(value);

  let input = "";

  function handleSubmit() {
    value = input;
  }
</script>

<svelte:head>
  <meta name="description" content={description} />
  <title>Here's a title!</title>
</svelte:head>

<h1 class="text-4xl font-bold">
  Example reading data from a local SQLite database
</h1>
<hr />
<br />
<label>
  Enter something here:
  <input
    class="p-2"
    type="search"
    autocomplete="on"
    placeholder="Search in database"
    bind:value={input}
    style="margin: 2em 1em;"
  />
</label>

<FancyBtn text="Submit" on_click={handleSubmit} padding_x="px-8" style="margin-left: 2em;"/>

<br />

<FancyBtn text="clear" on_click={_ => items = []} padding_x="px-5" />

<!-- <div style="padding: 20px 0px">
  <p>Entered value: "{input}"</p>
</div> -->

<h2 class="text-2xl font-bold" style=" padding-top: 40px">Results</h2>
<hr />

<SuperHeroes {items} />

<style>
  hr {
    margin-top: 1em;
    padding-bottom: 1.5em;
  }
</style>
