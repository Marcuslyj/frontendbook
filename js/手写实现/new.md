# new

### new做了什么

1. A new object is created in memory.
2. The new object’s internal [[Prototype]] pointer is assigned to the constructor’s prototype property.
3. The this value of the constructor is assigned to the new object (so this points to the new object).
4. The code inside the constructor is executed (adds properties to the new object).
5. If the constructor function returns a non-null value, that object is returned. Otherwise, the new object that was just created is returned.



### 实现一个new

```js
function myNew(Ctr, ...args) {
    // 1.创建一个对象
    // 2.对象原型指向构造函数原型
    let o = Object.create(Ctr.prototype);
    // 3.this指向对象
    // 4.执行构造函数
    let res = Ctr.call(o, ...args);
    // 返回
    return (res && typeof res === 'object') ? res : o
}
```

