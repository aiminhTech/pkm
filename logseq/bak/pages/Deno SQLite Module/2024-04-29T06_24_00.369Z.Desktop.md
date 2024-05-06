tags:: [[Javascript]], [[Typescript]]

- https://deno.land/x/sqlite@v3.8
- https://github.com/dyedgreen/deno-sqlite
- https://deno.land/x/sqlite@v2.4.2/docs/examples.md?source=
- This is an SQLite module for JavaScript and TypeScript. The wrapper is targeted
  at [Deno](https://deno.land/) and uses a version of SQLite3 compiled to WebAssembly (WASM).
- This module focuses on correctness, ease of use and performance.
- ## Example
	- ```typescript
	  import { DB } from "sqlite/mod.ts";
	  
	  const schema_ddl = `
	  PRAGMA foreign_keys = ON;
	  
	  CREATE TABLE IF NOT EXISTS calls (
	    id INTEGER PRIMARY KEY NOT NULL,
	    ts TEXT NOT NULL
	  ) STRICT;
	  
	  CREATE INDEX IF NOT EXISTS idx_calls_ts ON calls(ts);
	  
	  CREATE TABLE IF NOT EXISTS header_keys (
	    id INTEGER PRIMARY KEY NOT NULL,
	    keyname TEXT NOT NULL
	  ) STRICT;
	  
	  CREATE UNIQUE INDEX IF NOT EXISTS idx_header_keys_keyname ON header_keys(keyname);
	  
	  CREATE TABLE IF NOT EXISTS header_vals (
	    id INTEGER PRIMARY KEY NOT NULL,
	    val TEXT NOT NULL
	  ) STRICT;
	  
	  CREATE UNIQUE INDEX IF NOT EXISTS idx_header_vals_val ON header_vals(val);
	  
	  CREATE TABLE IF NOT EXISTS response_headers (
	    calls_id INTEGER REFERENCES calls(id),
	    header_keys_id INTEGER REFERENCES header_keys(id),
	    header_vals_id INTEGER REFERENCES header_vals(id),
	    PRIMARY KEY (calls_id, header_keys_id, header_vals_id)
	  ) WITHOUT ROWID, STRICT;
	  `;
	  
	  const db = initDB();
	  
	  // Open a database
	  function initDB(): DB {
	    const path = Deno.env.get("OPENAI_DB_PATH") ?? "openai.db";
	    const db = new DB(path);
	    db.execute(schema_ddl);
	    return db;
	  }
	  
	  export function saveResponseData(res: Response): void {
	  
	    const ts = new Date();
	    const calls = db.query(
	      "INSERT INTO calls (ts) VALUES (?) ON CONFLICT DO NOTHING RETURNING ID",
	      [ts],
	    );
	  
	    for (const keyname of Object.keys(resHeaders)) {
	      db.query(
	        "INSERT INTO header_keys (keyname) VALUES (?) ON CONFLICT DO NOTHING RETURNING ID",
	        [keyname],
	      );
	    }
	  
	    // Print out data in table
	    console.log("headers_keys");
	    for (const [id, keyname] of db.query("SELECT * FROM header_keys")) {
	      console.log(id, keyname);
	    }
	  
	    console.log("calls");
	    for (const [id, ts] of db.query("SELECT * FROM calls")) {
	      console.log(id, ts);
	    }
	  }
	  ```