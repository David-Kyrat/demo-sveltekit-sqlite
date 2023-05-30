<script>
  /*let btn_class =
    "relative inline-flex items-center justify-center p-0.5 mb-2 ml-20 mr-2 overflow-hidden text-sm font-medium hover:bg-gray-900 text-gray-900 rounded-lg group bg-gradient-to-br from-purple-600 to-blue-500  white:text-dark focus:ring-2 focus:outline-none focus:ring-blue-200 white:focus:ring-blue-800";
  let btnspan_class =
    "relative px-5 py-2.5 transition-all ease-in duration-75 bg-white white:bg-gray-900 rounded-md group-hover:text-violet-600";*/

  import FancyBtn from "$lib/components/FancyBtn.svelte";
  let a = 0;
  let b = 0;
  let total = 0;

  async function add() {
    const response = await fetch("/api/add", {
      method: "POST",
      body: JSON.stringify({ a, b }),
      headers: {
        "content-type": "application/json",
      },
    });

    total = await response.json();
  }
</script>

<div class="prose">
  <input type="number" bind:value={a} /> +
  <input type="number" bind:value={b} /> =
  {total}

  <FancyBtn text="add" on_click={add} style="margin-left: 50px" />
</div>

<style>
  input {
    height: 3em;
    border: 1.5px solid darkslategray;
    padding: 10px 20px;
    margin: 0px 20px;
    border-radius: 20px;
  }
</style>
