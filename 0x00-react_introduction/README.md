# 0x01. React Intro

## Table of Contents

1. [How to Create a Basic Javascript Application using React](#how-to-create-a-basic-javascript-application-using-react)
2. [How to Use the Package `create-react-app` to Start Developing Quickly with React](#how-to-use-the-package-create-react-app-to-start-developing-quickly-with-react)
3. [What JSX is and How to Use It](#what-jsx-is-and-how-to-use-it)
4. [How to Use the React Developer Tools to Debug Your Code](#how-to-use-the-react-developer-tools-to-debug-your-code)
5. [How to Use Enzyme's Shallow Rendering to Test Your Application](#how-to-use-enzymes-shallow-rendering-to-test-your-application)
6. [How to Use React with Webpack & Babel](#how-to-use-react-with-webpack--babel)
7. [Resources](#resources)

---

## How to Create a Basic Javascript Application using React

React is a powerful JavaScript library for building user interfaces, particularly single-page applications where you want a fast and interactive user experience. To create a basic application with React, follow these steps:

1. **Setup your development environment:**

   - Install Node.js and npm from [Node.js official website](https://nodejs.org/).
   - Verify the installation by running `node -v` and `npm -v` in your terminal.

2. **Initialize a React project:**

   - Open your terminal and create a new directory for your project: `mkdir my-react-app && cd my-react-app`
   - Initialize a new npm project: `npm init -y`

3. **Install React and ReactDOM:**

   - Run `npm install react react-dom`

4. **Create a basic React component:**

   - Create a new file `App.js` with the following content:

   ```javascript
   import React from "react";

   function App() {
     return (
       <div>
         <h1>Hello, React!</h1>
       </div>
     );
   }

   export default App;
   ```

5. **Create an entry point:**

   - Create an `index.js` file with the following content:

   ```javascript
   import React from "react";
   import ReactDOM from "react-dom";
   import App from "./App";

   ReactDOM.render(<App />, document.getElementById("root"));
   ```

6. **Setup an HTML file:**

   - Create an `index.html` file in a `public` directory:

   ```html
   <!DOCTYPE html>
   <html lang="en">
     <head>
       <meta charset="UTF-8" />
       <meta name="viewport" content="width=device-width, initial-scale=1.0" />
       <title>My React App</title>
     </head>
     <body>
       <div id="root"></div>
       <script src="index.js"></script>
     </body>
   </html>
   ```

7. **Run the application:**
   - To run the application, you'll need a bundler like Webpack (covered later) or use `create-react-app` for simplicity (next section).

---

## How to Use the Package `create-react-app` to Start Developing Quickly with React

`create-react-app` is a command line tool that helps you quickly create and set up a new React application without having to configure build tools like Webpack and Babel manually.

1. **Install `create-react-app`:**

   - Run `npx create-react-app my-react-app`

2. **Navigate into your project directory:**

   - `cd my-react-app`

3. **Start the development server:**
   - `npm start`

This will start a local development server and open your new React application in the browser. You can now start developing your application by modifying the files in the `src` directory.

---

## What JSX is and How to Use It

JSX stands for JavaScript XML. It is a syntax extension for JavaScript that allows you to write HTML directly within React.

1. **JSX Syntax:**

   - JSX allows you to write elements in a format that looks very similar to HTML.

   ```javascript
   const element = <h1>Hello, world!</h1>;
   ```

2. **Embedding Expressions:**

   - You can embed any JavaScript expression in JSX by wrapping it in curly braces.

   ```javascript
   const name = "Josh";
   const element = <h1>Hello, {name}</h1>;
   ```

3. **Attributes in JSX:**

   - JSX attributes are written in camelCase.

   ```javascript
   const element = <div tabIndex="0"></div>;
   ```

4. **Using JSX in Components:**
   - You can use JSX to define what a component should render.
   ```javascript
   function Welcome(props) {
     return <h1>Hello, {props.name}</h1>;
   }
   ```

---

## How to Use the React Developer Tools to Debug Your Code

React Developer Tools is a browser extension that allows you to inspect the React component hierarchy in the Chrome and Firefox Developer Tools.

1. **Install the React Developer Tools:**

   - Chrome: Install from the [Chrome Web Store](https://chrome.google.com/webstore/detail/react-developer-tools).
   - Firefox: Install from the [Firefox Add-ons site](https://addons.mozilla.org/en-US/firefox/addon/react-devtools/).

2. **Using the Tools:**

   - Open your React application in the browser.
   - Open the developer tools (F12 or right-click -> Inspect).
   - Navigate to the "React" tab to inspect your component tree.

3. **Features:**
   - Inspect and edit component props and state.
   - View the component hierarchy.
   - Performance monitoring tools.

---

## How to Use Enzyme's Shallow Rendering to Test Your Application

Enzyme is a JavaScript Testing utility for React that makes it easier to test your React components' output.

1. **Install Enzyme and its Adapter:**

   - `npm install enzyme enzyme-adapter-react-16`

2. **Setup Enzyme:**

   - Create a setup file, e.g., `setupTests.js`:

   ```javascript
   import { configure } from "enzyme";
   import Adapter from "enzyme-adapter-react-16";

   configure({ adapter: new Adapter() });
   ```

3. **Write a shallow rendering test:**

   - Create a test file, e.g., `App.test.js`:

   ```javascript
   import React from "react";
   import { shallow } from "enzyme";
   import App from "./App";

   it("renders without crashing", () => {
     shallow(<App />);
   });
   ```

4. **Run your tests:**
   - Use `npm test` to run your tests.

Shallow rendering renders only the component itself without its children, making it a fast and isolated test method.

---

## How to Use React with Webpack & Babel

Webpack and Babel are powerful tools for bundling your JavaScript applications and transpiling modern JavaScript syntax to be compatible with older browsers.

1. **Install Webpack and Babel:**

   - `npm install --save-dev webpack webpack-cli babel-loader @babel/core @babel/preset-env @babel/preset-react`

2. **Create a Webpack configuration file:**

   - `webpack.config.js`:

   ```javascript
   const path = require("path");

   module.exports = {
     entry: "./src/index.js",
     output: {
       path: path.resolve(__dirname, "dist"),
       filename: "bundle.js",
     },
     module: {
       rules: [
         {
           test: /\.js$/,
           exclude: /node_modules/,
           use: {
             loader: "babel-loader",
             options: {
               presets: ["@babel/preset-env", "@babel/preset-react"],
             },
           },
         },
       ],
     },
   };
   ```

3. **Create a Babel configuration file:**

   - `.babelrc`:

   ```json
   {
     "presets": ["@babel/preset-env", "@babel/preset-react"]
   }
   ```

4. **Update `package.json` scripts:**

   ```json
   "scripts": {
     "build": "webpack --mode production",
     "start": "webpack serve --mode development --open"
   }
   ```

5. **Run Webpack:**
   - `npm run build` to build your application.
   - `npm start` to start a development server.

By using Webpack and Babel, you can bundle your JavaScript files and ensure that your code is compatible with a wide range of browsers.

### Resources

- [React Official website](https://react.dev/)
- [getting started with React](https://www.taniarascia.com/getting-started-with-react/)
- [Quick Start ith React](https://react.dev/learn)
- [create-react-app](https://github.com/facebook/create-react-app)
- [React Dev Tools](https://chromewebstore.google.com/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)
- [hat is Bable?](https://babeljs.io/docs/)
- [Enzyme](https://enzymejs.github.io/enzyme/docs/api/shallow.html)
