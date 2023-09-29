---
tags:
  - Webpack
---
#### 1. HtmlWebpackPlugin：將 CSS 與 JS 注入 HTML 中

透過 **HtmlWebpackPlugin** 可以產生 HTML5 的檔案，並且把 webpack 打包好的檔案以 `<script>` 注入到 HTML 的 `<body>` 內。此外，如果你有使用 [mini-css-extract-plugin](https://github.com/webpack-contrib/mini-css-extract-plugin) 來產生 CSS 檔，HtmlWebpackPlugin 也會將 CSS 檔以 `<link>` 注入到 HTML 的 `<head>` 內。

##### 安裝

```bash
npm install html-webpack-plugin --save-dev
```

##### 設定

HtmlWebpackPlugin 會自動拿 `output.publicPath` 的路徑，灌到 template 的 `<script>` 中，如果在 `webpack.config.js` 中沒有設定 `output.publicPath` 的話，當網址切換時可能會無法順利載到 bundle 過的檔案：

```js
// webpack.config.js
const HtmlWebpackPlugin = require('html-webpack-plugin');
module.exports = {  
// ...  plugins: [    /* 只是要在 HTML 添加打包好的 webpack 檔案 */    // new HtmlWebpackPlugin(),    /* 或者也可以定義要使用的樣版，或其他更多參數 */    new HtmlWebpackPlugin({      title: 'Webpack 6 - Output Management with HtmlWebpackPlugin',      template: './index.html', // 以 index.html 這支檔案當作模版注入 html    }),  ],};

```

提示

HtmlWebpackPlugin 還有其他可用的參數可以參考 [html-webpack-plugin > options](https://github.com/jantimon/html-webpack-plugin#options) 的說明。

> - [Setting up HtmlWebpackPlugin](https://webpack.js.org/guides/output-management/#setting-up-htmlwebpackplugin) @ Webpack Guides > Output Management