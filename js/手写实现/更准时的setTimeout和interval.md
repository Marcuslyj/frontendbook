## requestAnimationFrame+promise

chrome测试并不能准时（测试结果像settimeout一样处理，放进队列的），引入promise是想提高优先级

firefox符合

```js
    function timer(fn, timeout) {
      let task = {
        time: new Date().getTime() + timeout,
        fn
      }

      function executor(fn, time) {
        window.requestAnimationFrame(function () {
          if (new Date().getTime() >= time) {
            // Promise.resolve().then(fn)
              fn()
          } else {
            executor(fn, time)
          }
        })
      }

      executor(task.fn, task.time)
    }
```

