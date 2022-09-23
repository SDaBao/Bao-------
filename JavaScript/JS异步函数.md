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




