## setState更新同步异步问题

脱离了React的控制，React不知道如何进行Batch Update，setState()就会是**同步**的。

回调函数可以获取最新值。

 settimeout等是同步更新



## 通讯

1.父—>子：使用props
2.子—>父：使用props回调
3.兄弟组件通信：层层传递props；发布者订阅者模式
4.非嵌套组件间通信：发布者订阅者模式；redux











































