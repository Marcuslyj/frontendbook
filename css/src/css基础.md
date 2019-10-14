##### css3新特性有哪些？

##### 怎么让一个div水平垂直居中？

##### 分析比较 opacity: 0、visibility: hidden、display: none 优劣和适用场景



## 介绍下 BFC、IFC、GFC 和 FFC（或，介绍下 BFC 及其应用）

Formatting context(格式化上下文) 

### BFC

Block Formatting Contexts (块级格式化上下文)

具有 BFC 特性的元素可以看作是隔离了的独立容器，容器里面的元素不会在布局上影响到外面的元素，并且 BFC 具有普通容器所没有的一些特性。

BFC特性：

1. 内部box会在垂直方向，一个接一个地放置。
2. Box垂直方向的距离由margin决定，在一个BFC中，两个相邻的块级盒子的垂直外边距会产生折叠。
3. 在BFC中，每一个盒子的左外边缘（margin-left）会触碰到容器的左边缘(border-left)（对于从右到左的格式来说，则触碰到右边缘）
4. 形成了BFC的区域不会与float box重叠
5. 计算BFC高度时，浮动元素也参与计算

### 触发 BFC

只要元素满足下面任一条件即可触发 BFC 特性：

- body 根元素
- 浮动元素：float 除 none 以外的值
- 绝对定位元素：position (absolute、fixed)
- display 为 inline-block、table-cells、flex、flow-root
- overflow 除了 visible 以外的值 (hidden、auto、scroll)

### BFC应用

1. 同一个 BFC 下外边距会发生折叠
2. BFC 可以包含浮动的元素（清除浮动）
3. BFC 可以阻止元素被浮动元素覆盖

![img](../../_assets/image/v2-5ebd48f09fac875f0bd25823c76ba7fa_hd.png)











##### 字体图标原理？字体是如何在浏览器里被渲染出来的？

先说字符转义，`&#xe869;`中，`&`表示转义，`#x`可以用于表示16进制转义字符，而`&#`可以用来对十进制的数进行转义，如，`&#59497`

#### 3种viewport

#### 行内元素的padding和margin是否无效