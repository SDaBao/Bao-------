# 错误处理

## `try...catch`

- `try...catch`同步执行，内部异步函数丢出的错误不会被捕获
- Error 对象：发生错误时，传递给 catch 的包含详细信息的对象
  - `name` `message` 两个主要属性，错误名称与详细描述
  - `stack` 当前调用栈
- 不需要 err 可忽略（新增特性）
- 自定义 error 对象的属性 并用 `throw` 抛出
  - 自定义类型（建议有 `name` `message` 属性）
  - 使用内建构造器 `Error`，`SyntaxError`，`ReferenceError`，`TypeError`
- 再次抛出：当前的 `try...catch` 不知道如何处理 error 时，抛出给外部的 `try...catch` 处理
- `try…catch…finally` finally 在所有情况下都会被执行
  - `try` 中的 `return` 会在 `finally` 执行后转向外部
  - 没有 `catch` 的 `try...finally`
- 全局 catch：`window.onerror`
  - 将错误信息发送给开发者，作为日志

## 自定义与拓展 error

- 自定义一个 `Error` 对象
- 使用继承的方法拓展 `Error` 对象
  - 有利于使用 `instanceof` 判断错误类型
  - `this.name = this.constructor.name` 将 name 设置为类的名称
  
### 包装异常

用于处理低级别异常并创建高级别 error 而不是各种低级别 error 的函数

> 将各种异常统一成一种异常，用于在 catch 中处理（低级别异常可以是包装异常对象的属性）
