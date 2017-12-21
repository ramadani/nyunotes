## SASS loader in create-react-app project

Install `sass-loader` and `node-sass` with following commands:

* `npm install sass-loader node-sass --save-dev`, or
* `yarn add sass-loader node-sass --dev`, if you prefer using yarn

run `npm run eject` for using configs from `create-react-app` project. there are few webpack configurations will be exported, it is `webpack.config.dev.js` and `webpack.config.prod.js`.

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

### Reference
* [Adding Sass or Scss to Create-React-App](https://medium.com/@Connorelsea/using-sass-with-create-react-app-7125d6913760)