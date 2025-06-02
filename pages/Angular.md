tags:: [[TypeScript]], [[HTML]], [[CSS]], [[RxJS]], [[Ng Bootstrap]], [[NgModule]], [[Angular Material]]

- https://angular.dev/
- Angular is a web framework used to be build scalable web apps with confidence
- **Use**
	- [[TypeScript]]: to programm logic in the application
	- [[HTML]]: to define markup in templates
	- [[CSS]]: to style the template
-
- ## Courses
  collapsed:: true
	- https://frontendmasters.com/courses/production-angular/ #frontentmaster
	- https://frontendmasters.com/courses/angular-fundamentals/ #frontentmaster
	  collapsed:: true
		- https://static.frontendmasters.com/assets/courses/2024-01-29-angular-fundamentals/angular-fundamentals-slides.pdf
		- https://github.com/MarkTechson/angular-fundamentals-lessons
	- [Learn Angular for Modern Web Applications [Video]]([https://learning.oreilly.com/course/learn-angular-for/9780137324842/](https://learning.oreilly.com/course/learn-angular-for/9780137324842/)) #OReilly
- ## Why Angular?
  collapsed:: true
	- **Motivation**:
		- Many companies have adopted Angular, leading to numerous job postings.
		- Understanding Angular's purpose and benefits is as crucial as learning to use it.
	- **What is Angular?**:
		- **Angular** is an open-source, front-end framework created and maintained by Google, along with the open-source community.
		- It's designed to help developers create maintainable, performant applications swiftly.
		- Encourages organized front-end development with a robust structure.
	- **Benefits of Angular**:
		- **Modular Components**: Allows code reuse across the application, reducing redundancy.
		- **Written in TypeScript**: A statically-typed dialect of JavaScript that helps keep code organized and maintainable, especially for larger applications.
		- **Longevity and Support**: Around since 2010 (major changes in 2015), ensuring extensive online help and community support.
	- **Comparison with React and Vue**:
		- **React**:
			- A library (not a full framework like Angular).
			- Offers flexibility in how things are done, which can be both a strength and a challenge.
		- **Vue**:
			- Easier to integrate into existing websites gradually.
			- Less daunting for incremental adoption compared to Angular, which is more suited for starting projects from scratch.
		- **Angular**:
			- Provides a structured, "right way" to do everything.
			- Better for building applications from the ground up rather than integrating into existing projects.
- ## Installation
	- https://angular.dev/tools/cli/setup-local
	- ```bash
	  sudo npm install -g @angular/cli
	  ```
- ## Angular CLI
  collapsed:: true
	- https://v17.angular.io/cli
	- ### Create new project
		- ```bash
		  ng new <project-name>
		  ```
	- ### Create new component
		- https://v17.angular.io/cli/generate
		- ```bash
		  ng generate component example
		  
		  //or
		  
		  ng g c example
		  ```
		- Is used in Angular's CLI to generate a new component named `example`
		- This will create a folder with component files (like `.ts`, `.html`, `.css`, `.spec.ts`) set up for you.
	- ### Create new service
		- ```ts
		  ng generate service example
		  
		  //or
		  
		  ng g s example
		  ```
-
- ## `main.ts`
  collapsed:: true
	- The main *entry point for the application*. This file is essential as it sets up the Angular environment and bootstraps the root module, typically `AppModule`, which then starts the application.
	- In summary, `main.ts` is fundamental in Angular application startup, handling the environment configuration, and bootstrapping the root Angular module.
	- **Example**
		- ```ts
		  import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';
		  import { enableProdMode } from '@angular/core';
		  import { AppModule } from './app/app.module';
		  import { environment } from './environments/environment';
		  
		  if (environment.production) {
		    enableProdMode();
		  }
		  
		  platformBrowserDynamic().bootstrapModule(AppModule)
		    .catch(err => console.error(err));
		  
		  ```
		- **Importing Angular Modules and Core Functions:** `main.ts` imports necessary Angular packages, notably the `platformBrowserDynamic` function from `@angular/platform-browser-dynamic` and the root `AppModule` from application files.
		- **Bootstrapping the Root Module:**
			- The `platformBrowserDynamic().bootstrapModule(AppModule)` starts the application by bootstrapping `AppModule`.
		- **Enabling Production Mode (Optional):** If the application is in production mode, `enableProdMode()` is called to disable Angular's development mode, which can include additional checks that are not necessary in production.
- ## Modules `app.module.ts`
  collapsed:: true
	- https://angular.dev/style-guide#app-root-module
	- Are used to group components, directives, pipes, and services that are related to each other.
	- **NgModule Decorator**: We define a module using the `@NgModule` decorator. This decorator takes a metadata object that tells Angular how to compile and launch the application.
	- **Features**:
		- **Declarations**: Components, directives, and pipes that belong to the module.
		- **Imports**: Other modules that this module needs (often including Angular's core modules or third-party modules).
		- **Providers**: Services that the module contributes to the global collection of services.
		- **Bootstrap**: The main application view, called the root component, which hosts all other app views. Only the root module should set this property.
	- ### Infos
		- From Angular v17 onwards, Standalone is now the new default for the CLI
		- So when you create a new project, you won't have any modules in it if you don't specify anything. However, it is still possible to create a module-based app by using the `--no-standalone` flag :
			- ```bash
			  ng new --no-standalone
			  ```
		- Standalone components are a feature introduced in v14. With the change in v17, the Angular team [strongly recommends to use them](https://blog.angular.io/introducing-angular-v17-4d7033312e4b#586d) as they are easier to use, understand and are require less boilerplate.
	- ### Why Use Modules?
		- **Modularity**: Angular Modules help in organizing an application into cohesive blocks of functionality. This promotes reusability and maintainability.
		- **Dependency Management**: Modules allow Angular to efficiently manage dependencies between different parts of the application.
		- **Encapsulation**: Each Angular Module can be designed to encapsulate a specific feature or part of the application, keeping the codebase clean and manageable.
-
- ## Component
	- ### Syntax
	  collapsed:: true
		- The `@Component` decorator annotates a class to specify that it is a component.
		- Each property within the decorator serves a different purpose:
			- `selector` is the custom HTML tag.
				- The `selector` property in an Angular component specifies the custom HTML tag that will represent this component in the application's HTML.
				- When Angular encounters this tag in the DOM, it replaces it with the component's template and applies its associated logic.
			- `standalone` denotes if the component is self-sufficient.
				- In Angular, the `standalone` property being set to `true` indicates that the component is self-contained and does not need to be declared within an Angular module to be used.
			- `template` contains the HTML content.
			- `styles` are for CSS specifics.
		- ```ts
		  import { Component } from '@angular/core';
		  
		  @Component({
		    selector: 'app-root',
		    standalone: true,
		    template: `
		      <h1>If you are reading this...</h1>
		      <p>Things have worked out well! 🎉</p>
		    `,
		    styles: ``,
		  })
		  ```
		- ```ts
		  import { Component } from '@angular/core';
		  
		  @Component({
		    selector: 'app-example',       
		    templateUrl: './example.component.html', 
		    styleUrls: ['./example.component.css']   
		  
		  ```
	- ### Composition
	  collapsed:: true
		- ```ts
		  //userinfo.component.ts
		  
		  @Component({
		    selector: 'app-userinfo',
		    standalone: true,
		    imports: [CommonModule],
		    template: `
		      <p>
		        userinfo works!
		      </p>
		    `,
		    styles: ``
		  })
		  export class UserinfoComponent {
		  
		  }
		  ```
		- ```ts 
		  //app.component.ts
		  
		  //import the component
		  import { UserinfoComponent } from './userinfo/userinfo.component'
		  
		  @Component({
		    selector: 'app-root',
		    standalone: true,
		    imports: [UserinfoComponent], //import the component
		    template: `
		  	<section class="content">
		          <article class="tile">
		            <app-userinfo/>  //use selector name from child component 
		          </article>
		      </section>
		    `,
		  })
		  export class AppComponent {
		    
		  }
		  ```
- ## Template
  collapsed:: true
	- ### Conditional Logic
		- #### @if
		  collapsed:: true
			- ```html
			  //app.component.html
			  <section class="membership-info">
			    	<p>{{ account.name }}</p>
			  	<p>Valid Thru: {{ account.validThru }}</p>
			  	<p>CVV: {{ account.CVV }}</p>
			  	<p>
			        @if (account.membershipStatus === "gold") {
			        <span class="badge gold">Gold</span>
			        } @else if (account.membershipStatus === "platinum") {
			        <span class="badge platinum">Platinum</span>
			        } @else {
			        <span class="badge silver">Silver</span>
			        }
			  	</p>
			  </section>
			  ```
			- ```ts
			  //app.component.ts
			  export class AppComponent {
			    account: AccountInfo = {
			      name: 'Melisa Evan',
			      membershipStatus: 'gold',
			      validThru: '12/2022',
			      CVV: '123',
			    };
			  }
			  ```
		- #### @switch
		  collapsed:: true
			- ```html
			  //app.component.html
			  
			  import { AccountInfo } from './account-info';
			  
			  <section class="membership-info">
			  	<p>
			        @switch (account.membershipStatus) {
			              @case ('gold') {
			                <span class="badge gold">Gold</span>
			              }
			              @case ('platinum') {
			                <span class="badge platinum">Platinum</span>
			              }
			              @default {
			                <span class="badge silver">Silver</span>
			              }
			            }
			  	</p>
			  </section>
			  ```
			- ```ts
			  //account-info.ts
			  
			  export interface AccountInfo {
			    name: string;
			    membershipStatus: 'silver' | 'gold' | 'platinum';
			    validThru: string;
			    CVV: string;
			  }
			  
			  ```
	- ### Loop
	  collapsed:: true
		- #### @for
			- ```html
			  <section class="container">
			        <!-- This article element represents and entire listing -->
			        @for (car of carList; track car) {
			          
			        <article class="listing">
			          <div class="image-parent">
			            <img class="product-image" src="https://placehold.co/100x100" />
			          </div>
			          <section class="details">
			  
			            <p class="title">{{car.make}} {{car.model}}</p>
			            <hr />
			            <p class="detail">
			              <span>Year</span>
			              <span>{{car.year}}</span>
			            </p>
			  
			          </section>
			        </article>
			  
			        } @empty {
			          <p>No listings available</p>
			        }
			  
			    </section>
			    
			  ```
	- ### Property binding
	  collapsed:: true
		- Property binding in Angular enables you to **set values for properties** of **elements in your templates**
		- #### @Input
		  collapsed:: true
			- Send information into a component (like props)
			- ```ts
			  //listing.component.ts
			  import { Component, Input } from '@angular/core';
			  import { CommonModule } from '@angular/common';
			  import { Car } from '../car';
			  
			  @Component({
			    selector: 'app-listing',
			    standalone: true,
			    imports: [CommonModule],
			    template: `
			        <article class="listing">
			          <div class="image-parent">
			            <img class="product-image" src="https://placehold.co/100x100" />
			          </div>
			          <section class="details">
			            <p class="title">{{car.make}} {{car.model}}</p>
			          </section>
			        </article>
			    `,
			    styles: ``,
			  })
			    
			  export class ListingComponent {
			    @Input({
			      required: true
			    }) car!: Car
			  }
			  ```
				- The `@Input` decorator is used to mark `car` as an input property, and `{ required: true }` ensures that it must be provided.
				- The `!` marks the property as definitely assigned to avoid TypeScript errors
			- ```ts
			  @Component({
			    selector: 'app-root',
			    standalone: true,
			    template: `
			      <h1>Saved Cars {{ savedCarList.length }}</h1>
			      <section class="container">
			        @for (car of carList; track car) {
			          <app-listing [car]="car"/>
			        }
			      </section>
			    `,
			    styles: [],
			    imports: [ListingComponent]
			  })
			  
			  export class AppComponent {
			    savedCarList: Car[] = [];
			    carList: Car[] = [
			      {
			        make: 'Foyoda',
			        model: 'Famery',
			      },
			      {
			        make: 'Ronda',
			        model: 'Disaccord',
			      },
			    ];
			  }
			  ```
				- `<app-listing [car]="car"/>`: the square brackets make the right-hand side be an expression an not a string
		- #### @Output
			- Send information from a child component to a parent via custom events
			- ```ts
			  //listing.component.ts
			  
			  @Component({
			    selector: 'app-listing',
			    standalone: true,
			    imports: [CommonModule],
			    template: `
			        <article class="listing">
			          <div class="image-parent">
			            <img class="product-image" src="https://placehold.co/100x100" />
			          </div>
			          <section class="details">
			            <p class="title">{{car.make}} {{car.model}}</p>
			            <hr />
			        </article>
			        
			        <button (click)="handleCarSaved()">Save Car</button>
			    `,
			    styles: ``,
			  })
			  export class ListingComponent {
			    @Output() carSaved = new EventEmitter<Car>()
			  
			    handleCarSaved() {
			      this.carSaved.emit(this.car)
			    }
			  
			  }
			  ```
				- **Template:**
					- Displays an article with an image and car details.
					- Has a button that triggers the `handleCarSaved` method on click.
				- **Class:**
					- `@Output() carSaved = new EventEmitter<Car>()`: Declares an output event emitter to notify parent components when a car is saved.
					- `handleCarSaved()`: Method that emits the current `car` object through the `carSaved` event when the Save Car button is clicked.
			- collapsed:: true
			  ```ts
			  import { Component, Input } from '@angular/core';
			  import { Car } from './car';
			  import { ListingComponent } from './listing/listing.component';
			  
			  @Component({
			    selector: 'app-root',
			    standalone: true,
			    template: `
			      <h1>Saved Cars {{ savedCarList.length }}</h1>
			      <section class="container">
			        @for (car of carList; track car) {
			          <app-listing [car]="car" (carSaved)="addCarToSaved($event)"/>
			        }
			      </section>
			    `,
			    imports: [ListingComponent]
			  })
			  export class AppComponent {
			    savedCarList: Car[] = [];
			     carList: Car[] = [
			      {
			        make: 'Foyoda',
			        model: 'Famery',
			      },
			      {
			        make: 'Ronda',
			        model: 'Disaccord',
			      }
			    ];
			  
			    addCarToSaved(car: Car) {
			      this.savedCarList.push(car)
			    }
			  }
			  
			  ```
				- **Template**:
					- `(carSaved)="addCarToSaved($event)"`: Sets up an event binding to call `addCarToSaved` when the `carSaved` event is emitted from `ListingComponent`.
				- **Class:**
					- `savedCarList: Car[] = [];`: Initializes an empty list to store saved cars.
					- `carList: Car[] = [{ make: 'Foyoda', model: 'Famery' }, { make: 'Ronda', model: 'Disaccord' }];`: Initializes a list of two cars.
					- `addCarToSaved(car: Car)`: Method that adds a car to the `savedCarList` when called.
- ## Navigation
  collapsed:: true
	- `route-outlet`
		- A `router-outlet` in Angular is a directive that acts as a placeholder within your application where the router will dynamically insert the component for the active route.
		- Essentially, it's where the routed component's template will be displayed.
	- ### Routing
		- `app.routes.ts`: Defines the routing configuration
			- ```ts
			  //app.routes.ts
			  
			  import { Routes } from '@angular/router';
			  import { GreetingsComponent } from './greetings.component';
			  
			  export const routes: Routes = [
			    {
			      path: "",
			      component: GreetingsComponent
			    },
			  ];
			  
			  ```
				- `path: ""`: The default route, also known as the root path.
				- `component: GreetingsComponent`: The component that will be displayed when the default path is accessed.
		- `app.config.ts`: Configures the application to use the router
		  collapsed:: true
			- ```ts
			  //app.config.ts
			  import { ApplicationConfig } from '@angular/core';
			  import { provideRouter } from '@angular/router';
			  import { routes } from './app.routes';
			  
			  export const appConfig: ApplicationConfig = {
			    providers: [
			      provideRouter(routes),
			    ],
			  };
			  
			  ```
				- Imports `provideRouter` from `@angular/router` which is used to configure the router with the defined routes.
				- `appConfig` is an `ApplicationConfig` object where router providers are listed.
		- `app.component.ts`
			- ```ts
			  //app.component.ts
			  import { Component } from '@angular/core';
			  import { CommonModule } from '@angular/common';
			  import { RouterModule } from '@angular/router';
			  
			  @Component({
			    selector: 'app-root',
			    standalone: true,
			    imports: [CommonModule, RouterModule],
			    template: `
			      <h1>Enable routing to see the greeting below</h1>
			      <router-outlet/>
			    `,
			    styles: [],
			  })
			  export class AppComponent {
			    title = '07-routing-basics';
			  }
			  
			  ```
				- `imports: [CommonModule, RouterModule]`: Imports necessary modules for common Angular directives and routing capabilities.
				- `<router-outlet/>`: A placeholder where the routed component (in this case, `GreetingsComponent` for the default path) will be displayed.
	- ### RouterLink
		- Create clickable links using the *router link directive*
		- A *route link* might be used instead of an `href` attribute when we want to navigate between routes without reloading the page
		- ```ts
		  //app.component.ts
		  @Component({
		    imports: [RouterOutlet, RouterLink],
		    template: `
		     
		     <a routerLink=''>home</a>
		     
		     <router-outlet/>
		    `,
		  })
		  
		  
		  //app.routes.ts
		  export const routes: Routes = [
		    {
		      path: '',
		      component: HomeComponent
		    }
		  ];
		  
		  ```
		- How to pass dynamic values to a route using placeholders and input binding
	- ### Dynamic Routes
		- `app.routes.ts`
			- ```ts
			  //app.routes.ts
			    
			  export const routes: Routes = [
			    {
			      path: 'details/:id'  
			        component: DetailsComponent
			    }
			  ]
			  
			  //It sets up a route that matches the URL path `details/:id`, where`:id` is a route parameter.
			  //When this path is matched, the`DetailsComponent` will be displayed.
			  ```
		- `app.config.ts`
		  collapsed:: true
			- ```ts
			  import { ApplicationConfig } from '@angular/core';
			  import { provideRouter, withComponentInputBinding } from '@angular/router';
			  
			  import { routes } from './app.routes';
			  
			  export const appConfig: ApplicationConfig = {
			    providers: [provideRouter(routes, withComponentInputBinding())]
			  };
			  ```
				- It sets up an `ApplicationConfig` object called `appConfig` which includes providers for the router.
				- Specifically, it uses `provideRouter` to supply the routing configuration, and `withComponentInputBinding` to enable input binding from the router.
		- `details.component.ts`
			- ```ts
			  import { Component, Input } from '@angular/core';
			  import { CommonModule } from '@angular/common';
			  
			  @Component({
			    selector: 'app-details',
			    standalone: true,
			    imports: [CommonModule],
			    template: `
			      <section>
			        <p>{{this.productList[productId].title}}</p>
			        <ul>
			          <li>{{this.productList[productId].price}}</li>
			          <li>{{this.productList[productId].description}}</li>
			        </ul>
			      </section>
			    `,
			    styles: ``,
			  })
			  export class DetailsComponent {
			    productId = 0;
			  
			    @Input() set id(value: number) {
			      this.productId = value;
			    }
			  
			    productList = [
			      {
			        title: 'Product 1',
			        price: 9234,
			        description: 'Product 1 is the best',
			      },
			      {
			        title: 'Product 2',
			        price: 3043,
			        description: 'Product 2 is special',
			      },
			      {
			        title: 'Product 3',
			        price: 4355,
			        description: 'Product 3 has my heart',
			      },
			    ];
			  }
			  	
			  ```
			- `productId`: An integer property initialized to 0.
			- `@Input() set id(value: number)`: A setter method to set `productId` from the input binding
		- `app.component.ts`
			- ```ts
			  import { Component } from '@angular/core';
			  import { RouterOutlet, RouterLink } from '@angular/router';
			  
			  @Component({
			    selector: 'app-root',
			    standalone: true,
			    imports: [RouterOutlet, RouterLink],
			    template: `
			     <h1>Welcome to {{ title }}!</h1>
			  
			     @for (title of productTitles; track title) {
			      <p>
			        <a [routerLink]="['details', $index]">{{title}}</a>
			      </p>
			     }
			     <router-outlet/>
			    `,
			  })
			  export class AppComponent {
			    title = '08-routing-recap';
			  
			    productTitles = ['Product 1', 'Product 2', 'Product 3'];
			  }
			  ```
	- ### Use URL Parameters & Query Parameters
		- Extra pieces of information about the page that are added to the URL
		- ==**Advantage of using query params over URL params:**== query paramsallow us to share the extract state of an application by copying and pasting the URL. This makes it convenient to send specific configurations or settings to someone else
		- #### URL (Route) Parameters
			- URL parameters *are used for important data that is part of the route pattern itself*
			- **Setting Up Route Parameters**
				- ```ts
				  //app-routing.module.ts
				  const routes: Routes = [
				    { path: 'user/:id', component: MyComponent }
				  ];
				  
				  ```
			- **Accessing Route Parameters**
				- // 
				  // To access these parameters in your component, use the ActivatedRoute 
				  // service
				  
				  import { Component, OnInit } from '@angular/core';
				  import { ActivatedRoute } from '@angular/router';
				  
				  @Component({
				    selector: 'app-my-component',
				    templateUrl: './my-component.component.html',
				    styleUrls: ['./my-component.component.css']
				  })
				  export class MyComponent implements OnInit {
				    userId: string;
				  
				    constructor(private route: ActivatedRoute) { }
				  
				    ngOnInit(): void {
				      this.userId = this.route.snapshot.paramMap.get('id') || "";
				    }
				  }
		- #### Query Parameters
			- Query parameters *are used for optional data that does not fit into the route pattern*
			- **Accessing Query Parameters**
			  collapsed:: true
				- ```ts
				  
				  export class MyComponent implements OnInit {
				    params: any[] = []
				  
				    constructor(private route: ActivatedRoute) { }
				  
				    ngOnInit(): void {
				    	this.route.queryParams.subscribe(params => this.params = Object.keys(params).map(key => ({ name: key, value: params[key] }))
				    }
				  }
				  ```
	- ### Create "Not Found" page
		- ```ts
		  //app-routing.ts
		  const routes: Routes = [
		    { path: "**", component: NotFoundPageComponent },
		  ];
		  ```
- ## Forms
	- **We have 2 ways to define forms and gather input from users**
	- ### Template Driven Forms (Uncontrolled Forms)
		- *We let the DOM handle all the form's functionality*
		- Quick to setup and use
		- Best for small one-time use forms
		- Requires more configuration for testing
		- ```ts
		  import { Component } from '@angular/core';
		  import { FormsModule } from '@angular/forms';
		  
		  @Component({
		    selector: 'app-root',
		    standalone: true,
		    imports: [FormsModule],
		    template: `
		      <article>
		        <h1>Blog Post</h1>
		        <section>
		          <label for="title">Post Title</label>
		          <input type="text" id="title" [(ngModel)]="title"/>
		  
		          <label for="body">Post Body</label>
		          <textarea id="body" [(ngModel)]="body"></textarea>
		  
		        </section>
		        <section>
		          <p>{{title}}</p>
		          <p>{{body}}</p>
		        </section>
		      </article>
		    `,
		  })
		  export class AppComponent {
		    title = '';
		    body = '';
		  
		  }
		  
		  ```
			- **Bound Variables and Two-way Data Binding**:
			- **title = ''; body = '';**
				- These are the variables that store the title and body of the blog post. They are initially set to empty strings.
				- They are bound to the `input` and `textarea` elements using `[(ngModel)]`, which is Angular’s two-way data binding syntax. This means any changes in the input fields will be reflected in the `title` and `body` variables, and changes in the variables will update the input fields.
			- Angular’s **`ngModel`** directive updates the `title` and `body` properties with the new values.
	- ### Reactive Forms (Controlled Forms)
		- *The state of our form is explicitly tracked*
		- Supports typing
		- Reuseable, can share models
		- More robust testing configuration
		- collapsed:: true
		  ```ts
		  import { Component } from '@angular/core';
		  import { FormControl, FormGroup, ReactiveFormsModule } from '@angular/forms';
		  
		  @Component({
		    selector: 'app-root',
		    standalone: true,
		    //This imports ReactiveFormsModule to enable the use of reactive forms.
		    imports: [ReactiveFormsModule],
		    template: `
		      <article>
		        <h1>Blog Post</h1>
		        <form name="blogForm" [formGroup]="blogForm" (ngSubmit)="handleFormSubmit()">
		          <section>
		            <label for="title">Post Title</label>
		            <input type="text" id="title" formControlName="title"/>
		  
		            <label for="body">Post Body</label>
		            <textarea name="" id="body" cols="30" rows="10" formControlName="body"></textarea>
		          </section>
		          <button type="submit">Submit Post</button>
		        </form>
		      </article>
		    `,
		    styles: [],
		  })
		  export class AppComponent {
		    blogForm = new FormGroup({
		      title: new FormControl(''),
		      body: new FormControl(''),
		    })
		  
		    handleFormSubmit() {
		      this.postBlog(this.blogForm.value.title, this.blogForm.value.body)
		  
		    }
		  
		    postBlog(title: string | null | undefined, body: string | null | undefined) {
		      console.log(`Posting blog titles ${title}, with the contents ${body}.`);
		    }
		  }
		  
		  ```
			- **Reactive Form Definition: `FormGroup` and `FormControl`**
			  collapsed:: true
				- `blogForm` is an instance of `FormGroup`, which aggregates multiple form controls into a single object, allowing management of the entire form.
				- The `FormGroup` is initialized with two form controls: `title` and `body`, both set to empty strings. `FormControl` objects track the value and the validation status of each individual form field.
			- **`handleFormSubmit` Method**
			  collapsed:: true
				- This method is called when the form is submitted (triggered by `(ngSubmit)="handleFormSubmit()"` in the template).
			- It calls the `postBlog` method, passing in the current values of the `title` and `body` form controls.
			- **`postBlog` Method**
			  collapsed:: true
				- This method takes two arguments (title and body), logs a message to 
				  the console with these values, simulating a blog post submission
			- **Form Template**
			  collapsed:: true
				- The `<form>` element:
					- The form element uses the `formGroup` directive to bind the `blogForm` FormGroup.
					- It also uses the `(ngSubmit)` directive to bind the form's submit event to the `handleFormSubmit` method.
				- Input fields and textarea:
					- The `<input>` and `<textarea>` elements bind to `FormControl` instances using the `formControlName` directive.
				- Submit button:
					- The `<button>` element, with `type="submit"`, triggers the form submission when clicked.
		- #### Validation
			-
- ## Event Handling
	- ### `EventEmitter`
		- Is used to *create custom events in components and services*
		- *Provides a way for components to communicate with each other*
		- ```ts
		  import { Component, EventEmitter, Output } from '@angular/core';
		  
		  @Component({
		    selector: 'app-multiple-choice',
		    templateUrl: './multiple-choice.component.html',
		    styleUrl: './multiple-choice.component.css'
		  })
		  export class MultipleChoiceComponent {
		    @Output() a = new EventEmitter<void>();
		    @Output() b = new EventEmitter<void>();
		    @Output() c = new EventEmitter<void>();
		    @Output() d = new EventEmitter<void>();
		  
		    aClicked(): void {
		      this.a.emit()
		    }
		  
		    bClicked(): void {
		      this.b.emit()
		    }
		  
		    cClicked(): void {
		      this.c.emit()
		    }
		  
		    dClicked(): void {
		      this.d.emit()
		    }
		  }
		  
		  ```
		- ```ts
		  <h2 class="title">Outputs</h2>
		  
		  <div>
		    <button (click)="aClicked()">A</button>
		    <button (click)="bClicked()">B</button>
		    <button (click)="cClicked()">C</button>
		    <button (click)="dClicked()">D</button>
		  </div>
		  
		  
		  ```
-
- ## Signals
  collapsed:: true
	- Signals are a new way of handling change detection and reactivity in Angular application
	- ### signal
		- A value that can tell ANgular when it changes
		- capable of notifying its context of future changes in its value
	- ### computed
		- Derive new value when one of the dependent signals change
	- ### effect
		- An effect is a side-effectful operation which reads the value of zero or more signals
- ## Deferrable Views
  collapsed:: true
	- https://v17.angular.io/guide/defer
	- Allow for lazy loading of components and templates, which can help reduce the initial bundle size and improve performance
	- Refer to delaying the creation or update of some parts of your view until they are actually needed. This can help improve performance by not doing unnecessary work upfront.
	- ```
	  @defer {
	    <large-component />
	  }
	  
	  //The content of the main @defer block is the section of content that is 
	  lazily loaded. It will not be rendered initially, and all of the content 
	  will appear once the specified trigger or when condition is met and the 
	  dependencies have been fetched. 
	  By default, a @defer block is triggered when the browser state becomes idle.
	  ```
	- ### `on idle`
		- Load or perform an action when the browser is idle.
		- **Use Case**: Suitable for non-essential tasks that can be done when there's no other high-priority work. For example, preloading sections of an app in the background.
	- ### `on immediate`
		- Load or perform an action immediately without any delay.
		- **Use Case**: Useful for content that needs to be available as soon as possible, like critical UI components.
	- ### `on timer(...)`
		- Load or perform an action after a specified time delay.
		- **Use Case**: Useful for delaying tasks to improve perceived performance or to stagger resource loads.
	- ### `on viewport(...)`
		- Load or perform an action when a specific element comes into the viewport (is visible on the screen).
		- **Use Case**: Perfect for lazy-loading images or sections of a page to save bandwidth and improve load times.
	- ### `on interaction(...)`
		- Load or perform an action when the user interacts with a specific part of the UI (like clicking a button).
		- **Use Case**: Efficient for tasks triggered by user actions, ensuring that resources are only loaded when necessary.
	- ### `on hover(...)`
		- Load or perform an action when the user hovers over an element.
		- **Use Case**: Great for preloading content or showing tooltips and previews to improve the user experience.
		- ```html
		   @defer (on hover(loadPosts)) {
		          <app-posts />
		        }
		  ```
	- ### Summary
		- These strategies help manage resource loading and user experience effectively:
		- **`on idle`**: Non-essential tasks performed in the background.
		- **`on immediate`**: High-priority tasks executed instantly.
		- **`on timer(...)`**: Tasks delayed by a specified time.
		- **`on viewport(...)`**: Content loaded when visible on the screen.
		- **`on interaction(...)`**: Content loaded upon specific user actions.
		- **`on hover(...)`**: Content loaded on mouse hover for quick previews.
	-
- ## View encapsulation
  collapsed:: true
	- Is a way to control how styles defined in a component affect the component itself and other parts of the application
	- **Emulated (default)**:
		- Styles defined in this component are scoped to this component and do not affect other components
		- Angular adds unique attributes to elements in the component's template and styles so that they only apply to that component
	- **ShadowDom**:
		- Uses the native shadow DOM to encapsulate styles
		- Styles are completely isolated from the rest of the application, providing true style encapsulation
	- **None**:
		- No encapsulation is applied
		- Styles defined in the component are applied globally and can affect styles in other parts of the application
	- **Example**
		- ```ts
		  import { Component, ViewEncapsulation } from '@angular/core';
		  
		  @Component({
		    selector: 'app-my-component',
		    templateUrl: './my-component.component.html',
		    styleUrls: ['./my-component.component.css'],
		    encapsulation: ViewEncapsulation.Emulated
		  })
		  export class MyComponent {
		    // Component logic here
		  }
		  
		  ```
-
- ## Fetching Data
  collapsed:: true
	- [Fetching data in Angular: HttpClient or Fetch API? | by Saeid | Medium](https://medium.com/@saeid_38500/my-test-post-3e533db437f7/)
	- **Angular services:** handle data loading and server communication in Angular applications
	- **Observable**: a design pattern used for event handling
	- ### Fetch data with HTTPClient
	  collapsed:: true
		- ```ts
		  //user.service.ts
		  import { HttpClient } from '@angular/common/http';
		  import { Injectable } from '@angular/core';
		  import { Observable } from 'rxjs';
		  
		  @Injectable({
		    providedIn: 'root'
		  })
		  export class UserInfoService {
		  
		    constructor(private http: HttpClient) { }
		  
		    loadData(): Observable<any> {
		      return this.http.get<any>("https://randomuser.me/api/")
		    }
		  }
		  ```
		- ```ts
		  import { Component, OnInit } from '@angular/core';
		  import { UserInfoService } from '../user-info.service';
		  
		  @Component({
		    selector: 'app-user-info-display',
		    templateUrl: './user-info-display.component.html',
		    styleUrl: './user-info-display.component.css'
		  })
		  export class UserInfoDisplayComponent implements OnInit {
		    info: any = {}
		  
		    constructor(private userInfo: UserInfoService) { }
		  
		    ngOnInit(): void {
		      this.userInfo.loadData().subscribe(data => this.info = data.results[0])
		  
		    }
		  
		  }
		  ```
	- ### Fetch data with `fetch`
	  collapsed:: true
		- ```ts
		  //data.service.ts
		  import { Injectable } from '@angular/core';
		  
		  interface User {
		    firstname: string;
		    lastname: string;
		    birthday: string;
		    id: string;
		  }
		  
		  @Injectable({
		    providedIn: 'root'
		  })
		  export class DataService {
		    private apiUrl = 'https://6561036783aba11d99d1cff0.mockapi.io/api/test';
		  
		    getData(): Promise<User> {
		        const users = fetch(this.apiUrl).then(res => res.json());
		        return users;
		    }
		  }
		  ```
		- ```ts
		  export class MyComponent {
		    constructor(private dataService: DataService) {}
		  
		    logData() {
		      this.dataService.getData().then(data => console.log(data));
		    }
		  }
		  ```
- ## Dependency Injection (DI)
  collapsed:: true
	- DI is a design pattern and mechanism for **creating and delivering** some parts of an app to other **parts of an app that require them**
	- `user.service.ts`
	  collapsed:: true
		- ```ts
		  
		  import { Injectable } from '@angular/core';
		  import { data, User } from './data';
		  
		  @Injectable({
		    providedIn: 'root'
		  })
		  export class UserService {
		    private userData: User[] = data;
		  
		    constructor() { }
		  
		    getUserData(): Promise<User[]> {
		      return new Promise((resolve) => {
		        resolve(this.userData);
		      });
		    }
		  }
		  ```
			- **Decorator - `@Injectable`:**
				- The `Injectable` decorator indicates that this class can be injected as a dependency within other classes.
				- `{ providedIn: 'root' }` specifies that this service 
				  should be provided at the root level, meaning that the service is a 
				  singleton and available globally across the application.
			- **Class - `UserService`:**
				- This class, `UserService`, is intended to manage user-related data and operations.
				- A private property `userData` of type `User[]` is initialized with the value of `data`, which is imported.
			- **Method - `getUserData`:**
				- This method returns a `Promise` that resolves to an array of `User` objects.
				- It wraps the `userData` in a Promise and resolves it immediately.
	- `app.component.ts`
	  collapsed:: true
		- ```ts
		  @Component({
		    selector: 'app-root',
		    standalone: true,
		    imports: [UserInfoComponent],
		    template: `
		    <h1>User Listing</h1>
		    @for(user of userData; track user.id) {
		      <app-user-info [user]="user" />
		    }
		    `,
		  })
		  export class AppComponent implements OnInit {
		    userService = inject(UserService)
		    userData: User[] = []
		  
		    async ngOnInit(): Promise<void> {
		      const data = await this.userService.getUserData()
		      this.userData = data
		    }
		  
		  }
		  
		  ```
			- **Class - `AppComponent`:**
				- The class is named `AppComponent` and it implements the `OnInit` lifecycle hook from Angular.
			- **Properties:**
				- `userService`: This uses the `inject` utility function to inject the `UserService`. This is a new way introduced in Angular 14 (with standalone components support) for dependency injection.
				- `userData`: This is an array of `User` objects that starts as an empty array.
			- **Methods - `ngOnInit`:**
				- This method is called once the component is initialized.
				- It's defined as `async`, so it can use `await` to handle the `Promise` from `getUserData`.
				- It awaits the result of `getUserData` and assigns it to `userData`, updating the component's state with the user data fetched from the service.
-
- ## Lifecycle events
  collapsed:: true
	- https://v17.angular.io/guide/lifecycle-hooks
	- ### ngOnInit
		- **OnInit**
			- `OnInit` is an interface in Angular, part of the Angular core library (`@angular/core`). It provides a lifecycle hook method called `ngOnInit` that is called by Angular *to indicate that Angular is done creating the component or directive*
		- **When to Use**
			- Initialization logic like fetching data from a server.
			- Setup any additional logic that depends on the input properties.
		- **Example Use Case**
			- Suppose you have a component that needs to fetch user data when it is initialized. Here’s how you might use `ngOnInit`:
			- ```typescript
			  import { Component, OnInit } from '@angular/core';
			  import { UserService, User } from './user.service';
			  
			  @Component({
			  selector: 'app-user-list',
			  template: `
			    <h1>User List</h1>
			    <ul>
			      <li *ngFor="let user of users">
			        {{ user.name }}
			      </li>
			    </ul>
			  `
			  })
			  export class UserListComponent implements OnInit {
			  users: User[] = [];
			  
			  constructor(private userService: UserService) { }
			  
			  async ngOnInit(): Promise<void> {
			    this.users = await this.userService.getUserData();
			  }
			  }
			  ```
	- ### ngOnDestroy
		- `ngOnDestroy` is a lifecycle hook called by Angular just before destroying the directive/component
		- **When to Use**
			- Cleanup logic like unsubscribing from Observables or detaching event handlers to avoid memory leaks.
		- **Example**
			- ```ts
			  import { Component, OnDestroy } from '@angular/core';
			  
			  @Component({
			    selector: 'app-example',
			    templateUrl: './example.component.html',
			    styleUrls: ['./example.component.css']
			  })
			  export class ExampleComponent implements OnDestroy {
			  
			    constructor() { }
			  
			    ngOnDestroy(): void {
			      // Cleanup logic
			      console.log('ngOnDestroy called!');
			    }
			  
			  }
			  
			  ```
- ## Directives
  collapsed:: true
	- [Angular Directives: A Comprehensive Guide | Medium](https://medium.com/@ayushgrwl365/angular-directives-enhancing-user-interfaces-with-ease-bb99d74e69cd)
	- Directives are a way to extend HTML by attaching custom behaviours to DOM elements or creating new HTML elements. They are a crucial part of Angular’s declarative approach to building user interfaces. With directives, you can manipulate the DOM, apply CSS styles, handle user input, and much more.
	- ### `ng-for`
		- Used to iterate over a collection of data and generate dynamic HTML elements for each item in the collection.
		- ```ts
		  items = ['Apple', 'Banana', 'Orange'];
		  
		  <ul>
		    <li *ngFor="let item of items">{{ item }}</li>
		  </ul>
		  
		  ```
	- ### `ng-if`
	  :LOGBOOK:
	  CLOCK: [2024-06-15 Sat 18:00:24]--[2024-06-15 Sat 18:00:25] =>  00:00:01
	  CLOCK: [2024-06-15 Sat 18:00:27]--[2024-06-15 Sat 18:00:28] =>  00:00:01
	  CLOCK: [2024-06-15 Sat 18:00:30]
	  :END:
		- Used to conditionally render or remove an element from the DOM based on an expression or a boolean value.
		- ```ts
		  <div *ngIf="condition">
		    Content to render when condition is true.
		  </div>
		  ```
	- ### `ng-switch`
		- Used to conditionally display elements based on the evaluated value of an expression. It's similar to using a switch-case statement in traditional programming languages
		- `ngSwitch` works in conjunction with `ngSwitchCase` and `ngSwitchDefault` directives to render different blocks of content based on matching conditions
		- ```ts
		  <div [ngSwitch]="expression">
		    <div *ngSwitchCase="value1">Content for value1</div>
		    <div *ngSwitchCase="value2">Content for value2</div>
		    <div *ngSwitchDefault>Default content when no match</div>
		  </div>
		  ```
	- ### `ng-content`
		- It enables  the insertion of content inside component tags