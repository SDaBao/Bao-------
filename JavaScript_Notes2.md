# 异步 JavaScript
异步编程技术使你的程序可以在执行一个可能长期运行的任务的同时继续对其他事件做出反应而不必等待任务完成。与此同时，你的程序也将在任务完成后显示结果。
例如：发送HTTP请求、访问外部设备、访问文件等
- 使用 fetch() 发起 HTTP 请求
- 使用 getUserMedia() 访问用户的摄像头和麦克风
- 使用 showOpenFilePicker() (en-US) 请求用户选择文件以供访问
## 事件处理程序
事件处理程序是异步编程的一种形式：提供的函数（事件处理程序）将在事件发生时被调用（而不是立即被调用）。

例如在 XMLHttpRequest API 的应用中，程序可以在请求进行的同时继续运行，而事件处理程序将在请求完成时被调用

## 回调
事件处理程序是一种特殊类型的回调函数。
回调函数则是一个被传递到另一个函数中的会在适当的时候被调用的函数。
*回调函数曾是 JavaScript 实现异步函数的主要方式（现代API不常用）*

## Promise
Promise 是现代 JavaScript 中异步编程的基础
是一个由异步函数返回的可以向我们**指示当前操作所处的状态的对象**。

### fetch() API
基于 Promise 的替代 XMLHttpRequest 的方法
```javascript
const fetchPromise = fetch('https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json');

console.log(fetchPromise);

fetchPromise.then( response => {
  console.log(`已收到响应：${response.status}`);
});

console.log("已发送请求……");
```

### 链式使用 Promise
Promise 的优雅之处在于 then() 本身也会返回一个 Promise，这个 Promise 将指示 then() 中调用的异步函数的完成状态
**Promise 链**：直接返回 json() 返回的 Promise，并在该返回值上调用第二个 "then()"。
需要连续进行异步函数调用时，可以避免不断嵌套带来的缩进增加。

### 处理错误 catch()
```javascript
const fetchPromise = fetch('https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json');

fetchPromise
  .then( response => {
    if (!response.ok) {
      throw new Error(`HTTP error: ${response.status}`);
    }
    return response.json();
  })
  .then( json => {
    console.log(json[0].name);
  })
  .catch( error => {
    console.error(`无法获取产品列表：${error}`);
  });
```

### Promise 状态
- **待定（pending）**：初始状态，既没有被兑现，也没有被拒绝。这是调用 fetch() 返回 Promise 时的状态，此时请求还在进行中。
- **已兑现（fulfilled）**：意味着操作成功完成。当 Promise 完成时，它的 then() 处理函数被调用。
- **已拒绝（rejected）**：意味着操作失败。当一个 Promise 失败时，它的 catch() 处理函数被调用。

>**“成功”或“失败”的含义取决于所使用的 API：**
例如，fetch() 认为服务器返回一个错误（如404 Not Found）时请求成功，但如果网络错误阻止请求被发送，则认为请求失败。

有时我们用 **已敲定（settled）** 这个词来同时表示 **已兑现（fulfilled）** 和 **已拒绝（rejected）** 两种情况。
如果一个 Promise 处于**已决议（resolved）状态**，或者它被“锁定”以跟随另一个 Promise 的状态，那么它就是 **已兑现（fulfilled）**。

### 组合使用 Promise
**`Promise.all()` 方法**：接收一个 Promise 数组，并返回一个单一的 Promise。

- 当且仅当数组中所有的 Promise 都被兑现时，才会通知 `then()` 处理函数并提供一个包含所有响应的数组，数组中响应的顺序与被传入 `all()` 的 Promise 的顺序相同。
- 会被拒绝——如果数组中有任何一个 Promise 被拒绝。此时，`catch()` 处理函数被调用，并提供被拒绝的 Promise 所抛出的错误。

**`Promise.any()` 方法**：类似于 Promise.all()，但只有在 Promise 数组中的任何一个被兑现时它就会被兑现，如果所有的 Promise 都被拒绝，它也会被拒绝

### async & await
async 关键字为你提供了一种更简单的方法来处理基于异步 Promise 的代码。
在一个函数 function 的开头添加 async，就可以使其成为一个异步函数。

```javascript
async function fetchProducts() {
  try {
    // 在这一行之后，我们的函数将等待 `fetch()` 调用完成
    // 调用 `fetch()` 将返回一个“响应”或抛出一个错误
    const response = await fetch('https://mdn.github.io/learning-area/javascript/apis/fetching-data/can-store/products.json');
    if (!response.ok) {
      throw new Error(`HTTP 请求错误：${response.status}`);
    }
    // 在这一行之后，我们的函数将等待 `response.json()` 的调用完成
    // `response.json()` 调用将返回 JSON 对象或抛出一个错误
    const json = await response.json();
    console.log(json[0].name);
  }
  catch(error) {
    console.error(`无法获取产品列表：${error}`);
  }
}

fetchProducts();
```
> 这里调用 await fetch()，调用者得到的并不是 Promise，而是一个完整的 Response 对象，就好像 fetch() 是一个同步函数一样。

## workers 多线程
Workers 给了你在不同线程中运行某些任务的能力，因此你可以启动任务，然后继续其他的处理（例如处理用户操作）。
*但是，线程被挂起与运行的时间是未知的，不同的线程访问相同变量有可能会引发bug。*

**主代码和 worker 代码永远不能直接访问彼此的变量**
> Workers 和主代码运行在完全分离的环境中，只有通过相互发送消息来进行交互。这意味着 **workers 不能访问 DOM**（窗口、文档、页面元素等等）。

三种 workers 类型：
- dedicated workers
- shared workers
- service workers












