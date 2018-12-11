# microtask 和 macrotask 的区别是什么？

[HTML系列：macrotask 和 microtask](https://zhuanlan.zhihu.com/p/24460769) ，杨健 | 知乎，2016/12/20

浏览器的 event loop 至少包含两个队列，macrotask 队列和 microtask 队列。

macrotask 包含生成 DOM 对象、解析 HTML、执行主线程 js 代码、更改当前 URL 等。在浏览器看来，macrotask 代表离散独立的工作。

microtask 包含 promise 回调和 DOM 的修改，这些任务在浏览器重渲染前执行。microtask 避免了不必要的 UI 渲染。

> event loop 在 HTML 规范定义，而非 ECMAScript 规范。

event loop 基于两个基本原则：

1. 同一时间只能执行一个任务
2. 任务一直执行到完成，不能被其他任务抢断

在单次迭代中，event loop 首先检查 macrotask 队列，如果有一个 macrotask 等待执行，那么执行该任务。当该任务执行完毕后（或 macrotask 队列为空），event loop 继续执行 microtask 队列。如果 microtask 队列有等待执行的任务，event loop 就一直取出任务，直到 microtask 为空。

注意，macrotask 和 microtask 不同之处：单次 event loop 中，最多执行一个 macrotask（其他的仍然驻留在队列中），然而却可以处理完所有的 microtask。

当 microtask 队列为空时，event loop 检查是否需要执行 UI 重绘，如果需要则重新渲染 UI，从而结束本次渲染。然后从头开始检查 macrotask 队列。

event loop 有以下细节：

- 两个 task 队列都在 event loop 外，任务添加和任务处理行为分离。在 event loop 内负责执行任务（并从队列里删除），而在 event loop 外添加任务。
- 两种类型的 task 同时只能执行一个，因为 JavaScript 基于单线程模型。

[stackoverflow](https://stackoverflow.com/questions/25915634/difference-between-microtask-and-macrotask-within-an-event-loop-context)

[setImmediate.js](https://github.com/YuzuJS/setImmediate#macrotasks-and-microtasks)

[Tasks, microtasks, queues and schedules](https://jakearchibald.com/2015/tasks-microtasks-queues-and-schedules/), by *Jake Archibald*, 2015/08/17

TODO