回想一下，以前的Flexible方案是通过JavaScript来模拟`vw`的特性，那么到今天为止，`vw`已经得到了众多浏览器的支持，也就是说，可以直接考虑将`vw`单位运用于我们的适配布局中。



目前出视觉设计稿，我们都是使用`750px`宽度的，从上面的原理来看，那么`100vw = 750px`，即`1vw = 7.5px`。那么我们可以根据设计图上的`px`值直接转换成对应的`vw`值。



可以使用PostCSS的插件[postcss-px-to-viewport](https://github.com/evrone/postcss-px-to-viewport)







### 解决`1px`方案

为了解决`1px`的问题，使用PostCSS插件[postcss-write-svg](https://github.com/jonathantneal/postcss-write-svg),自动生成`border-image`或者`background-image`的图片



## Viewport不足之处

采用`vw`来做适配处理并不是只有好处没有任何缺点。有一些细节之处还是存在一定的缺陷的。比如当容器使用`vw`单位，`margin`采用`px`单位时，很容易造成整体宽度超过`100vw`，从而影响布局效果。对于类似这样的现象，我们可以采用相关的技术进行规避。比如将`margin`换成`padding`，并且配合`box-sizing`。只不过这不是最佳方案，随着将来浏览器或者应用自身的Webview对`calc()`函数的支持之后，碰到`vw`和`px`混合使用的时候，可以结合`calc()`函数一起使用，这样就可以完美的解决。

另外一点，`px`转换成`vw`单位，多少还会存在一定的像素差，毕竟很多时候无法完全整除。



另外，控制容器长宽比，可以用PostCSS插件[postcss-aspect-ratio-mini](https://github.com/yisibl/postcss-aspect-ratio-mini)