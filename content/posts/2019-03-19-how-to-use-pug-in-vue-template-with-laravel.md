+++
categories = ["laravel", "vue", "pug"]
date = "2021-04-04"
description = "How to use pug(jade) in Vue templates with Laravel Mix configuration"
title = "Pug in Vue template with Laravel"
+++

# Introduction

Pug (known as jade) is an awesome way to write HTML and I have used it in past with Gulp but with server side rendering it is tough so I stopped now I am finally developing a SPA powered by VueJS so I thought I will use it but I faced some difficulty in setup because I don't understand how Webpack works, after some trial and error I have finally found this snippet, it was in GitHub issue comments on Laravel mix repository, enjoy.

Add these lines to your `webpack.mix.js`

```js
const mix = require('laravel-mix');

// Start copy from here
mix.webpackConfig({
   module: {
      rules: [
         {
            test: /\.pug$/,
            oneOf: [
               {
                  resourceQuery: /^\?vue/,
                  use: ['pug-plain-loader']
               },
               {
                  use: ['raw-loader', 'pug-plain-loader']
               }
            ]
         }
      ]
   }
});
// Stop copy here

mix.js('resources/js/app.js', 'public/js')
   .sass('resources/sass/app.sass', 'public/css');
```

Now open your terminal and type `npm install pug pug-plain-loader vue vue-template-compiler`