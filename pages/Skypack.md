tags:: [[NPM]], [[CDN]], [[JavaScript]], [[ES Module]], [[Web Components]]

- https://www.skypack.dev/
- Is a [[CDN]] for [[NPM]] packages that allow to use [[JavaScript]] packages directly in the browser **without any installer, bundler or build tool**.
- It automatically delivers optimized, modern ES modules
-
- ```html
  <script type="module">
    import { debounce } from 'https://cdn.skypack.dev/lodash-es';
  
    const input = document.querySelector('#search');
    input.addEventListener('input', debounce(() => {
      console.log('Debounced input:', input.value);
    }, 300));
  </script>
  ```
- No `npm install` needed
- The browser gets an [[ES Module]] ready to use
- Perfect for quick prototypes or lightweight projects