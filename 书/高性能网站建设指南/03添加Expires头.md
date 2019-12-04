使用缓存来较少http请求的数量，斌个减少http响应的大小。



expires在有效期就直接不请求http了？





expires绝对时间，b/s时间差问题

cache-control（http1.1） max-age  缓存多久，秒为单位

> 服务端响应设置的？
>
> 客户端设置，那不是很难管理？if-modified-since之类的，怎么设置？



expires和cache-control max-age同时出现，http规范规定max-age指令将重写expires头。





更新时，修订文件名以避免使用缓存





如果一个组件没有长久的expires头，他仍然会存储在浏览器的缓存中。在后续的请求中，浏览器会检查缓存并发现组件已经过期。为提高效率，浏览器会想原始服务器发送get请求，如果组件没变，服务器只是发送一个很小的头，告诉浏览器可以使用缓存。







































