tags:: [[JSX]], [[Javascript]]

- https://vuejs.org/guide/introduction.html
- A JavaScript framework for building user interfaces.
- It builds on top of standard HTML, CSS, and JavaScript and provides a declarative and 
  component-based programming model that helps you efficiently develop user interfaces, be they simple or complex.
- ## Learn Links
	- [https://jj09.net/vue-for-react-developers/](https://jj09.net/vue-for-react-developers/)
	- [https://prismic.io/blog/compare-react-vs-vue](https://prismic.io/blog/compare-react-vs-vue)
	- [https://blog.logrocket.com/vue-3-react-developers-side-by-side-comparison-demos/#rendering-lists-items-v-for](https://blog.logrocket.com/vue-3-react-developers-side-by-side-comparison-demos/#rendering-lists-items-v-for)
- ## Quick Start
	- https://vuejs.org/guide/quick-start.html
	- `npm create vue@latest`
	- Once the project is created, follow the instructions to install dependencies and start the dev server:
		- ```
		  > cd <your-project-name>
		  > npm install
		  > npm run dev> 
		  ```
- ## `<script setup>`
	- https://vuejs.org/api/sfc-script-setup.html
	- ```vue
	  <script setup>
	  console.log('hello script setup')
	  </script>
	  ```
	- The code inside is compiled as the content of the component's `setup()` function.
	- This means that unlike normal `<script>`, which only executes once when the component is first imported, code inside `<script setup>` will **execute every time an instance of the component is created**.
- ## Syntax
	- ### directly in html
	  collapsed:: true
		- ```vue
		  <!DOCTYPE html>
		  <html>
		  <head>
		    <title>My Application</title>
		    <script src="path/to/script"></script>
		  </head>
		    
		  <body>
		    <div id="app">
		      <h1>{{ greeting }}</h1>
		      <button @click="changeGreeting">Click me!</button>
		    </div>
		  
		    <script>
		      // Create Vue instance
		      new Vue({
		        el: '#app',
		        data: {
		          greeting: 'Hello World!'
		        },
		        methods: {
		          changeGreeting: function() {
		            this.greeting = 'Hello Vue.js!';
		          }
		        }
		      });
		    </script>
		  </body>
		    
		  </html>
		  
		  ```
	- ### SFC (Single File Components)
	  collapsed:: true
		- SFC allows you to define your templates, JavaScript logic, and styling in a single file with a `.vue` extension.
		- This is often referred to as the "Vue Single-File Component" syntax.
		- ```vue
		  <template>
		    <div>
		      <h1>{{ greeting }}</h1>
		      <button @click="changeGreeting">Click me!</button>
		    </div>
		  </template>
		  
		  <script>
		  export default {
		    data() {
		      return {
		        greeting: 'Hello World!'
		      }
		    },
		    methods: {
		      changeGreeting() {
		        this.greeting = 'Hello Vue.js!'
		      }
		    }
		  }
		  </script>
		  
		  <style>
		  h1 {
		    color: blue;
		  }
		  button {
		    background-color: orange;
		    color: white;
		  }
		  </style>
		  
		  ```
		- **Template**:
			- The `<template>` section is where you define the HTML structure and layout of the component.
			- It contains the markup and elements that make up the visual part of the component.
		- **Script**:
			- The `<script>` section contains the JavaScript code and options for the component.
			- This is where you define the data, methods, computed properties, lifecycle hooks, and other configurations for the component.
		- **Style**:
			- The `<style>` section is used to define the component's styling rules
		-
- ## Built-in Directives
	- https://vuejs.org/api/built-in-directives.html
	- ### v-bind
	  collapsed:: true
		- used to bind values dynamically to**HTML attributes** , **component props**, or **other directives**.
		- dynamically set the value of an attribute or prop based on the data in your Vue instance.
		- ### binding HTML attributes:
			- ```html
			  <button v-bind:class="btnClass">Click Me</button>
			  ```
			- the `class` attribute of the `button` element is bound to the value of the `btnClass` variable.
			- Any changes to `btnClass` in the Vue instance will automatically update the class of the button.
		- ### binding component props
			- ```html
			  <my-component v-bind:prop-name="value"></my-component>
			  ```$
			- the prop called `prop-name` in the `my-component` Vue component is bound to the value of the `value` variable.
			- This allows passing dynamic data from the parent component to the child component.
		- ### binding dynamic inline styles
			- ```html
			  <div v-bind:style="{ color: textColor, fontSize: fontSize + 'px' }">Dynamic Style</div>
			  ```
			- In this example, the `style` attribute of the `div` element is bound to an object.
			- The values of `textColor` and `fontSize` are dynamically set, allowing you to apply dynamic inline styles.
	- ### conditional rendering
	  collapsed:: true
		- use to directives to conditionally render content in your templates
		- ### v-if
			- ```vue
			  <template>
			  	<div v-if="condition">
			    		This element is rendered when the condition is true.
			  	</div>
			  </template>
			  ```
		- ### v-else
			- Does not expect expression
			- ```vue
			  
			  <template>
			  	<div v-if="condition1">
			    		This element is rendered when condition1 is true.
			  	</div>
			  	<div v-else>
			    		This element is rendered when condition1 is false.
			  	</div>
			  </template>
			  ```
		- ### v-else-if
			- ```vue
			  <template>
			  	<div v-if="type === 'A'"> A </div>
			  	<div v-else-if="type === 'B'"> B </div>
			  	<div v-else-if="type === 'C' "> C </div>
			  	<div v-else> Not A/B/C </div>
			  </template>
			  
			  ```
- ## Event Handling
	- https://vuejs.org/guide/essentials/event-handling.html
	- ### Inline event handling
		- You can directly bind an event to an element using the `v-on` directive followed by the event name.
		- Use the `@` symbol as a shorthand for `v-on`. For example, to handle a button click event:
		- ```htmlmixed
		  <button @click="handleClick">Click me</button>
		  ```
	- ### Method event handling
		- define methods in the `methods` section of your component and then bind them to events using `v-on` or `@`
		- ```html
		  <button v-on:click="handleClick">Click me</button>
		  ```
		- ```javascript
		  methods: {
		    handleClick() {
		      console.log("Cliked")
		    }
		  }
		  
		  ```
- ## API Styles
	- Vue components can be authored in two different API styles: **Options API** and **Composition API**.
	- ### Options API
		- With Options API, we define a component's logic using an object of options such as `data`, `methods`, and `mounted`.
		- Properties defined by options are exposed on `this` inside functions, which points to the component instance:
			- ```vue
			  <script>
			  export default {
			    // Properties returned from data() become reactive state
			    // and will be exposed on `this`.
			    data() {
			      return {
			        count: 0
			      }
			    },
			  
			    // Methods are functions that mutate state and trigger updates.
			    // They can be bound as event handlers in templates.
			    methods: {
			      increment() {
			        this.count++
			      }
			    },
			  
			    // Lifecycle hooks are called at different stages
			    // of a component's lifecycle.
			    // This function will be called when the component is mounted.
			    mounted() {
			      console.log(`The initial count is ${this.count}.`)
			    }
			  }
			  </script>
			  
			  <template>
			    <button @click="increment">Count is: {{ count }}</button>
			  </template>
			  ```
	- ### Composition API
		- With Composition API, we define a component's logic **using imported API functions** . In SFCs, Composition API is typically used with [`<script setup>`](https://vuejs.org/api/sfc-script-setup.html).
		- The `setup` attribute is a hint that makes Vue perform compile-time transforms that allow us to use Composition API with less boilerplate.
		- For example, imports and top-level variables / functions declared in `<script setup>` are directly usable in the template.
		- ```vue
		  <script setup>
		  import { ref, onMounted } from 'vue'
		  
		  // reactive state
		  const count = ref(0)
		  
		  // functions that mutate state and trigger updates
		  function increment() {
		    count.value++
		  }
		  
		  // lifecycle hooks
		  onMounted(() => {
		    console.log(`The initial count is ${count.value}.`)
		  })
		  </script>
		  
		  <template>
		    <button @click="increment">Count is: {{ count }}</button>
		  </template>
		  ```
-