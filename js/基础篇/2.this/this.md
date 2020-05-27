#### this

<https://github.com/mqyqingfeng/Blog/issues/7>

ECMAScript 的类型分为语言类型和规范类型。规范类型，它们的作用是用来描述语言底层行为逻辑。

Reference 类型就是用来解释诸如 delete、typeof 以及赋值等操作行为的。

Reference 的构成，由三个组成部分，分别是：

- base value(*属性所在的对象, 否则就是 EnvironmentRecord*) `EnvironmentRecord我的理解是, 假如这个变量/属性不属于某一对象, 那么他属于某个环境`
- referenced name(*属性的名称*)
- strict reference(*是否严格模式*)

base value 就是属性所在的对象或者就是 EnvironmentRecord，它的值只可能是 undefined, an Object, a Boolean, a String, a Number, or an environment record 其中的一种。



GetBase：返回 reference 的 base value

IsPropertyReference：如果 base value 是一个对象，就返回true

GetValue： 返回对象属性真正的值，***不是reference***



------

##### 确定this的值

1. 计算 MemberExpression 的结果赋值给一个变量 ref (简单理解 MemberExpression 其实就是()左边的部分。)
2. 判断 ref 是不是一个 Reference 类型
3. 结果:

- 若 ref 是 Reference，且 IsPropertyReference(ref) 是 true, 那么 this 的值为 GetBase(ref)
- 若ref是 Reference，且 base 值是 EnvironmentRecord, 那this的值为 ImplicitThisValue(ref)undefined
- 如果 ref 不是 Reference，那么 this 的值为 undefined

------



例子：

```js
var value = 1;

var foo = {
  value: 2,
  bar: function () {
    return this.value;
  }
}

//示例1
console.log(foo.bar()); // 2
//示例2
console.log((foo.bar)()); // 2
//示例3
console.log((foo.bar = foo.bar)()); // 1
//示例4
console.log((false || foo.bar)()); // 1
//示例5
console.log((foo.bar, foo.bar)()); // 1
```

**示例1：**

```js
var Reference = {
  base: foo,
  name: 'bar',
  strict: false
};
```

1. 是reference

2. IsPropertyReference 方法，如果 base value 是一个对象，结果返回 true
3. getValue，this指向foo

**示例2：**

foo.bar 被 () 包住，查看规范 11.1.6 The Grouping Operator

直接看结果部分：

> Return the result of evaluating Expression. This may be of type Reference.

> NOTE This algorithm does not apply GetValue to the result of evaluating Expression.

实际上 () 并没有对 MemberExpression 进行计算，所以其实跟示例 1 的结果是一样的。

**示例3：**

有赋值操作符，查看规范 11.13.1 Simple Assignment ( = ):

计算的第三步：

> 3.Let rval be GetValue(rref).

因为使用了 GetValue，所以返回的值不是 Reference 类型，this是undefined，非严格模式下指向window

**示例4：**

逻辑与算法，查看规范 11.11 Binary Logical Operators：

计算第二步：

> 2.Let lval be GetValue(lref).

因为使用了 GetValue，所以返回的不是 Reference 类型，this 为 undefined

**示例5：**

逗号操作符，查看规范11.14 Comma Operator ( , )

计算第二步：

> 2.Call GetValue(lref).

因为使用了 GetValue，所以返回的不是 Reference 类型，this 为 undefined





