## cdn

> 是什么

- Content Delivery Network，即内容分发网络。
- 各地部署多套静态存储服务，本质上是空间换时间
- 自动选择最近的节点内容，不存在再请求原始服务器
- 适合存储更新很少的静态内容，文件更新慢（更新文件可修改文件名，使用hash等）

***举个栗子***

你，要喝水，每次都要去水房里接水喝，你觉得很麻烦，所以你就选择了水壶去装水，这样就不用每一次都要去水房接水，就可以选择最近的水壶进行接水。

> 为什么（优势）

- 本地Cache加速，提高了企业站点（尤其h含有大量图片和静态页面站点）的**访问速度**
- 跨运营商的网络加速，保证不同网络的用户都得到良好的访问质量
- 远程访问用户根据DNS负载均衡技术智能自动选择Cache服务器
- 自动生成服务器的远程Mirror（镜像）cache服务器，远程用户访问时从cache服务器上读取数据，**减少远程访问的带宽、分担网络流量、减轻原站点web服务器负载等功能**
- 广泛分布的CDN节点加上节点之间的智能冗余机制，可以有效地预防黑客入侵。

