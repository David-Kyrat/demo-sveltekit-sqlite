<script>
  import { json, error } from "@sveltejs/kit";

  import Database from "better-sqlite3";
  import fs from "node:fs";

  db = new Database(fs.readFileSync("superheroes.db"));

  export function GET({ url }) {
    const query = url.searchParams.get("q");
    if (!query) {
      throw error(401, "Query (`?q=`) is required");
    }
    const stmt = db.prepare("select * from superheroes where name like ?");

    return json(stmt.all(`%${query}%`));
  }
</script>

<svelte:head>
  <meta name="db req" />
  <title>dbb req</title>
</svelte:head>

<h1 class="text-3xl font-bold">
  Example reading data from a local SQLite database
</h1>
