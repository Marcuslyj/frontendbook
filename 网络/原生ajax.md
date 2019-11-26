get方式

```js
export function get(url) {
    // 创建XMLHttpRequest对象
    let xhr = new XMLHttpRequest();
    // 编写回调函数
    xhr.onreadystatechange = function () {
        if (xhr.readyState === 4 && xhr.status === 200) {
            console.log(xhr.responseText)
        }
    }
    // 设置请求方法和请求路径(异步)
    xhr.open('get', url, true)
    // 发送
    xhr.send()
}
```

post

```js
export function post(url, data) {
    // 创建XMLHttpRequest对象
    let xhr = new XMLHttpRequest();
    // 编写回调函数
    xhr.onreadystatechange = function () {
        if (xhr.readyState === 4 && xhr.status === 200) {
            console.log(xhr.responseText)
        }
    }
    // 设置请求方法和请求路径
    xhr.open('post', url, true)
    // 这是请求头
    xhr.setRequestHeader('content-type', 'application/x-www-form-urlencoded');
    // 发送
    xhr.send("username=" + data.userval + "&age=" + data.ageval + "&timp" + new Date().getTime());
}
```







- `application/x-www-form-urlencoded`: 表示使用URL编码的方式来编码表单。如果没有将`enctype`属性设置为任何值，那么这就是**默认值**。
- `multipart/form-data`: 当用户想上传文件这种二进制等文件或者前面的那个方式不能满足时，使用这种类型的表单
- `text/plain`: 文本形式，只发送数据而不进行任何编码时使用。