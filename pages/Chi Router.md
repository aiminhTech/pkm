tags:: [[Go]]

- https://github.com/go-chi/chi
- A lightweight and idiomatic router for Go
-
- ## Installation
	- ```bash
	  go get -u github.com/go-chi/chi/v5
	  ```
- ## Why use?
	- Lightweight and fast
	- Supports middlewares easily
	- Makes building  REST APIs simple and clean
	- Path params, wildcards and nested routes are easy
	-
- ## Basic Example
	- ### `app.go`
		- ```go
		  func (a *App) HealthCheck(w http.ResponseWriter, r *http.Request) {
		  	fmt.Fprintln(w, "Status is available")
		  }
		  ```
	- ### `routes.go`
		- `SetupRoutes` is a function that **creates and configures a Chi router**.
		- `chi.NewRouter()` creates a new router instance.
		- `r.Get("/health", app.HealthCheck)` connects the `/health` path to the `HealthCheck` method on your `App`.
		- Returns the configured router, ready to be used in `main.go`.
		- **Benefits**:
			- Keeps routing logic separate from business logic.
			- Easy to add more routes without touching `main.go`.
		- ```go
		  package routes
		  
		  import (
		  	"git.ipip.ch/quach/learning-go/internal/app"
		  	"github.com/go-chi/chi/v5"
		  )
		  
		  func SetupRoutes(app *app.App) *chi.Mux {
		  	r := chi.NewRouter()
		  
		  	r.Get("/health", app.HealthCheck)
		  	return r
		  }
		  ```
	- ### `main.go`
		- ```go
		  import (
		  	"git.ipip.ch/quach/learning-go/internal/app"
		  	"git.ipip.ch/quach/learning-go/internal/routes"
		  )
		  
		  func main () {
		    // rest of code ...
		    
		    // Setup routes with Chi
		    r := routes.SetupRoutes(app)
		  
		    server := &http.Server{
		      Addr:    ":8080",
		      Handler: r,
		    }
		  }
		  ```
		-