[video](https://www.youtube.com/watch?v=TOb1c39m64A)

```pwsh
npm init -y
npm install react-dom react
```

```bash
npm install --save-dev webpack webpack-cli webpack-dev-server
```

```shell
npm install --save-dev @babel/core babel-loader @babel/preset-react @babel/preset-env
```

```sh
npm install --save-dev html-webpack-plugin
```

-   folder

    -   node_modules

    -   webpack.config.js
        -   src
        -   index.js
        -   index.html
    -   package.json
    -   package-lock.json

webpack.config.js:

```js
const path = require("path");
const HTMLWebpackPlugin = require("html-webpack-plugin");

module.exports = {
    entry: "./src/index.js",

    output: {
        path: path.join(__dirname, "/dist"),
        filename: "bundle.js",
    },
    plugin: [
        new HTMLWebpackPlugin({
            template: "./src/index.html",
        }),
    ],

    module: {
        rule: [
            {
                test: /.js$/,
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

index.js:

```jsx
import React from "react";
import ReactDOM from "react-dom";
import App from "./components/App";

ReactDOM.render(<App />, document.getElementById("root"));
```

index.html:

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Document</title>
    </head>
    <body>
        <div id="root"></div>
    </body>
</html>
```

packate.json:

```json
{
    "private": true,
    "scripts": {
        "start": "webpack-dev-server --mode development --open --hot",
        "build": "webpack --mode production"
    }
}
```
