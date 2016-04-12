---
layout:  post
title:  "Webpack学习笔记（1）—— 模块化与Webpack"
---

## 为什么会有module
>  
Today’s websites are evolving into web apps:  
  - More and more JavaScript is in a page.  
  - You can do more stuff in modern browsers.  
  - Fewer full page reloads → even more code in a page.  
> As a result there is a lot of code on the client side!
A big code base needs to be organized. Module systems offer the option to split your code base into modules.  
>  ***—— [WEBPACK](http://webpack.github.io/docs/motivation.html)***  

总的来说，就是前端应用越来越复杂，催生了模块化。

## 如何实现模块化

目前模块化的解决方案或者标准有：
  - AMD  
  {% highlight javascript linenos %}
  require(["module", "../file"], function(module, file) { /* ... */ });   
  define("mymodule", ["dep1", "dep2"], function(d1, d2) {  
  return someExportedValue;  
  });  
  {% endhighlight %}   

  可以异步加载，实现方案有：  
    - requireJS  
    - curl  

  - commonJS  

  {% highlight javascript linenos %}
  require("module");  
  require("../file.js");  
  exports.doStuff = function() {};  
  module.exports = someValue;  
  {% endhighlight %}  
  不能异步加载，实现方案有：  
    - node.js - server-side  
    - browserify  
    - modules-webmake - compile to one bundle  
    - wreq - client-side  

  - ES6  
  {% highlight javascript linenos %}  
  import "jquery";  
  export function doStuff() {}  
  module "localModule" {}  
  {% endhighlight %}  

  目前没有实现方案

  - 其它

## 模块如何加载
1. 一次性全部加载  
2. 每次模块单独加载  
3. 分块，每块中包含一个或者多个模块。`Webpack`就是干这个的  

## webpack要做什么
  webpack把任何资源（包括字体、模板、图片等，不仅仅是javascript）封装成module，解析并形成最终加载的文档。
