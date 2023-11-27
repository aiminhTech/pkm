tags:: [[React]], [[Vue.js]]

- stands for**JavaScript XML** . It is a syntax extension for JavaScript that allows us to write HTML-like code within our JavaScript code.
- commonly used with React, a popular JavaScript library for building user interfaces.
- JSX syntax closely resembles HTML, using familiar HTML tags to define the structure of components. One key difference is that we use curly braces {} to embed JavaScript expressions within JSX. This allows us to dynamically generate content and include JavaScript logic directly in our markup.
- ```jsx
  import React from 'react';
  
  const App = () => {
    const name = 'John Doe';
    return (
      <div>
        <h1>Hello, {name}!</h1>
        <p>Welcome to my website.</p>
      </div>
    );
  };
  
  export default App;
  
  ```