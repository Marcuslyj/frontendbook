## Flexible方案

通过设置dpr对应1/dpr的scale

只处理了IOS，弃疗android





## border-image



## PostCSS Write SVG

使用`border-image`每次都要去调整图片，总是需要成本的。基于上述的原因，我们可以借助于PostCSS的插件[postcss-write-svg](https://link.juejin.im/?target=%2F%2Fgithub.com%2Fjonathantneal%2Fpostcss-write-svg)来帮助我们。



使用PostCSS的`postcss-write-svg`插件，除了可以使用`border-image`来实现`1px`的边框效果之外，还可以使用`background-image`来实现。



## transform+伪类

