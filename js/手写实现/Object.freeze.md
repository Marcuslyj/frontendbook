# 实现Object.freeze



### 属性描述符

- writable

  writable 决定是否可以修改属性的值。（设置可逆）

- configurable

  属性值true，才可以使用 defineProperty(..) 方法来修改属性描述符。
  属性值false，属性不能delete（false设置不可逆）。

- enumerable

  for...in



### 禁止扩展

Object.prevent Extensions



### Object.seal()

创建一个密封对象。禁止扩展、删除、修改描述符。属性值可修改。

实际是Object.preventExtensions()+configurable:false。

```js
function seal(obj) {
    for (let key in obj) {
        Object.defineProperty(obj, key, {
            configurable: false,
            writable: true
        })
    }
    Object.preventExtensions(obj)
    return obj
}
```



### Object.free()

Object.seal() + writable: false

```js
function freeze(obj) {
    for (let key in obj) {
        Object.defineProperty(obj, key, {
            configurable: false,
            writable: false
        })
    }
    Object.preventExtensions(obj)
    return obj
}
```



