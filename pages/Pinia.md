tags:: [[Vue.js]]

- https://pinia.vuejs.org/introduction.html
- The intuitive store for Vue.js
- Die Pinia Library ist eine State Management Library für Vue.js-Anwendungen. Sie ist inspiriert von Vuex, aber mit einem Fokus auf TypeScript-Unterstützung, verbesserte Typensicherheit und eine 
  modernere API.
- Pinia bietet eine einfachere Art, den Anwendungszustand zu verwalten, und macht es einfacher, gut strukturierte Anwendungen zu erstellen.
- ## Getting Started
	- https://pinia.vuejs.org/getting-started.html
	- ## Installation
		- `npm install pinia`
		- `yarn add pinia`
		- `bun add pinia`
	- ## Create pinia instance (root store) `main.ts`
		- ```jsx
		  import { createApp } from 'vue'
		  import { createPinia } from 'pinia'
		  import App from './App.vue'
		  
		  const pinia = createPinia()
		  const app = createApp(App)
		  
		  app.use(pinia)
		  app.mount('#app'
		  ```
- ## Defining a Store
	- https://pinia.vuejs.org/core-concepts/
	- ### Option Stores
		- ```jsx
		  export const useCounterStore = defineStore('counter', {
		    state: () => ({ count: 0, name: 'Eduardo' }),
		    getters: {
		      doubleCount: (state) => state.count * 2,
		    },
		    actions: {
		      increment() {
		        this.count++
		      },
		    },
		  })
		  ```
	- ### Setup Store
		- ```jsx
		  export const useCounterStore = defineStore('counter', () => {
		    const count = ref(0)
		    const name = ref('Eduardo')
		    const doubleCount = computed(() => count.value * 2)
		    function increment() {
		      count.value++
		    }
		  
		    return { count, name, doubleCount, increment }
		  })
		  ```
		- `ref()`s become `state` properties
		- `computed()`s become `getters`
		- `function()`s become `actions`