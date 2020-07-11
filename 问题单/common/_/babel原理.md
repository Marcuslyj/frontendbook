# Babel原理



## Babel的包构成

#### 核心包

- babel-core：babel转译器本身，提供了babel的转译API，如babel.transform等，用于对代码进行转译。像webpack的babel-loader就是调用这些API来完成转译过程的。
- babylon：js的词法解析器
- babel-traverse：用于对AST（抽象语法树，想了解的请自行查询编译原理）的遍历，主要给plugin用
- babel-generator：根据AST生成代码



## babel的工作原理

babel是一个转译器，感觉相对于编译器compiler，叫转译器transpiler更准确，因为它只是把同种语言的高版本规则翻译成低版本规则，而不像编译器那样，输出的是另一种更低级的语言代码。
 但是和编译器类似，babel的转译过程也分为三个阶段：**parsing、transforming、generating**，以ES6代码转译为ES5代码为例，babel转译的具体过程如下：

1. ES6代码输入
2. babylon进行解析，得到AST
3. plugin用babel-traverse对AST树进行遍历转译，得到新的AST树
4. 用babel-generator通过AST树生成ES5代码

此外，还要注意很重要的一点就是，babel只是转译新标准引入的语法，比如ES6的箭头函数转译成ES5的函数；而**新标准引入的新的原生对象，部分原生对象新增的原型方法，新增的API等（如Proxy、Set等），这些babel是不会转译的。需要用户自行引入polyfill来解决**



