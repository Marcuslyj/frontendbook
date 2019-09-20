#### 什么是防抖和节流？有什么区别？如何实现？



#### promise的原理？手写

#### 模拟实现一个 Promise.finally

#### 介绍下 Promise.all 使用、原理实现及错误处理

#### 设计并实现 Promise.race()

#### 如何实现一个 new

new做了什么？

- 它创建了一个全新的对象
- 将构造函数的作用域赋给新对象（因此 this 就指向了这个新对象）；
- 执行构造函数中的代码（为这个新对象添加属性）；
- 返回新对象。如果函数没有返回对象类型Object(包含Functoin, Array, Date, RegExg, Error)，那么new表达式中的函数调用将返回该对象引用



实现

```js
function objectFactory() {
    // 创建新对象
    const obj = new Object()
    // 取出构造函数
    const Constructor = [].shift.call(arguments)
    // 修改原型指向
    obj.__proto__ = Constructor.prototype
    // 执行构造函数
    const ret = Constructor.apply(obj, arguments)
    // 若构造函数返回对象，则返回该对象
    return ret !== null && (typeof ret === 'object' || typeof ret === 'function') ? ret : obj
}
```



#### 使用迭代的方式实现 flatten 函数。

#### 实现一个 sleep 函数

> 比如 sleep(1000) 意味着等待1000毫秒，可从 Promise、Generator、Async/Await 等角度实现

#### 模拟实现一个深拷贝，并考虑对象相互引用以及 Symbol 拷贝的情况

#### 模拟实现一个 localStorage

#### 模拟 localStorage 时如何实现过期时间功能

#### 手写Object.freeze

#### 代码模拟实现事件循环

#### a与a.b与a.b.c这种多重与访问，简化（判空麻烦，使用代理自动填充属性）

```js
let obj = {
    a: {
        b: {
            c: {
                d: 'hhefie'
            }
        }
    }
}
function Folder(obj) {
    return new Proxy(obj ? obj : {}, {
        get: (target, property) => {
            if (!(property in target)) {
                target[property] = new Folder()
            }

            return target[property]
        }
    })
}
let fo = new Folder(obj)
```

