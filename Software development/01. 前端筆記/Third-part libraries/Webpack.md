---
tags:
  - "#Webpack"
---

#### Intro 
Webpack 是 **JS應用程式的靜態資源打包工具**。當建立應用程式時，通常會有很多不同的程式碼檔案，像是HTML、CSS、JavaScript等等。Webpack 是一個工具可以幫助把程式碼檔案整合在一起，讓應用程式運作得更有效率

Webpack 的工作方式有點像是把所有的程式碼檔案捆綁在一起，當使用者使用時，只需要下載一個大的檔案，而不是很多小檔案，這樣可以節省時間並提高速度。

Webpack 包含幾個核心部分：

- [Entry](#Entry)
- [Output](#Output)
- [Loaders](#Loaders)
- [Plugins](#Plugins)
- [Mode](#Mode)
- [Browser Compatibility](#Browser Compatibility)

> [Concept @Webpack官方文件](https://webpack.js.org/concepts/)

#### 安裝指令
```bash
$ npm install webpack webpack-cli --save-dev  
$ npx webpack # 預設以 ./src/index.js 為 entry；以 ./dist/main.js 為 output  
  
# 預設就會吃 webpack.config.js，因此除非檔名有不同，否則可以省略  
$ npx webpack --config webpack.config.js  
  
$ npx webpack -p # build in production  
  
$ npx webpack-dev-server --open # run in dev-server 
```


#### 解決的問題
1. 將所有 js 檔案打包成單一檔案，減少請求次數，提高加載效能
 2. 透過不同loader讓檔案轉換成babel 支援語法轉換（例如：將JavaScript ES6 或 ES7轉換成舊版本，以確保在不同的瀏覽器上都能運行，或是使用sass或less轉換成css）
 3. 使用 `npm packages` 來開發，webpack 會整合所有套件
 4. Minify 或優化程式碼，減少檔案大小
 5. 使用 HMR（Hot Module Replacement）


#### Entry
設定 webpack 的進入點是哪隻檔案，預設會使用 `./src/index.js`

#### Output
設定 bundle 過的檔案的位置及其檔名，預設會使用 `/dist/main.js`

####  Loaders
webpack 預設可以解析 JavaScript 和 JSON ，但應用程式中仍可能包含許多其他類型的檔案例如：圖片，這時候會需要透過 loader 來處理 JS / JSON 以外的檔案類型。在設定時，是透過 `module.rules` 的屬性來設定。

```javascript
const path = require('path');

module.exports = {
  output: {
    filename: 'my-first-webpack.bundle.js',
  },
  module: {
    rules: [{ test: /\.txt$/, use: 'raw-loader' }],
  },
};
```

> [!WARNING]  
> 特別留意使用 regex 來選擇要套用該 loader 的檔案類型是，**不要加上單引號或雙引號**，也就是使用 `/\.txt$/`，而不是 `'/\.txt$/'` 或 `"/\.txt$/"`

#### [[常見 Webpack Plugins]] 
Loaders 用來處理特定類型的檔案，而 plugins 則可以用來執行某些功能更廣泛的任務，像是打包最佳化（bundle optimization）、資源管理（asset management）和注入環境變數。

```javascript
const HtmlWebpackPlugin = require('html-webpack-plugin') // installed via npm
const webpack = require('webpack'); //to access built-in plugins

module.exports = {
  module: {
    rules: [{ test: /\.txt$/, use: 'raw-loader' }],
  },
  plugins: [new HtmlWebpackPlugin({ template: './src/index.html' })],
};
// html-webpack-plugin 為應用程式產生一個 HTML 文件，並自動將所有產生的套件注入到該文件中
```



> [!info] 
> 由於可以根據需求在設定檔的不同位置重複使用該 plugin，因此在使用 plugin 是需使用 `new` 來確保每個 plugin 是獨立的 instance。
> 

#### Mode[​](https://pjchender.dev/webpack/note-webpack/#mode "Mode的直接連結")

預設值是 `production`，也可以設為 `development` 或 `none`。
透過這個設定，webpack 會自動啟用最佳化的策略。
```javascript
module.exports = {
  mode: 'production',
};
```

##### Browser Compatibility 
Webpack 支援所有符合ES5 的瀏覽器

#### Reference 
[Webpack官方文件](https://webpack.js.org/guides/)