# window.requestAnimationFrame()

**`window.requestAnimationFrame()`** 告诉浏览器——你希望执行一个动画，并且要求浏览器在下次重绘之前调用指定的回调函数更新动画。该方法需要传入一个回调函数作为参数，该回调函数会在浏览器下一次重绘之前执行。

为了提高性能和电池寿命，因此在大多数浏览器里，当`requestAnimationFrame()` 运行在后台标签页或者隐藏的<iframe>里时，`requestAnimationFrame()` 会被暂停调用以提升性能和电池寿命。

（实际上 FireFox/Chrome 浏览器对定时器做了优化：页面闲置时，如果时间间隔小于 1000ms，则停止定时器，与`requestAnimationFrame`行为类似。如果时间间隔>=1000ms，定时器依然在后台执行）





- 是属于微任务？

  The spec now says when this happens in the [*Event Loop Processing Model*](https://html.spec.whatwg.org/multipage/webappapis.html#event-loop-processing-model) section. The shortened version with a lot of detail removed is:

  1. Do the oldest (macro) task
  2. Do microtasks
  3. If this is a good time to render:
     1. Do some prep work
     2. Run `requestAnimationFrame` callbacks
     3. Render

- 执行耗时任务会怎样？

  耗时任务会降频

- 准时？

  js阻塞渲染，所以也不是准时的，但是与settimeout相比会准时些。

