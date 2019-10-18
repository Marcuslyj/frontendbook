





## 介绍下 webpack 热更新原理，是如何做到在不刷新浏览器的前提下更新页面的

1.当修改了一个或多个文件；
2.文件系统接收更改并通知webpack；
3.webpack重新编译构建一个或多个模块，并通知HMR服务器进行更新；
4.HMR Server 使用webSocket通知HMR runtime 需要更新，HMR运行时通过HTTP请求更新jsonp；
5.HMR运行时替换更新中的模块，如果确定这些模块无法更新，则触发整个页面刷新。





## 页面打开速度

几个方面：加载文件的体积小，加载文件的速度快、减少需要加载的文件加载、提前加载、js执行速度

#### 加载文件的体积小

代码压缩：普通压缩（去除空格等）+gzip

代码分割，按需加载（路由懒加载、动态import），基础库分离，提取公用代码

加载文件的速度快

擦除无用代码：treeshaking擦除无用js，    擦除无用的css

ScopeHoisting（减少大量闭包，减少体积，还能减少内存开销，提升性能）

#### 加载文件的速度快（网络和服务器响应速度）

cdn

gzip文件由前端项目构建生成，减少服务器操作

#### 减少需要加载的文件加载

缓存（文件指纹，基础库分离、提取公用代码以方便复用）

资源内联（图标字体等base64）

#### 提前加载

prefetch

prerender？

#### js执行速度

scopehoisting

#### 其他

ssr（减少白屏时间，seo友好）







#### webpack 打包 vue 速度太慢怎么办？

#### 打包优化



#### 打包体积更小？

公共资源分离（基础库分离）



构建速读更快？



## webpack针对不同环境的打包策略？

#### development

- 热更新配置

- sourcemap，方便调试定位代码

#### production

- 代码压缩
  - html（html-webpack-plugin的minify参数）
  - css（optimize-css-assets-webpack-plugin+cssnano）
  - js（内置uglifyjs-webpack-plugin插件，默认开启））
- 文件指纹
- treeshaking
- scope hoisting
- 速度优化
  - 基础包cdn
- 体积优化
  - 代码分割

#### 基础配置

- 资源解析（es6、jsx、ts等语法、css、less、图片、字体）
- 样式增强（css前缀补全、pxtorem）
- css提取独立文件
- 构建目录清理
- 多页面打包

- 优化构建命令行打印信息：stats配置项；friendly-errors-webpack-plugin（增加高亮提示）

- 错误捕获和处理

  构建是否成功：echo $? 获取错误码；

  compiler在每次构建结束后会触发done这个hook

  process.exist 主动抛错误码

  可以上报构建日志

- 

#### SSR

- output的libraryTarget设置
- css解析ignore



## 构建速度分析

speed-measure-webpack-plugin

- 分析整个打包总耗时
- 每个loader和插件执行耗时



## 构建速度优化

- 使用高版本webpack+node

- 多进程多实例构建

  thread-loader：打包任务划分成多个进程

- 多进程多实例，并行压缩

  方法1： parallel-uglify-plugin

  方法2：

  方法3：



## 体积分析

webpack-bundle-analyzer

- 依赖的第三方文件大小
- 业务里的组件代码大小







# vue 如何优化首页的加载速度？vue 首页白屏是什么问题引起的？如何解决呢？

首页白屏的原因：
单页面应用的 html 是靠 js 生成，因为首屏需要加载很大的js文件(`app.js` `vendor.js`)，所以当网速差的时候会产生一定程度的白屏



体积更小，网络更快，减少加载，提前加载



解决办法：

1. 优化 webpack 减少模块打包体积（查看每个模块的体积大小，是否可以优化），code-split 按需加载（路由懒加载），去掉dead code
2. 服务端渲染，在服务端事先拼装好首页所需的 html
3. 首页加 loading 或 骨架屏 （仅仅是优化体验）
4. 服务端开启gzip压缩，（前端项目打包可以直接打包出gzip，减少服务器工作量）
5. 提取公共代码包
6. cdn
7. 合理使用resource hint，即preload，prefetch, dns-connect等
8. 缓存（文件指纹）
9. 图片方面，像淘宝，会优先使用webp，如果不支持再用jpg，以及，小图采用base64编码，雪碧图等



# vue 渲染大量数据时应该怎么优化

按需加载局部数据, 虚拟列表，无限下拉刷新

运行异步处理:分割任务

大量纯展示的数据,不需要追踪变化的 用object.freeze冻结

分页处理







