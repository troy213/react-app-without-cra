# React App without CRA

## 1. Installing Dependencies

- npm init -y
- npm install react
- npm install react-dom
- npm install webpack --save-dev
- npm install webpack-cli --save-dev
- npm install webpack-dev-server --save-dev
- npm install babel-loader --save-dev
- npm install @babel/core --save-dev
- npm install @babel/preset-react --save-dev
- npm install @babel/preset-env --save-dev
- npm install html-webpack-plugin --save-dev

or you can shorten all up above to

```
npm init -y
npm i react react-dom
npm i webpack webpack-cli webpack-dev-server babel-loader @babel/core @babel/preset-react @babel/preset-env html-webpack-plugin --save-dev
```

## 2. Set Up Webpack Config and Folder Structure

webpack.config.js

```js
const path = require('path')
const HTMLWebpackPlugin = require('html-webpack-plugin')

module.exports = {
  entry: './src/index.js',
  output: {
    path: path.join(__dirname, '/build'),
    filename: 'bundle.js',
  },
  plugins: [
    new HTMLWebpackPlugin({
      template: './public/index.html',
    }),
  ],
  module: {
    rules: [
      {
        test: /.js$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['@babel/preset-env', '@babel/preset-react'],
          },
        },
      },
    ],
  },
}
```

public/index.html

_standard HTML boilerplate_

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>React App without CRA</title>
  </head>
  <body>
    <div id="root"></div>
  </body>
</html>
```

src/index.js

```js
import React from 'react'
import ReactDOM from 'react-dom'
import App from './component/App'

ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
)

// And if you use React 18

import { createRoot } from 'react-dom/client'

const container = document.getElementById('root')
const root = createRoot(container)
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
)
```

src/component/App.js

```js
import React from 'react'

const App = () => {
  return <h1>Hello World!</h1>
}

export default App
```

## 3. Edit scripts in package.json

```
"scripts": {
	"start": "webpack-dev-server --mode development --open --hot --port 3000"
	"build": "webpack --mode production"
}
```

explanation:

```
--open = used to display application in new tab when the script is running
--hot = used for Hot Module Replacement
--port = to specify which port the app will be open
```

## 4. Run the script!

Happy coding!
