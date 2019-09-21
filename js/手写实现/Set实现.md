## Set特性

- 本身是构造函数（不能当方法调用）
- 操作方法：
  - add
  - delete
  - has
  - clear
- 遍历方法
  - keys()：返回键名的遍历器
  - values()：返回键值的遍历器
  - entries()：返回键值对的遍历器
  - forEach()：使用回调函数遍历每个成员，无返回值
- 属性：
  - Set.prototype.constructor：构造函数，默认就是 Set 函数。
  - Set.prototype.size：返回 Set 实例的成员总数。



```js
// 特殊处理NaN
let NaNSymbol = Symbol('NaN')
let encodeVal = function (value) {
    return value !== value ? NaNSymbol : value;
}
let decodeVal = function (value) {
    return (value === NaNSymbol) ? NaN : value;
}

function MySet(data) {
    // 需要new
    if (!(this instanceof MySet)) {
        throw new Error("Constructor Set requires 'new'")
    }
    // 数据存储
    this._values = []
    // 实现size
    Object.defineProperty(this, 'size', {
        get() {
            return this._values.length
        }
    })

    // 初始化数据,数据要求可遍历的
    if (data) {
        for (let item of data) {
            this.add(item)
        }
    }
    // 实例实现可遍历
    Set.prototype[Symbol.iterator] = function () {
        return this.values();
    }
}
// 操作方法
MySet.prototype.add = function (value) {
    value = encodeVal(value)
    if (this._values.indexOf(value) === -1) {
        this._values.push(value)
    }
    return this
}
MySet.prototype.has = function (value) {
    return this._values.indexOf(encodeVal(value)) !== -1
}
MySet.prototype.clear = function () {
    this._values = []
}
MySet.prototype.delete = function (value) {
    let i = this._values.indexOf(encodeVal(value))
    if (i === -1) {
        return false
    }
    this._values.splice(i, 1)
    return true
}
MySet.prototype.forEach = function (cb, thisArg = window) {
    for (let i = 0; i < this._values.length; i++) {
        cb.call(thisArg, decodeVal(this._values[i]), decodeVal(this._values[i]), this)
    }
}
// 遍历方法（返回迭代器）
MySet.prototype.values = MySet.prototype.keys = function () {
    return (this._values.map(item=>decodeVal(item)))[Symbol.iterator]()
}
// 返回键值对的迭代器
MySet.prototype.entries = function () {
    return (this._values.map(item => [decodeVal(item), decodeVal(item)]))[Symbol.iterator]()
}
```

