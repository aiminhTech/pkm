parent:: [[CSS]]
link:: https://tailwindcss.com/

- An **utility-first CSS Framwork** that uses samll, single-purpose classes to style elements
  background-color:: blue
- It makes prototyping faster and helps avoid common CSS problems like cascade issues
- **How does it work?**
	- Scans project files as plain text, which means no code parsing
	- Looks for tokens that match class names
	- Generate CSS for recognized utilities
-
- ## 📔 Learning
  collapsed:: true
	- https://frontendmasters.com/courses/tailwind-css-v2/
		- https://github.com/stevekinney/tailwind-skatepark
-
- ## Useful Resources
  collapsed:: true
	- [Tailwind Prettier Plugin](https://tailwindcss.com/blog/automatic-class-sorting-with-prettier)
	- [Tailwind CSS IntelliSense](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss)
	- [UI Colors](https://uicolors.app/)
	- [designrift](https://designrift.vercel.app/)
- ## Best Pratices
  collapsed:: true
	- ### Using CSS Layers
		- `@import "tailwindcss";` injects the four layers in that order. Write custom code where it belongs
			- `@layer theme`: Design token variables
			- `@layer base`: Element resets and typography
			- `@layer components`: Reusable overridable pattern
			- `@utility`: One-off helpers that behave like core utilities
		- This mean we dont have to worry about where TW goes. Just add custom code in the appropriate layer and TW handles the order internally
	- ### Theme Layer & CSS variables
		- The **theme layer** defines design tokens like colors, spacing and fonts in `tailwind.config.ts`
		- TW uses CSS variables internally, so update a color or spacing in the theme, it automatically updates all utilities that use it
		- **Example**
			- ```js
			  theme: {
			    colors: {
			      primary: '#1DA1F2',
			      secondary: '#14171A',
			    },
			  }
			  ```
			- `bg-primary` or `text-secondary` can be used in HTML, and TW applies the correct color
	- ### Responsive, state and container variants
		- Mobile-first: default rule, then `md:`, `lg:` prefixes
		- Combine state and media: `md:hover:bg-primary-600`
- ## Anti-Patterns
  collapsed:: true
	- Avoid creating lots of custom CSS classes fot hings TW already provides
	- Avoid using arbitrary values (`bg-[#123456]` or `p-[17px]`) unless necessary. This make code harder to maintain
-
- ## Basics
  collapsed:: true
	- ### Button
		- https://stevekinney.com/courses/tailwind/building-a-button
	- ### Border, Outline and Ring
		- https://stevekinney.com/courses/tailwind/border-outline-ring
		- **Borders**
		  background-color:: yellow
			- Surround the element and affect layout/size
			- Adding a border can push or shift nearby elements, which may cause layout issues
			- **Use it when:**
				- Need actual structural borders (like table cells or card edges)
				- The border is part of the design, not just an interaction state
				- Ok with the element taking up more space
		- **Outlines**
		  background-color:: yellow
			- Drawn outside the element **without affecting layout**
			- Ideal for **focus states** on buttons, inputs and links
			- ```html
			  <button class="focus:outline focus:outline-2 focus:outline-blue-500">Click Me</button>
			  ```
			- **Use it when:**
				- Need quick debugging (slap `outline` on verything to see layouts)
				- Building focus states for non-`rounded-md` elements
				- Want something that definitely wont affect layout
		- **Rings**
		  background-color:: yellow
			- TW implements rings as **special box shadows** around elements
			- Mostly a visual effect. They dont change layout but are less semantically standard than outlines
			- **Use it when:** Need to stack multiple visual effects
	- ### Card
		- https://stevekinney.com/courses/tailwind/building-a-card
		- ```html
		  <div class="border p-4 rounded-md shadow-md bg-slate-50 border-slate-300">
		    <h2 class="font-semibold text-lg">Card title</h2>
		    <p class="mt-1.5 text-sm">Description</p>
		  </div>
		  ```
	- ### Spacing and Dividing Utilities
		- https://stevekinney.com/courses/tailwind/spacing-and-dividing-utilities
- ## Form Styling
	- https://stevekinney.com/courses/tailwind/building-a-form-input
	- ### Basic Form
	  collapsed:: true
		- https://stevekinney.com/courses/tailwind/focus-states
		- ```html
		  <div class="space-y-1">
		    <label class="block font-semibold text-slate-900" for={id}>Name</label>
		    <input
		      class="w-full block outline outline-slate-600 rounded px-2 py-1 focus:outline-2 focus:outline-blue-500 placeholder:italic"
		     	{id}
		      aria-describedby={descriptionId}
		      aria-invalid={!!error}
		      aria-errormessage={errorId}
		      {...props}
		    />
		  </div>
		  ```
	- ### Focus States
	  collapsed:: true
		- https://stevekinney.com/courses/tailwind/focus-states
		- `:focus`
			- Triggered on any focus (via keyboard, mouse)
			- Works for all focusable elements (inputs, buttons, links)
			- ```html
			  <button class="focus:outline-none focus:ring-2 focus:ring-blue-500">Click me</button>
			  ```
		- `:focus-visible`
			- Only keyboard focus
			- Avoid showing focus on mouse click
			- ```html
			  <button class="focus-visible:ring-2 focus-visible:ring-green-500">Click me</button>
			  ```
		- `:focus-within`
			- When any child inside is focused
			- Highlight a container of form group
			- ```html
			  <div class="border rounded bg-slate-200 p-4 outline-sky-400 focus-within:bg-sky-200">
			    <input class="accent-purple-400" {id} {...props} type="checkbox" />
			    <label for={id}>{label}</label>
			  </div>
			  ```
		-
- ## Utility-First Styling
  collapsed:: true
	- ### Parent State Styling
		- https://stevekinney.com/courses/tailwind/group-and-peer-modifiers
		- **`group`** (parent -> children)
			- Add `group` to a **parent element**, then use `group-hover:`, `group-focus:` or `group-focus-within:` on **child elements** to style them when the parent is ineracted with
			- ```html
			  <div class="group border p-4 rounded-md hover:border-blue-500 transition">
			    <h2 class="text-gray-700 group-hover:text-blue-500">Hover over me</h2>
			    <p class="text-gray-500 group-hover:text-blue-300">I change color too!</p>
			  </div>
			  ```
		- **`peer`** (sibling -> elements)
			- Add `peer` to an **input or element**, then use `peer-checked:`, `peer-focus:`, etc. on **sibling elements** to style them based on the peer's state
			- ```html
			  <div class="border rounded bg-slate-200 p-4 outline-sky-400 focus-within:bg-sky-100">
			    <input class="peer accent-green-400" {id} {...props} type="checkbox" />
			    <label class="peer-checked:line-through" for={id}>{label}</label>
			  </div>
			  ```
	- ### Has Utility Class - `:has()`
		- https://tailwindcss.com/docs/hover-focus-and-other-states#has
		- https://stevekinney.com/courses/tailwind/has-utility
		- Allows a **parent element to change style based on its children**. Works like a parent query, so ywe can stlye containers dynamically
		- ```html
		  <div class="flex items-center gap-3 rounded-lg border p-4 has-[input:checked]:border-green-500 has-[input:checked]:bg-green-50">
		    <input type="checkbox" id="terms" class="h-4 w-4" />
		    <label for="terms" class="text-slate-900">I agree to the terms</label>
		  </div>
		  
		  // has-[input:checked]:border-green-500 → changes the border color of the container if the checkbox is checked
		  // has-[input:checked]:bg-green-50 → changes the background color of the container when checked
		  
		  // Initially, the container has a gray border and white background
		  // When the checkbox is checked, the parent container’s border turns green and the background becomes a light green
		  ```
		- #### Key Differences
			- **`has-*`** - Styles the element containing the target
			- **`group-has-*`** - Styles descendant when ancestor contains target
			- **`peer-has-*`** - Styles sibling when previous sibling contains target
- ## Container Queries
	- https://tailwindcss.com/docs/responsive-design#container-queries
	- https://stevekinney.com/courses/tailwind/container-queries
	- Are a modern CSS feature that let you style something based on the size of a parent element instead of the size of the entire viewport
	- ```html
	  <div class="@container">
	    <div class="flex flex-col @md:flex-row">
	      <!-- ... -->
	    </div>
	  </div>
	  ```
-
-
- ## Dark Mode
	- https://stevekinney.com/courses/tailwind/dark-mode
	- ### Custom Variant in `index.css`
		- ```css
		  /* index.css */
		  /* add dark mode variant */
		  @custom-variant dark (&:where(.dark, .dark *));
		  
		  /* Now any element with .dark will activate dark:* utilities */
		  ```
	- ### Utility Classes in HTML
		- ```html
		  <div class="border p-4 rounded-md shadow-md 
		              bg-slate-50 border-slate-300 
		              dark:border-slate-700 dark:bg-slate-900 dark:text-slate-100">
		    <h2 class="font-semibold text-lg">Card Title</h2>
		    <p class="mt-1.5 text-sm">This adjusts with dark mode.</p>
		  </div>
		  ```
-
- ## Animations & Transitions
	- https://tailwindcss.com/docs/animation
	- https://tailwindcss.com/docs/transition-property
	- https://stevekinney.com/courses/tailwind/tailwind-transition
	- ### Basic Transition
		- ```html
		  <button class="bg-blue-500 hover:bg-blue-700 text-white px-4 py-2 rounded transition-colors">
		    Hover me
		  </button>
		  
		  // transition-colors → applies transition to color properties (background-color, color, border-color).
		  // default duration: 150ms, default easing: ease-in-out.
		  ```
		- Other properties you can target:
			- `transition-opacity`
			- `transition-shadow`
			- `transition-transform`
			- `transition-all`
	- ### Basic Animation
		- ```html
		  <div class="w-8 h-8 bg-blue-500 animate-bounce rounded-full"></div>
		  ```
- ## Tailwind Tools
	- ### Tailwind Merge (`tailwind-merge`)
		- Helps **merge multiple Tailwind class strings** safely, avoiding conflicts
		- Useful when dynamically generating classes in React, Vue, or Angular
		- ```jsx
		  // Here, bg-red-500 and bg-green-500 might conflict
		  <div className={`p-4 bg-red-500 ${isActive ? 'bg-green-500' : 'bg-blue-500'}`}></div>
		  
		  //-----------------------------
		  
		  // Only the last conflicting class (bg-green-500) is applied
		  import { twMerge } from 'tailwind-merge';
		  <div className={twMerge('p-4 bg-red-500', isActive && 'bg-green-500')}></div>
		  
		  ```
	- ### Class Variance Authority (CVA)
		- https://cva.style/docs
		- Lets us **define reusable, variant-based components** with consistent Tailwind classes
		- Great for buttons, cards, or any UI element with multiple styles