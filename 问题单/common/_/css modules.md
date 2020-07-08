# CSS Modules

本文介绍的 [CSS Modules](https://github.com/css-modules/css-modules) 有所不同。它不是将 CSS 改造成编程语言，而是功能很单纯，只加入了局部作用域和模块依赖，这恰恰是网页组件最急需的功能。

因此，CSS Modules 很容易学，因为它的规则少，同时又非常有用，可以保证某个组件的样式，不会影响到其他组件。 



## 局部作用域

CSS的规则都是全局的，任何一个组件的样式规则，都对整个页面有效。

产生局部作用域的唯一方法，就是使用一个独一无二的`class`的名字，不会与其他选择器重名。这就是 CSS Modules 的做法。



下面是一个React组件[`App.js`](https://github.com/ruanyf/css-modules-demos/blob/master/demo01/components/App.js)。

 ```jsx
 import React from 'react';
 import style from './App.css';
 
 export default () => {
   return (
     <h1 className={style.title}>
       Hello World
     </h1>
   );
 };
 ```

上面代码中，我们将样式文件[`App.css`](https://github.com/ruanyf/css-modules-demos/blob/master/demo01/components/App.css)输入到`style`对象，然后引用`style.title`代表一个`class`。

```css
.title {
  color: red;
}
```

构建工具会将类名`style.title`编译成一个哈希字符串。

```css
<h1 class="_3zyde4l1yATCOkgn-DBWEL">
  Hello World
</h1>
```

`App.css`也会同时被编译。

```css
._3zyde4l1yATCOkgn-DBWEL {
  color: red;
}
```

这样一来，这个类名就变成独一无二了，只对`App`组件有效。