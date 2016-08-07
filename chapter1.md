# Chapter 0 - Setup

### **Init**

Go ahead, create a new directory and jump in

```
mkdir universal-app && cd universal-app
```

Initialize a git repository

```
git init
```

Create a new branch `setup`

```
git checkout -b setup
```

Set node version to v6

```
nvm install 6 && nvm use 6

```

Add a README

```
echo 'Javascript Universal App' > README.md
```

Initialize npm (go thru the interactive setup)

```
npm init
```

Ignore `node_modules`
```
echo node_modules > .gitignore
```

You are all set!


### **Webpack**

Webpack is a widely used module bundler, and the first thing to setup

```
install webpack —-save-dev
```

First create a `/src` and `/dist` directories

```
mkdir src && mkdir dist
```

Save the following file as `webpack.config.js`


```js
var webpack = require('webpack')
var path = require('path')
module.exports = {  
  context: __dirname,  
  entry: './src/index.js',  
  output: {    
    path: path.resolve('dist'),    
    filename: 'bundle.js',  },  
    plugins: [ new webpack.NoErrorsPlugin() ],  
    resolve: {    
      extensions: ['', '.js', '.json'],    
      modulesDirectories: ['.', 'src', 'node_modules']  
    }
  }
}
```

Add `/dist` to the `.gitignore` file

```
node_modules
dist
```

Add `build` and `start` scripts to your `package.json`

```
"build": "webpack --config webpack.config.js", 
"start": "node dist/bundle.js",
```


**Test it**:

Create the following `index.js` file inside `/src`: 

```js
console.log('hello world’)
```

Now just `npm run build` and then  `npm run start`

You should see a `hello world` in your console, and you will find that you 1 line `src/index.js` has become a 51 lines `dist/bundle.js`. Yay... right? This will pay off in the future tho, as we start plugging stuff into webpack.


### **Babel**

Babel is a JavaScript compiler. It extends the language capabilities thru syntax transformers, we will need this in order to use ES2015 and React.

Get ready to install a truckload of dependencies

```
npm install --save babel-core babel-plugin-jsx-display-if babel-plugin-transform-object-rest-spread babel-polyfill babel-preset-es2015 babel-preset-react babel-register babel-runtime babel-loader
```

Add `.babelrc` to configure babel

```js
{ 
  "presets": ["es2015", "react"], 
  "plugins": [ 
    "transform-object-rest-spread", 
    "jsx-display-if" 
  ]
}
```

And finally add loader to `webpack.config.js` so webpack transpiles all the `.js` files using babel (except the ones in `node_modules`)

```js
module: {  
  loaders: [    
    {      
      test: /\.js$/,      
      loaders: ['babel'],      
      exclude: /node_modules/    
    }  
  ]
}
```

**Test it**:

index.js

const obj = { a: 1, b:2, c:3 }

const { a, ...rest } = obj

const spread = { ...rest, d: 4 }

console.log\(rest\) \/\/ { b:2, c: 3}

console.log\(spread\) \/\/ { b:2, c: 3, d: 4 }

tag \#babel

**PostCSS**

setup\/postcss branch

npm install --save-dev autoprefixer css-loader style-loader url-loader postcss-import postcss-loader postcss-mixins postcss-nested postcss-simple-vars

add loader to webpack.config.js

{

test: \/\(.scss\|.css\)$\/,

loaders: \['style', 'css?sourceMap&modules&importLoaders=1&localIdentName=\[name\]\_\_\[local\]\_\_\_\[hash:base64:5\]', 'postcss'\]

},

postcss: \[

require\('autoprefixer'\),

require\('postcss-import'\),

require\('postcss-nested'\),

require\('postcss-simple-vars'\)

\]

resolve.extensions ‘css’, ‘scss'

test it:

index.css

.red {

color: red;

}

index.js

import styles from '.\/index.css'

console.log\(styles\) \/\/ { red: '...' }

window.onload = \(\) =&gt; document.body.classList.add\(styles.red\)

index.html

&lt;script src="..\/dist\/bundle.js"&gt;&lt;\/script&gt;

&lt;body&gt;

Hello World

&lt;\/body&gt;

npm run build

open src\/index.html

tag \#postcss

**ESLint**

setup\/eslint branch

npm install --save-dev eslint babel-eslint eslint-config-standard eslint-config-standard-react eslint-plugin-babel eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-promise eslint-plugin-react eslint-plugin-standard eslint-watch

add .eslintrc

{

"env": {

"browser": true,

"node": true

},

"parser": "babel-eslint",

"extends": \["standard", "standard-react"\],

"rules": {

"comma-dangle" : \[0, "always-multiline"\],

"semi": \[2, "never"\],

"no-extra-semi": 2,

"jsx-quotes": \[2, "prefer-single"\],

"react\/jsx-boolean-value": \[0, "always"\],

"react\/jsx-max-props-per-line": \[2, {"maximum": 4}\],

"react\/self-closing-comp": 2,

"react\/jsx-indent-props": \[2, 2\],

"react\/sort-comp": 2

}

}

test it:

const a = 1

const b = 2

const c = 3 \/\/ ‘c’ is defined but never used

console.log\(a + b\)

tag \#eslint

**DevServer**

setup\/dev-server branch

npm install --save express

npm install --save-dev redbox-react webpack-dev-middleware webpack-hot-middleware

add dev-server.js

var webpack = require\('webpack'\)

var webpackDevMiddleware = require\('webpack-dev-middleware'\)

var webpackHotMiddleware = require\('webpack-hot-middleware'\)

var config = require\('.\/webpack.config.js'\)

var Express = require\('express'\)

var app = new Express\(\)

var port = process.env.PORT \|\| 9999

var compiler = webpack\(config\)

var dev = webpackDevMiddleware\(compiler, { noInfo: true, publicPath: config.output.publicPath }\)

var hot = webpackHotMiddleware\(compiler\)

app.use\(dev\)

app.use\(hot\)

app.get\('\*', function \(req, res\) {

res.send\(\`

&lt;html&gt;

&lt;head&gt;

&lt;title&gt;Webpack Development Server&lt;\/title&gt;

&lt;\/head&gt;

&lt;body&gt;

&lt;div id="root"&gt;

Hello World

&lt;\/div&gt;

&lt;\/body&gt;

&lt;script src="\/bundle.js" async defer&gt;&lt;\/script&gt;

&lt;\/html&gt;

\`\)

}\)

app.listen\(port, \(error\) =&gt; {

if \(error\) {

console.error\(error\)

return

}

console.info\('Open up http:\/\/localhost:%s\/ in your browser.', port\)

}\)

change webpack.config.js

devtool: 'cheap-module-eval-source-map',

entry: \[

'webpack-hot-middleware\/client',

'.\/src\/index.js'

\],

output: {

path: require\('path'\).resolve\('dist'\),

filename: 'bundle.js',

publicPath: '\/'

},

plugins: \[

new webpack.HotModuleReplacementPlugin\(\),

new webpack.NoErrorsPlugin\(\)

\]

remove index.html

add script "dev-server": "node dev-server.js”

test it

npm run dev-server

tag \#dev-server

