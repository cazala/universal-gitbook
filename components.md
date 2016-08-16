# Chapter 1 - Components

The purpose of this chapter is to create a few stateless views of our application using React.

**Branch**: To see the commits of this chapter checkout [this branch](https://github.com/cazala/universal-app/pull/1).

**Release**: To skip this chapter just clone [this release](https://github.com/cazala/universal-app/releases/tag/Setup).

---

## React

[React](https://facebook.github.io/react/) is a library for building user interfaces. Why so much hype about this technology? Here are a few key points:

+ **Component-based**: simple components can be encapsulated and composed into more complex UIs. 

+ **Declarative**: components can be just a functions that take properties and return JSX, making them predicatble and easy to debug, since data flows just in one way (in contrast to Angular's two-way bindings)

+ **Virtual DOM**: React holds a representation of the DOM and updates the actual DOM only when necessary by diff'ing the changes in the virtual DOM. This makes React very fast and also  allows it to be rendered on the client, the server, or on mobile apps thru [React Native](https://facebook.github.io/react-native/)

Now go ahead and install these deps:

```
npm install react react-dom --save
npm install react-loader --save-dev
```
Add `react-hot` to your webpack loaders:

```js
{ 
  test: /\.js$/, 
  loaders: ['react-hot', 'babel'], 
  exclude: /node_modules/
},
```

So lets create a simple `App` component -> make a `components` folder inside `src`, and save the following file as `src/components/App.js`:

```js
import React, { PropTypes } from 'react'
import styles from './App.css'

const App = (props) => ( 
  <div className={styles.header}> {props.text} </div>
)

App.propTypes = { 
  text: PropTypes.string.isRequired
}

export default App
```

And the following as `src/components/App.css`

```css
.header { 
  font-size: 20px; 
  color: blue;
}
```

**NOTE**: there are different opinions about what folder structure to follow, some people separate components in individual folders, or by page in a nested fashion, or by feature, etc. I''ll let you figure out the folder structure that works best for you, I'll just drop all the `js` and `css` files in `components` by component name.

So we just created a component that receives a `text` property which is a string, and renders a `<div>` with that text in blue.

Now lets use this component and rendering using `react-dom`, save the following as `src/index.js`

```js
import 'babel-polyfill'
import React from 'react'
import ReactDOM from 'react-dom'
import App from 'components/App'

const app = <App text='Hello Wolrd' />
const root = document.getElementById('root')

ReactDOM.render(app, root)
```
That will import our component, render it passing `'Hello Wolrd'` as its `text` property, and mount it on the `#root` element of the document, using `react-dom`.

In order for this line to work:

```js
import App from 'components/App'
```

We'll need to add an alias for `components` in our webpack config's `resolve.alias`:

```js
resolve: { 
  alias: { 
    'components': 'src/components' 
  },
  ...
}
```

---

**Test It Out**:

Now just `npm run dev-server` and open up `http://localhost:9999`, you should see a blue *Hello World* in the screen.

---

**Diff**: to see the diff for this step [click here](https://github.com/cazala/universal-app/commit/75e8f3a76a4d5666adb8c9958535a422c2e259de).

**Fast-forward**: `git clone --branch react https://github.com/cazala/universal-app.git --depth=1`

---

## React Toolbox

[React Toolbox](http://react-toolbox.com/) is a UI kit. We'll install it so we don't have to waste much time making the most basic components, but you don't actually need this to use React.

```
npm install --save react-toolbox react-addons-update react-addons-css-transition-group normalize.css
npm install --save-dev sass-loader node-sass
```

We'll need `sass-loader` in order to use `React Toolbox` from webpack.

So add it to the end of the loaders list for css files:

```js
{ 
  test: /(\.scss|\.css)$/, 
  loaders: ['style', 'css?sourceMap&modules&importLoaders=1&localIdentName=[name]__[local]___[hash:base64:5]', 'postcss', 'sass?sourceMap'] 
}

```

Also we can add a `theme.css` file at the root level of our app to set the colors of the variables:

```scss
@import "~react-toolbox/lib/colors";

$color-primary: #00A0DF !default;
$color-primary-dark: #00607C !default;
$color-accent: #77BC1F !default;
$color-accent-dark: #009444 !default;
$color-primary-contrast: #ffffff !default;
$color-accent-contrast: #646469 !default;
```

And just add this to `webpack.config.js` so the sass loader includes our `theme.css` variables:

```js
sassLoader: { 
  data: '@import "' + path.resolve(__dirname, 'theme.css') + '";' 
},
```

You are all set.

---

**Test It Out**:

Add this line as your last import in `src/components/App`

```js
import Button from 'react-toolbox/lib/button'
```

And change your App component to this:

```js
const App = (props) => ( 
  <Button label={props.text} />
)
```

Now `npm run dev-server` and you should see this time a button that reads *Hello Wolrd*.

---

**Diff**: to see the diff for this step [click here](https://github.com/cazala/universal-app/commit/75e8f3a76a4d5666adb8c9958535a422c2e259de).

**Fast-forward**: `git clone --branch react https://github.com/cazala/universal-app.git --depth=1`

---
