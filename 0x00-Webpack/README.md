# 0x00. Webpack

## Overview

Webpack is a powerful tool for bundling JavaScript modules, along with other assets like CSS, images, and fonts.

## Resources

- [Webpack Concepts - Official Documentation](https://webpack.js.org/concepts/)
- [A Beginner's Guide to Webpack](https://www.sitepoint.com/webpack-beginner-guide/)

## Setting Up Webpack

### Step 1: Installation

First, ensure you have Node.js and npm (Node Package Manager) installed on your system. Then, initialize your project and install Webpack:

```bash
npm init -y
npm install webpack webpack-cli --save-dev
```

### Step 2: Project Structure

Create a directory structure for your project, including folders for source code (`src`) and output (`dist`). Your project structure might look like this:

```
project
│   ├── src
│   │   └── index.js
│   └── dist
│       └── index.html
└── package.json
```

### Step 3: Configuration

Create a `webpack.config.js` file in the root of your project to define Webpack configuration:

```javascript
const path = require('path');

module.exports = {
  entry: './src/index.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js',
  },
  // Add loaders and plugins here
};
```

### Entry Points and Output

- **Entry Points**: Define the entry point(s) of your application in the `entry` field. This is where Webpack starts bundling your files.
- **Output**: Specify the output configuration in the `output` field, including the output directory (`path`) and the bundled file name (`filename`).

## Loaders

Loaders allow Webpack to process different file types (like CSS, images, and fonts) by transforming them into valid modules that can be included in your bundle.

### Example: Adding Babel Loader

To use Babel with Webpack for transpiling ES6+ JavaScript:

```bash
npm install babel-loader @babel/core @babel/preset-env --save-dev
```

Update your `webpack.config.js`:

```javascript
module.exports = {
  // other config...
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['@babel/preset-env']
          }
        }
      }
    ]
  }
};
```

## Plugins

Webpack plugins extend its functionality for tasks like code optimization, asset management, and more.

### Example: Adding HtmlWebpackPlugin

To automatically generate HTML files with script tags for your bundles:

```bash
npm install html-webpack-plugin --save-dev
```

Update your `webpack.config.js`:

```javascript
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  // other config...
  plugins: [
    new HtmlWebpackPlugin({
      template: './src/index.html',
    })
  ]
};
```

## Code Splitting

Code splitting improves performance by splitting your code into smaller chunks, which can be loaded on demand.

### Example: Dynamic Import

Use dynamic import to split code into separate bundles:

```javascript
const button = document.getElementById('loadButton');

button.addEventListener('click', () => {
  import('./dynamicModule.js')
    .then(module => {
      // Use module
    })
    .catch(error => {
      // Handle error
    });
});
```

## Dev Server

Webpack Dev Server provides a live development server with hot reloading for easier development.

### Installation

```bash
npm install webpack-dev-server --save-dev
```

### Configuration

Update your `webpack.config.js`:

```javascript
module.exports = {
  // other config...
  devServer: {
    contentBase: path.join(__dirname, 'dist'),
    compress: true,
    port: 9000,
  }
};
```

### Running Dev Server

Add a script in your `package.json`:

```json
"scripts": {
  "start": "webpack-dev-server --open"
}
```

Now you can start the dev server with:

```bash
npm start
```

This will open your default browser and serve your project from `http://localhost:9000`.
