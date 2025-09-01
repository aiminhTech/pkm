tags:: [[Go]], [[PostgreSQL]]

- https://github.com/jackc/pgx
-
- A [[PostgreSQL]] driver and toolkit for Go. It's a popular alternative to the standard `database\sql` drive with some added features specifically for Postgres.
- **Driver**: Lets Go programs connect to a PostgreSQL database
- **Toolkit**: Includes extra ultilities for working with Postgres, like connection ppoling, type mapping and better support for Postgres-specific features
-
- ## When to use?
	- Want **full Postgres features**, not just standard SQL
	- Care about **performance** and **efficient** data handling
	- Plan to use **connection pooling**
	-
- ## Installation
	- go get github.com/jackc/pgx/v4/stdlib
-
- ## Basic Example
	- ### `db.ts`
		- ```go
		  package store
		  
		  import (
		    "database/sql"
		    "fmt"
		  
		    _ "github.com/jackc/pgx/v4/stdlib"
		  )
		  
		  // Declares a function Open that:
		  // Returns *sql.DB (a database handle).
		  // Returns an error if something goes wrong.
		  func Open() (*sql.DB, error) {
		    // Calls sql.Open to create a connection handle using the pgx driver.
		    db, err := sql.Open("pgx", "host=localhost user=postgres password=postgres dbname=postgres port=5432 sslmode=disable")
		  
		    // Checks if sql.Open returned an error.
		    // If yes, wraps it with context using fmt.Errorf and returns it.
		    if err != nil {
		      return nil, fmt.Errorf("failed to open database: %w", err)
		    }
		  
		    // Returns the *sql.DB handle and nil error if everything is fine
		    return db, nil
		  }
		  
		  ```
	- ### `app.go`
		- ```go
		  type App struct {
		    DB   *sql.DB
		  }
		  
		  func NewApp() (*App, error) {
		    pgDb, err := store.Open()
		    if err != nil {
		      return nil, err
		    }
		  
		    app := &App{
		      Logger:         logger,
		      WorkoutHandler: workoutHandler,
		      DB:             pgDb,
		    }
		  
		    return app, nil
		  }
		  ```