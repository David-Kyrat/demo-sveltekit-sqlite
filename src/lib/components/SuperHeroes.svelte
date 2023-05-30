<script>
  import { marked } from "marked";
  const fields = [
    "id",
    "name",
    "eye_color",
    "hair_color",
    "appearance_count",
    "first_appearance",
    "first_appearance_year",
  ];
  function capitalize(str) {
    return str[0].toUpperCase() + str.slice(1);
  }
  function sanitize(str) {
    return str
      .split("_")
      .map((s) => capitalize(s))
      .join(" ");
  }
  const wanted_fields = [fields[1], fields[3], fields[5], fields[4]];
  const li_class = "w-full flex justify-between";
  function format_header() {
    let col1 = wanted_fields.map((field) => sanitize(field)).join("|");
    let col2 = wanted_fields.map((_) => "-").join("|");
    let str = `${col1}\n${col2}`;
    return str;
  }
  function format(item) {
    return wanted_fields.map((field) => item[field]).join("|");
  }

  export let items = [];

  function format_resp() {
    return `${format_header()}\n${items
      .map((item) => format(item))
      .join("\n")}`;
  }
</script>

<ul>
  <li class={li_class}>
    {#if items && items.length > 0}
      {@html marked(format_resp())}
    {:else}
      No Results
    {/if}
  </li>
</ul>

<!-- <li class={li_class}>
    {#each wanted_fields as header}
      <span>{sanitize(header)}</span>
    {/each}
  </li> -->
<!-- {#each items as item}
    <li>
      {format(item)} -->
<!-- {#each wanted_fields as field}
        <span> {item[field]} | </span>
      {/each} -->

<!-- {item.name}
      {#if item.first_appearance_year}
        <span>First appearance: {item.first_appearance_year}</span>
      {/if} -->
<!-- </li>
  {/each} -->
