#### 什么是防抖和节流？有什么区别？如何实现？

#### call 和 apply 的区别是什么，哪个性能更好一些？并实现

区别：apply参数是数组

性能：call性能更好，

为什么call 比apply 快？ 这里就要提到他们被调用之后发生了什么。

apply做了更多的判断转换操作，最后调用的是call。

```
Function.prototype.apply (thisArg, argArray)
```

1. 如果IsCallable（Function）为false，即Function不可以被调用，则抛出一个TypeError异常。

2. 如果argArray为null或未定义，则返回调用function的[[Call]]内部方法的结果，提供thisArg和一个空数组作为参数。

3. 如果 Type（argArray）不是Object，则抛出TypeError异常。

4. 获取argArray的长度。调用argArray的[[Get]]内部方法，找到属性length。 赋值给len。

5. 定义 n 为ToUint32（len）。ToUint32（len）方法：将其参数len转换为范围为0到2^32-1的2^32个整数值中的一个。

6. 初始化 argList 为一个空列表。

7. 初始化 index 为 0。

8. 循环迭代取出argArray。重复循环 while（index 1. 将下标转换成String类型。初始化 indexName 为 ToString(index).

   > 1. 定义 nextArg 为 使用 indexName 作为参数调用argArray的[[Get]]内部方法的结果。
   > 2. 将 nextArg 添加到 argList 中，作为最后一个元素。
   > 3. 设置 index ＝ index＋1 。

9. 返回调用func的[[Call]]内部方法的结果，提供thisArg作为该值，argList作为参数列表。

```
Function.prototype.call (thisArg [ , arg1 [ , arg2, … ] ] )
```

1. 如果 IsCallable（Function）为false，即Function不可以被调用，则抛出一个TypeError异常。

2. 定义argList 为一个空列表。

3. 如果使用超过一个参数调用此方法，则以从arg1开始的从左到右的顺序将每个参数附加为argList的最后一个元素

4. 返回调用func的[[Call]]内部方法的结果，提供thisArg作为该值，argList作为参数列表。

   

实现call

```js
        Function.prototype.myCall = function(context=window,...args){
            // 防止属性冲突
            let fn = Symbol()
            // 添加方法
            context[fn] = this
            // 执行
            let result = context[fn](...args)
            // 删除
            delete context[fn]
            return result
        }
```

实现apply

```js
        Function.prototype.myApply = function (context = window, arr) {
            // 防止属性冲突
            let fn = Symbol()
            // 添加方法
            context[fn] = this
            // 执行
            let result = context[fn](...arr)
            // 删除
            delete context[fn]
            return result
        }
```



#### promise的原理？手写

#### 模拟实现一个 Promise.finally

#### 介绍下 Promise.all 使用、原理实现及错误处理

#### 设计并实现 Promise.race()

#### 如何实现一个 new

#### 使用迭代的方式实现 flatten 函数。

#### 实现一个 sleep 函数

> 比如 sleep(1000) 意味着等待1000毫秒，可从 Promise、Generator、Async/Await 等角度实现

#### 模拟实现一个深拷贝，并考虑对象相互引用以及 Symbol 拷贝的情况

#### 模拟实现一个 localStorage

#### 模拟 localStorage 时如何实现过期时间功能

#### 手写Object.freeze

