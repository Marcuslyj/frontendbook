```js
setInterval(()=>{
    // ...
},10)
```

后台线程在相应时间点，把事件添加到事件队列

如，10ms、20ms、30ms、40ms...



如果interval事件触发，并且***队列中***已经有对应的任务等待执行时，则不会再添加新任务。

注意，如果上一个interval操作的耗时任务还没执行结束，还是会添加到队列里边，因为上一个interval事件已经从队列取出（执行中），队列里边没有等待中的interval事件。





浏览器测试

谷歌浏览器是准确的时间点添加事件

火狐浏览器则是与上一个事件间隔相应的间隔事件，导致时间偏离越来越大（轨迹像，添加1事件后的，x时间间隔添加2事件，settime）





That's because [Chrome's implementation of `setInterval`](https://cs.chromium.org/chromium/src/third_party/WebKit/Source/platform/Timer.cpp?rcl=e6d900fb6ed08dbd3a048899f38962ee75f4d8d0&l=162) does correct the drift between each call. So instead of blindly calling again `setTimeout(fn, 250)` at the end （end还是begin？）of the interval's callback, it actually does `setTimeout(fn, max(now - 250, 0))`.







实现一个准确的setInterval（修正时间）



```js
    function mySetInterval(fn, time) {
      let count = 0;
      let startTime = new Date().getTime();

      function fix() {
        count++;
        let accurate = startTime + count * time;
        let nextTime = Math.max(accurate - new Date().getTime(), 0);
        setTimeout(()=>{
            fix();
            fn();
        }, nextTime)
      }
      fix()
    }
```







