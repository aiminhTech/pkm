tags:: [[Golang]], [[PostgreSQL]]
id:: 68a47736-9161-4537-a1ca-afa7a17f1fe2

- https://github.com/pressly/goose
- https://pressly.github.io/goose/
-
- A lightweight DB migration tool for Go
- It allows developers to manage DB schema changes through incremental SQL scripts or Go functions, facilitating version-controlled and reversible DB migrations
-
- ## Installation
	- ```bash
	  go install github.com/pressly/goose/v3/cmd/goose@latest
	  go get github.com/pressly/goose/v3/cmd/goose@latest
	  ```
-
- ## Purpose
	- When developing software, our DB schema envolves adding tables, changing columns, creating indexes, populating seed data, etc.
	- Goose tracks these changes so we can
		- Apply migrations in the correct order
		- Roll back changes if needed
		- Keep development, staging and production DB in sync
-
- ## How it works
	- Goose uses **versioned migration files**
	- Each migration has a version number in its filename. For example:
		- ```sql
		  001_users.sql
		  002_workouts.sql
		  003_workout_entries.sql
		  ```
	- Goose records the **current version** in the DB (usually in a table called `goose_db_version`)
	- When we run `goose up`, it applies any migrations with a higher version than the current one
	- ### Up Migration
		- Apply new changes to DB schema
		- Goose looks at the current version in the DB and runs all migrations with a **higher version number**
		- ```sql
		  -- +goose Up
		  -- +goose StatementBegin
		  CREATE TABLE IF NOT EXISTS users (
		    id BIGSERIAL PRIMARY KEY,
		    username VARCHAR(50) UNIQUE NOT NULL
		  )
		  -- +goose StatementEnd
		  ```
		- This SQL will create the table when we run `goose up`
	- ### Down Migrations
		- Roll back changes made by an UP migration
		- Goose run the Down statements for the most recent migration or a specific version to undo changes
		- ```sql
		  -- +goose Down
		  -- +goose StatementBegin
		  DROP TABLE users;
		  -- +goose StatementEnd
		  ```
		- Running `goose down` will delete the users-Table, undoing the last migration