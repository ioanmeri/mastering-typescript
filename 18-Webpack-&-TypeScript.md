# Webpack & TypeScript

## Installing Webpack Dependencies

```
npm install --save-dev webpack webpack-cli typescript ts-loader
```

`Typescript` is a dependency because this is what you usually do. You don't use the global TS instal in an individual package that you are going to sharing with people.

`ts-loader` is the middleman between typescript and webpack. It is going to call TS, basically the `tsc` command and compile TS into JS and handle that over to webpack which then it will bundle everything together

---

## Adding Source Maps

Source maps will basically take the minified bundle and map it backwards to it's pre-build state.

`tsconfig.json`

```
sourceMap: true
```

and

`webpack.config.js`

```
devtool: "inline-source-map",
```

---

## Webpack Dev Server

```
npm install --save-dev webpack-dev-server
```

also add in `package.json`:

```
"serve": "webpack serve",
```

and in `webpack.config.js`:

```
publicPath: "/dist",
```

in output
