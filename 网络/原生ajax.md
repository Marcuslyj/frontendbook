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

