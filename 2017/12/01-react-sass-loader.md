## SASS loader in create-react-app project

Install `sass-loader` and `node-sass` with following commands:

* `npm install sass-loader node-sass --save-dev`, or
* `yarn add sass-loader node-sass --dev`, if you prefer using yarn

run `npm run eject` for using configs from `create-react-app` project. there are few webpack configurations will be exported, it is `webpack.config.dev.js` and `webpack.config.prod.js`.


### Development

In `webpack.config.dev.js` file, add this code to `modules` block

```
{
  test: /\.scss$/,
  use: [{
      loader: "style-loader" // creates style nodes from JS strings
  }, {
      loader: "css-loader" // translates CSS into CommonJS
  }, {
      loader: "sass-loader", // compiles Sass to CSS
      options: {
        includePaths: ['node_modules']
      },
  }]
},
```

add `includePaths: ['node_modules']` to `options` block for including dependencies from another packages.


### Production

In `webpack.config.prod.js` file, add this code

```
const extractSass = new ExtractTextPlugin({
  filename: cssFilename,
  disable: process.env.NODE_ENV === "development"
});
```

`cssFilename` was defined in that's file, and then add this code to `modules` block

```
{
  test: /\.scss$/,
  use: extractSass.extract({
      use: [{
          loader: "css-loader"
      }, {
          loader: "sass-loader",
          options: {
            includePaths: ['node_modules']
          },
      }],
      // use style-loader in development
      fallback: "style-loader"
  })
},
```

and then add this code to `plugin` block

```
plugins: [

  ......
  extractSass,
],
```

### Reference
* [Adding Sass or Scss to Create-React-App](https://medium.com/@Connorelsea/using-sass-with-create-react-app-7125d6913760)
* [sass-loader documentation](https://github.com/webpack-contrib/sass-loader)