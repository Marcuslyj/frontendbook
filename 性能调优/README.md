##### 为什么 for 循环嵌套顺序会影响性能？

> ```js
> var t1 = new Date().getTime()
> for (let i = 0; i < 100; i++) {
>   for (let j = 0; j < 1000; j++) {
>     for (let k = 0; k < 10000; k++) {
>     }
>   }
> }
> var t2 = new Date().getTime()
> console.log('first time', t2 - t1)
> 
> for (let i = 0; i < 10000; i++) {
>   for (let j = 0; j < 1000; j++) {
>     for (let k = 0; k < 100; k++) {
> 
>     }
>   }
> }
> var t3 = new Date().getTime()
> console.log('two time', t3 - t2)
> ```

