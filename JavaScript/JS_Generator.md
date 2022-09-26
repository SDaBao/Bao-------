# Generator

## Generator 函数

常规函数与 generator 区别：

- 常规函数只会返回一个单一值
- generator 可按需一个接一个返回多个值（可配合 iterable 创建数据流）

```JS
function* generateSequence() {
  yield 1;
  yield 2;
  return 3;
}
```

- `next()` 是 generator 的方法，结果为具有两个属性的对象
  - `value`：产出的值（yielded）
  - `done`：generator 函数是否已执行完 true/false

- generator 是可迭代的
  - 可使用 `for..of` `...` 遍历结果
  - 遍历不会迭代 `done:true` 的值（即 return 返回的值），`yield` 的值才可遍历

```JS
// 可迭代对象添加使用 generator 的迭代方法
let range = {
  from: 1,
  to: 5,

  *[Symbol.iterator]() { // [Symbol.iterator]: function*() 的简写形式
    for(let value = this.from; value <= this.to; value++) {
      yield value;
    }
  }
};

alert( [...range] ); // 1,2,3,4,5
```

- `yield*` **委托** 执行给另一个 Generator （在 generator 中嵌套 generator）
- `yield` 是双向的（使用 next/yield 与外部代码调用交换结果）
  - 调用 `next(value)` 方法，`value` 作为上一个 `yield` 的结果传递回 generator
- `generator.throw(err)` 向 yield 传递一个 error
  - err 未在 generator 函数内被捕获，则错误会掉入到外部调用代码中。
- `generator.return(value)` 完成 generator 的执行并返回给定的 `value`
  - 会设置 `done:true` 结束 generator 执行

## 异步迭代和 Generator

异步迭代：

- 使用 `Symbol.asyncIterator` 取代 `Symbol.iterator`
- `next()` 方法应该返回一个 promise（带有下一个值，并且状态为 fulfilled）
  - 关键字 async 可以实现这一点，我们可以简单地使用 `async next()`
- 使用 `for await (let item of iterable)` 循环来迭代这样的对象
  - 注意关键字 await
- spread 语法无法异步工作

异步 generator（finally）

- 在 `function*` 前面加上 `async`
- 使用 `for await (...)` 来遍历

异步可迭代对象：结合异步迭代与异步 generator 实现
