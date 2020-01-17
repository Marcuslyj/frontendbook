setTimeout throw 的error不能catch？



stack 解答

https://stackoverflow.com/questions/48969591/why-promise-can-not-catch-the-error-throw-by-settimeout



To understand why you cannot just throw an error from within the callback of `setTimeout` you need to understand a few concepts.

## The Stack

As a program is running information is stored in a data structure called the stack. When a method is called information is stored on the stack until the method returns. Since methods generally contain calls to other methods the stack grows and shrinks until all the methods have returned (this is generally the end of the program). When an error is thrown it is passed down the stack of function calls that have yet to return until it is caught and handled, or reaches the "main" method, which generally causes the program to crash.

## The Event Loop

The event loop is what powers the asynchronous functionality in Javascript. When `setTimeout` or any other asynchronous method is called the callback is placed in a queue called the event loop. As the javascript runtime executes the program and reaches the end of the stack (e.g. all methods have returned) instead of merely exiting the program it first looks to see if there is anything in the event loop, if there is it begins executing it causing the stack to grow and shrink once more. When there is nothing left in the event loop, and the stack is empty then the program is free to exit.

------

This means that when you call `setTimeout` the callback that is passed into the method ends up being executed in a different stack frame. This means that it is impossible for the error to be thrown down the stack and be caught by the promise, because the stack the promise was created in has already finished executing and is no more.

I would suggest watching this video on the topic, it goes into great detail and helps you visualize what is going on: [What the heck is the event loop anyway?](https://www.youtube.com/watch?v=8aGhZQkoFbQ)

