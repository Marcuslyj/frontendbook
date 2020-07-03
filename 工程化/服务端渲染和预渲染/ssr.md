## vue-server-renderer



## ssr分类

### 混合模式

服务端和客户端有不同的工作。

- entry.client.js 	

$mount，实际是激活，使得页面可交互。html结构server端已经返回，没必要销毁重建。只需要激活。

- entry.server.js	

创建url匹配组件，并返回。



## 效果

请求页面，返回的html已经包含页面需要展示的dom结构。实现页面还没初始化就可以看到页面内容，此时页面还不能交互，但是内容可见，客户端只需要做激活工作。



实际上就是网页应用，打开的第一个页面（不管是哪个url）是ssr。



## 页面数据提前获取

分为服务端预取和客户端预取。

### 服务端预取

vue组件，定义asyncData，ssr返回前，执行获取数据，并把数据设置到`window.__INITIAL_STATE__`，client side激活时把数据取出到vuex store，页面便初始化完成。







## 小结

- Each request should have a fresh & isolated app instance.

  no cross-request state pollution

- Pre-fetch data on the server

  app state resolved when we start rendering

- SSR lifecycle hooks: beforeCreate & created

  avoid starting timers in these hooks to avoid memory leaks.

- Avoid Platform-Specific APIs

  window does not exist on the server-side. module does not exist on the client-side. etc.

