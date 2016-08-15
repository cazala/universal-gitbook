# Chapter 1 - Components

The purpose of this chapter is to create a few stateless views of our application using React.

**Branch**: To see the commits of this chapter checkout [this branch](https://github.com/cazala/universal-app/commits/setup).

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

So lets create a simple `App` component: make a `components` folder inside `src`, and save the following file as `App.js`:

