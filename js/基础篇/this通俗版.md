4种方式调用一个函数

- 作为一个函数(function)——skulk()，直接被调用。

  > 非严格模式：window，严格模式：undefined

- 作为一个方法(method)——ninja.skulk()，关联在一个对象上，实现面向对象编程。

  > 该对象会成为函数的上下文

- 作为一个构造函数(constructor)——new Ninja()，实例化一个新的对象。

  > 新创建的对象

- 通过函数的apply或者call方法——skulk.apply(ninja)或者skulk.call(ninja)。

  > 显式绑定



另外：箭头函数

箭头函数没有单独的this值。箭头函数的this与声明所在的上下文的相同。































