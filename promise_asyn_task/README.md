promise 的使用思路：

何时使用 promise？
需要封装一系列有先后次序的任务时，用到 promise，通常是一些异步任务。无论是同步任务，还是异步任务，promise 中调用 resolve 之前都有一定的时间，要么是机器执行同步代码消耗的时间，要么是响应到了消耗的时间。
总结：使用 promise ---> 解决传统回调的回调地狱问题

promise 如何解决回调地狱的？
传统的回调如果要在耗时完成之后再执行一些耗时操作，只能在回调中写其他耗时操作，导致回调中写回调，表示，一些操作发生在回调执行之后。而 promise 的 resolve 和 reject 机制将这些原本发生在回调中的操作体分离到 then 中，当耗时任务执行完毕后，通过 resolve 执行后续的操作。由于 promise 结构有天生的扁平化特性，所以用 promise 封装的任何操作都不会再发生回调地狱，就是因为它的 resolve 和 then 的分离效果。
总结：promise 能解决回调地狱 ---> 因为 resolve 的分离作用

何时用 function 封装 promise？
不立马启动任务，而是在调用函数时启动任务
多处要用到同一个任务
总结：function return promise ---> 该 promise 封装的任务在多处需要调用，并且启动任务的时机延迟到在调用函数的时候

如何理解 new Promise？
new Promise 体中的代码实际上觉得了 Promise 何时变成 resolved，可以理解为：当 new Promise 封装的任务完成后，promise 变 resolved。
比如一个 new promise 封装了网络请求，那么其整体含义就是，当网络请求完成时，promise 变 resolved。而 promise 何时变 resolved 又决定了后续的 then 回调何时被抛如队列被执行。
总结：new Promise ---> 封装一个任务，任务结束时，promise 变 resolved
