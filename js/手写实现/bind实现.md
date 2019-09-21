bind要做什么？

- 返回一个函数，绑定this，传递预置参数
- bind返回的函数可以作为构造函数使用。故作为构造函数时应使得this失效，但是传入的参数依然有效



```js
Function.prototype.myBind = function (context) {
    // bind需要function来调用
    if (typeof this !== "function") {
        throw new Error("应该function调用");
    }
    let self = this
    // 获取预设参数
    let args = Array.prototype.slice.call(arguments, 1)
    // 返回的函数
    let fBound = function () {
        let bindArgs = Array.from(arguments)
        // new 的时候，this指向实例，否则，指向传入对象
        return self.apply(
            this instanceof fBound ? this : context, args.concat(bindArgs)
        )
    }

    // 原型维护,
    // 不直接指向this.prototype，
    // 防止修改fBound.prototype时直接修改到绑定函数的prototype
    fBound.prototype = Object.create(this.prototype)

    return fBound
}
```

