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



简单版

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



#### promiseA+规范

```js
// 三种状态
const PENDING = Symbol('PENDING')
const FULFILLED = Symbol('FULFILLED')
const REJECTED = Symbol('REJECTED')

export default class MyPromise {
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
                this.onResolvedCallbacks.forEach(fn => fn())
            }
        }
        // 失败
        let reject = reason => {
            if (this.state === PENDING) {
                this.state = REJECTED
                // 存储失败原因
                this.reason = reason
                this.onRejectedCallbacks.forEach(fn => fn())
            }
        }

        try {
            executor(resolve, reject)
        } catch (err) {
            reject(err)
        }
    }
    // then方法,返回promise以处理链式then
    then(onFulfilled, onRejected) {
        // 规范化传参
        onFulfilled = typeof onFulfilled === 'function' ? onFulfilled : v => v
        onRejected = typeof onRejected === 'function' ? onRejected : err => { throw err }

        let promise2 = new MyPromise((resolve, reject) => {
            // executor已经执行成功
            if (this.state === FULFILLED) {
                // 异步
                setTimeout(() => {
                    try {
                        let x = onFulfilled(this.value)
                        resolvePromise(promise2, x, resolve, reject)
                    } catch (err) {
                        reject(err)
                    }
                }, 0)
            }
            // executor已经执行失败
            else if (this.state === REJECTED) {
                // 异步
                setTimeout(() => {
                    try {
                        let x = onRejected(this.reason)
                        resolvePromise(promise2, x, resolve, reject)
                    } catch (err) {
                        reject(err)
                    }
                }, 0)
            }
            // executor未执行结束
            else if (this.state === PENDING) {
                // 存起回调函数
                this.onResolvedCallbacks.push(() => {
                    setTimeout(() => {
                        try {
                            let x = onFulfilled(this.value)
                            resolvePromise(promise2, x, resolve, reject)
                        } catch (err) {
                            reject(err)
                        }
                    }, 0)
                })
                this.onRejectedCallbacks.push(() => {
                    setTimeout(() => {
                        try {
                            let x = onRejected(this.reason)
                            resolvePromise(promise2, x, resolve, reject)
                        } catch (err) {
                            reject(err)
                        }

                    }, 0)
                })
            }
        })

        return promise2
    }
}

// 让不同的promise代码互相套用
function resolvePromise(promise2, x, resolve, reject) {
    // 自己等自己完成，循环报错
    if (x === promise2) {
        return reject(new TypeError('chaining cycle detected for promise'))
    }

    // 防止调用多次?
    let called

    if (x != null && (typeof x === 'object' || typeof x === 'function')) {
        try {
            let then = x.then
            // 判断为promise
            if (typeof then === 'function') {
                then.call(x, y => {
                    // 成功与失败只能调用一个
                    if (called) {
                        return
                    }
                    called = true
                    resolvePromise(promise2, y, resolve, reject)
                }, err => {
                    if (called) {
                        return
                    }
                    called = true
                    reject(err)
                })
            } else {
                resolve(x)
            }
        } catch (err) {
            if (called) {
                return
            }
            called = true
            reject(err)
        }

    } else {
        // 普通值
        resolve(x)
    }
}
```





#### Promise.resolve

```js
Promise.resolve = function(val){
  return new Promise((resolve,reject)=>{
    resolve(val)
  });
}
```

#### Promise.reject

```js
Promise.reject = function(val){
  return new Promise((resolve,reject)=>{
    reject(val)
  });
}
```

#### Promise.all

```js
//all方法(获取所有的promise，都执行then，把结果放到数组，一起返回)
Promise.all = function(promises){
  let arr = [];
  let i = 0;
  function processData(index,data){
    arr[index] = data;
    i++;
    if(i == promises.length){
      resolve(arr);
    };
  };
  return new Promise((resolve,reject)=>{
    for(let i=0;i<promises.length;i++){
      promises[i].then(data=>{
        processData(i,data);
      },reject);
    };
  });
}
```

#### Promise.race

```js
Promise.race = function(promises){
  return new Promise((resolve,reject)=>{
    for(let i=0;i<promises.length;i++){
      promises[i].then(resolve,reject)
    };
  })
}
```









