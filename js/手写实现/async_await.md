# 实现async/await



### 思路

生成器





### 实现

```js
      const getData = () =>
        new Promise(resolve => {
          setTimeout(() => {
            resolve("ppp");
          }, 1000);
        });
      // const getData = () => "ppp";

      function asyncFn(fn) {
        let gen = fn();

        function next(data) {
          let result = gen.next(data);
          if (result.done) return result.value;
          if (result.value instanceof Promise) {
            result.value.then(_data => {
              next(_data);
            });
          } else {
            next(result.value);
          }
        }
        next();
      }

      function* fn() {
        let msg = yield getData();
        console.log(msg);
        return msg;
      }

      asyncFn(fn);
```

