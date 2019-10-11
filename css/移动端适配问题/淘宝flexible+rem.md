> Q:能谈谈rem的作用吗，与em有什么区别？ 
>
> A: rem 是html 的font-size大小，一般为 16px， em 是父节点的 font-size 大小 
>
> Q: 我们为什么要用rem去做手机的适配？如果rem只是根节点字体大小的话，那么rem 其实和px 、em没有区别，rem解决了什么问题？

自己来：

通过媒体查询，不同尺寸屏幕设置不同的根元素字体大小，那我们用rem表示的尺寸就成了动态尺寸，达到屏幕的适配效果。







#### dpr

dpr实际上是一个比值，标识一个虚拟像素对应几个物理像素。

![img](../../_assets/image/webp)

#### lib-flexible 设置 dpr 又是为了什么？

为了解决“极致的1px”问题。

原理其实也很简单，对于 dpr=2的设备，设置 rem 的值为正常值的 2 倍，将需要画出“极致的线”的地方使用1px表示，再将页面缩小2倍，这样1px的线就变成了“0.5px”，实际上为1个物理像素来表示。

##### ios vs android

现在的 lib-flexible 有两个版本，master 版本和 2.0 版本。在 master 版本中使用 正则来判断系统种类（IOS/Andorid），但是只对 IOS 系统做了 dpr 的适配，对于 Android 手机，统一设置 dpr =1；









#### px2rem

```js
{
    loader: 'px2rem-loader',
        options: {
            // 默认 dpr 2
            // 1rem对应75px
            remUnit: 75,
            // px转成rem后的小数点位数
            remPrecision: 8
        }
}
```

flexible中，把设备宽度分成10份，一份就是1rem，即750px（10rem）屏宽为例，1rem = 75px





















































