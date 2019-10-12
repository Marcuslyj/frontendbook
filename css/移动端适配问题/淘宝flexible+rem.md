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

iphone6：

```xml
<meta name="viewport" content="initial-scale=0.5, maximum-scale=0.5, minimum-scale=0.5, user-scalable=no">
```

注意：

如果没有viewport的meta，插件才会自己加上



##### ios vs android

现在的 lib-flexible 有两个版本，master 版本和 2.0 版本。在 master 版本中使用 正则来判断系统种类（IOS/Andorid），但是只对 IOS 系统做了 dpr 的适配，对于 Android 手机，统一设置 dpr =1；

即，1px问题，flexible值处理了IOS！

###### 为什么弃疗android

lexible只处理了IOS机型，非iOS机型还是采用传统的scale=1.0，原因是在于安卓手机不一定有devicePixelRatio属性,以及devicePixelRatio的不规范（某些带小数），导致Flexible放弃治疗。









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

则设置font-size为75px（dpr为1的情况）







### 文本字号不建议使用`rem`

显然，我们在iPhone3G和iPhone4的Retina屏下面，希望看到的文本字号是相同的。也就是说，我们不希望文本在Retina屏幕下变小，另外，我们希望在大屏手机上看到更多文本，以及，现在绝大多数的字体文件都自带一些点阵尺寸，通常是`16px`和`24px`，所以我们不希望出现`13px`和`15px`这样的奇葩尺寸。

如此一来，就决定了在制作H5的页面中，`rem`并不适合用到段落文本上。所以在Flexible整个适配方案中，考虑文本还是使用`px`作为单位。只不过使用`[data-dpr]`属性来区分不同`dpr`下的文本字号大小。

```scss
@mixin font-dpr($font-size){
    font-size: $font-size;
 
    [data-dpr="2"] & {
        font-size: $font-size * 2;
    }
 
    [data-dpr="3"] & {
        font-size: $font-size * 3;
    }
}
```













































