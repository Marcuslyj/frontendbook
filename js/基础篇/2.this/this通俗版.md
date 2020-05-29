# this

### 定义

this 是在运行时进行绑定的，并不是在编写时绑定，它的上下文取决于函数调用时的各种条件。

当一个函数被调用时，会创建一个活动记录（有时候也称为执行上下文）。这个记录会包含函数在哪里被调用（调用栈）、函数的调用方法、传入的参数等信息。this 就是记录的 其中一个属性，会在函数执行的过程中用到。



### this绑定规则（4种方式调用）

- 默认绑定：指向全局对象（window），严格模式指向undefined。

  作为一个函数(function)——skulk()，直接被调用。

- 隐式绑定：谁调用指向谁

  作为一个方法(method)——ninja.skulk()，关联在一个对象上，实现面向对象编程。

- 显示绑定

  通过函数的apply或者call方法——skulk.apply(ninja)或者skulk.call(ninja)。

- new

  作为一个构造函数(constructor)——new Ninja()，实例化一个新的对象。

  

### 箭头函数

箭头函数不使用 this 的四种标准规则，而是根据外层（函数或者全局）作用域来决 定 this。

```js
// 硬绑定，后面如何调用，this指向都不会改变
function bind(fn, obj) {
	return function() {
        return fn.apply( obj, arguments ); 
    }; 
}
```



### new 做了什么

1. A new object is created in memory.创建对象
2. The new object’s internal [[Prototype]] pointer is assigned to the constructor’s prototype property.原型连接
3. The this value of the constructor is assigned to the new object (so this points to the new object).构造函数的this指向创建对象
4. The code inside the constructor is executed (adds properties to the new object).执行构造函数
5. If the constructor function returns a non-null value, that object is returned. Otherwise, the new object that was just created is returned.返回对象



### 优先级

new >>  过 call、apply（显式绑定）或者硬绑定 >> 隐式绑定 >> 默认绑定

























