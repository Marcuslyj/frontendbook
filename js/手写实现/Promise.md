## promisify

将 callback 语法的 API 改造成 Promise 语法

```js
function promisify(original) {
    return function (...args) {
        return new Promise((resolve, reject) => {
            args.push(function callback(err, ...values) {
                if (err) {
                    return reject(err);
                }
                return resolve(...values)
            });
            original.call(this, ...args);
        });
    };
}
```



## 手写promise

#### promise规范

Promise存在三个状态（state）pending、fulfilled、rejected

pending（等待态）为初始态，并可以转化为fulfilled（成功态）和rejected（失败态）

成功时，不可转为其他状态，且必须有一个不可改变的值（value）

失败时，不可转为其他状态，且必须有一个不可改变的原因（reason）



#### 简单版

1. 三种状态，成功值，失败原因
2. resolve、reject函数实现
3. then函数

```js
class MyPromise {
    // 三种状态
    const PENDING = symbol('PENDING')
    const FULFILLED = symbol('FULFILLED')
    const REJECTED = symbol('REJECTED')

    constructor(executor) {
        // 初始状态
        this.state = PENDING
        // 成功的值
        this.value = undefined
        // 失败原因
        this.reason = undefined

        // 处理一个promise对应多个then
        // 成功callbacks
        this.onResolvedCallbacks = []
        // 失败 callbacks
        this.onRejectedCallbacks = []

        // 成功
        let resolve = value => {
            // 修改状态
            if (this.state === PENDING) {
                this.state = FULFILLED
                // 存储成功值
                this.value = value
                // 执行成功callbacks  
                this.onRejectedCallbacks.forEach(fn => fn(this.value))))
            }
        }
        // 失败
        let reject = reason => {
            if (this.state === PENDING) {
                this.state = REJECTED
                // 存储失败原因
                this.reason = reason
                this.onRejectedCallbacks.forEach(fn => fn(this.value))
            }
        }

        try {
            executor(resolve, reject)
        } catch (err) {
            reject(err)
        }
    }
    // then方法
    then(onFulfilled, onRejected) {
        // 规范化传参
        onFulfilled = typeof onFulfilled === 'function' ? onFulfilled : v => v
        onRejected = typeof onRejected === 'function' ? onRejected : err => { throw err }

        // executor已经执行成功
        if (this.state === FULFILLED) {
            onFulfilled(this.value)
        }
        // executor已经执行失败
        if (this.state === REJECTED) {
            onrejected(this.reason)
        }
        // executor未执行结束
        if (this.state === PENDING) {
            // 存起回调函数
            this.onRejectedCallbacks.push(onFulfilled)
            this.onRejectedCallbacks.push(onRejected)
        }
    }
}
```



























