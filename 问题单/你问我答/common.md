> 说一下浏览器缓存

浏览器缓存分为**强缓存**和**协商缓存**，强缓存会直接从浏览器里面拿数据，协商缓存会先访问服务器看缓存是否过期，再决定是否从浏览器里面拿数据。

控制强缓存的字段有：Expires 和 Cache-Control。

控制协商缓存的字段是：Last-Modified / If-Modified-Since 和 Etag / If-None-Match，其中 Etag / If-None-Match 的优先级比 Last-Modified / If-Modified-Since 高。

> cookie 与 session 的区别



