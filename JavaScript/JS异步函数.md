# 异步行为

## 回调函数 callback

## Promise

- 生产者代码（producing code）：做一些耗时长的事，不能及时给出工作的结果
- 消费者代码（consuming code）：在生产者代码完成工作的第一时间获得其工作结果
- Promise：将生产者与消费者连接在一起的特殊 JS 对象

```JS
let promise = new Promise(function(resolve, reject) {
  // executor（生产者代码）
});
```

回调：

- `resolve(value)` —— 如果任务成功完成并带有结果 value。
- `reject(error)` —— 如果出现了 error，error 即为 error 对象。

`promise` 对象内部属性：

- `state` —— 最初是 "pending"，然后在 resolve 被调用时变为 "fulfilled"，或者在 reject 被调用时变为 "rejected"。
- `result` —— 最初是 undefined，然后在 resolve(value) 被调用时变为 value，或者在 reject(error) 被调用时变为 error。
- 只能有一个结果或一个 `Error`
- resolved 或 rejected 的 promise 都会被称为 “settled”

### `.then(handlingFunc, errorHandlingFunction)` 与 `.catch`

- 第一个参数是一个将在 promise resolved 且接收到结果后执行的函数。
- 第二个参数也是一个将在 promise rejected 且接收到 error 信息后执行的函数。

- `.catch` 是 `.then(null, errorHandlingFunction)` 的简写（不对执行成功做处理）

### `.finally`

- finally 没有得到前一个处理程序的结果（结果会继续传递）
- finally 返回的内容会被忽略
- 抛出 error，执行将转到最近的 error 的处理程序

## Promise 链

- 每个对 `.then` 的调用都会返回一个新的 Promise，可以继续调用下一个 `.then`
  - 返回具有 `.then` 方法的 “thenable” 对象：实现 promise 兼容

## promise 错误处理

`.catch` 处理 `reject()` 或是在程序中抛出的 `error`，不是立即的（可能在许多个 .then 之后），也不是必须的（附加到链的末尾可以捕获所有 error）

- 隐式的 `try...catch`
  > promise excutor 与 .then 内抛出的错误会作为 rejected promise 被处理。
- promise 错误的再次抛出
  > 与正常的错误一样，再次抛出的错误会在后续的 `.catch` 中被处理
- 未处理的错误
  > 会形成一个全局的 error，可以使用 `unhandledrejection` 捕获（建议在任何情况都使用，用于报告错误、防止程序崩溃）

## Promise API

Promise 类中的 6 种静态方法

- `Promise.all`
  并行执行多个 promise，并等待所有 promise settled，任何 promise 被 reject 则 `Promise.all` 返回的 promise 就会立即 reject，并带有其 error
  - 传入参数为包含 promise 的可迭代对象（如数组）不是 promise 则原样返回，返回与源 promise 顺序相同的数组
- `Promise.allSettled` （新特性）
  等待所有的 promise 都被 settle，无论结果如何（resolve or reject）
  - 对每个 promise 都得到其 status 与 value/reason
- `Promise.race`
  类似于 `Promise.all`，但只返回第一个 settled 的 promise，并获取其 value/error
- `Promise.any`
  类似于 `Promise.race`，但只等待第一个 fufilled 的 promise，并返回其 value
  - 若 promise 都 rejeced，则返回带有 `AggregareError` 的 error 对象（存储所有的 promise error）
- `Promise.resolve/reject` （因为 async/await 语法，使用较少）
  - `Promise.resolve(value)` 用结果 value 创建一个 resolved 的 promise
    - 兼容性封装：当函数期望一个 promise 时，使用 `Promise.resolve(value)` 将 value 封装进 promise
  - `Promise.reject(error)` 用 error 创建一个 rejected 的 promise。

## Promisification 回调函数 promise 化

Promisification 指将一个接受回调的函数转换为一个返回 promise 的函数。

> 使用包装函数进行转化，部分回调不能完全替代（回调可以被调用无数次），只适用于调用一次回调的函数

## 微任务（Microtask）

> promise 的处理程序 `.then`、`.catch` 和 `.finally` 都是**异步的**，会在代码块运行后触发

### 微任务队列（Microtask queue）

内部队列 PromiseJobs，通常被称为**微任务队列**用于异步任务管理。

- 队列先进先出，先进入的任务先执行。
- 只有在 JavaScript 引擎中没有其它任务在运行时，才开始执行任务队列中的任务

**未处理的 rejection**：微任务队列中的任务都完成时，引擎会检查 promise 是否出现 rejected 状态，并触发 `unhandledrejection` 事件

## async/await

`async/await` 是以更舒适的方式使用 promise 的一种特殊语法

- asycn：`async function f() { return 1; }` 函数总返回一个 promise，非 promise 值被自动包装在 resolved 的 promise 中。
- await：让 JavaScript 引擎等待直到 promise 完成（settle）并返回结果。
  - 只在 async 函数内工作，不能在普通函数中使用（报错）
  - 会暂停函数的执行，直到 promise settled

> 现代浏览器在 modules 中允许顶层 await
> `await` 接受 `thenable` 对象（兼容）

### async 的 error 处理

- `try..catch` 常规处理 await 抛出的异常
- `.catch` 处理：错误未被处理，则异步函数调用返回的 promise 变为 rejected，添加 `.catch` 即可处理
- `unhandledrejection` 捕获 promise 错误
