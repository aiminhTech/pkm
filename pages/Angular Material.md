tags:: [[Angular]]

- https://material.angular.io/
- ## Installation
	- https://material.angular.io/guide/getting-started
	- ```bash
	  ng add @angular/material
	  ```
- ## Display a component
	- You need to import the `MatSlideToggleModule` that you want to display by adding the following lines to your `app.module.ts` file.
	- ```ts
	  import { MatSlideToggleModule } from '@angular/material/slide-toggle';
	  
	  @NgModule ({
	    imports: [
	      MatSlideToggleModule,
	    ]
	  })
	  class AppModule {}
	  ```
	- Add the `<mat-slide-toggle>` tag to the `app.component.html` like so:
	- ```
	  <mat-slide-toggle>Toggle me!</mat-slide-toggle>
	  ```