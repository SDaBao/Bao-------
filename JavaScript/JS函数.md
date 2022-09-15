# 函数进阶

## 递归与堆栈

执行上下文

## Rest 参数与 Spread 语法

- rest参数 `...args` （出现在函数参数列表最后）：收集剩余的参数并存进指定数组中
  - `arguments` 变量：可在函数中访问的特殊类数组对象（存储所有参数，可迭代）
  - 箭头函数没有 arguments
- Spread 语法（在函数调用与类似的表达式中） 将可迭代对象转化为参数列表（与 `for...of` 相同）
  - spread 浅拷贝 数组与对象

## 变量作用域、闭包

代码块 块级作用域在严格模式下具有独立的词法环境

嵌套函数 函数内包含函数

### 词法环境

**闭包**：是指一个函数可以记住其外部变量并可以访问这些变量。

> 在 JavaScript 中，所有函数都是天生闭包的（"new Function" 语法除外）。JavaScript 中的函数会自动通过隐藏的 `[[Environment]]` 属性记住创建它们的位置，所以它们都可以访问外部变量。

### 垃圾收集

- 嵌套函数（理论上），只要内部函数词法环境可达，仍可被保留在内存中
- JS 引擎优化：嵌套中，未被使用的外部变量会被删除

## var（被淘汰的）

- 没有块级作用域（不是函数作用域就是全局作用域，在代码块外可见）
- 允许重新声明（新的 var 声明会被忽略）
- 可以在声明前被使用（变量提升，赋值不提升）

### 立即调用函数表达式

> 早期只有 var 这一种声明变量方式时，立即调用 用于模仿块级作用域

## 全局对象

- 提供可在任何地方使用的变量和函数，默认内健在语言或环境中
  - 浏览器：`window`，Node：`global`, `globalThis` 全局对象标准名称
- （var）声明的全局函数和变量会成为全局对象的属性（除非使用 modules）
- 使用 `window.x` 直接的方式访问全局对象，更加便于理解

### polyfills

- 判断全局中的内建对象（如较新的 promise）是否存在测试浏览器支持
- 在全局中创建 polyfills 定制实现功能

## 函数对象

> 函数的类型是对象（行为对象 action object）

属性 name：上下文命名，根据上下文推测该属性值（无法推测时为空字符串）

属性 length：返回入参个数（rest 参数不计数）

自定义属性：属性不是变量，可以替代闭包（闭包中定义在函数内的变量不能在外部被访问，但函数的属性可以）

```JS
function makeCounter() {

  function counter() {
    return counter.count++;
  };

  counter.count = 0; // 初始化

  return counter;
}

let counter = makeCounter();

counter.count = 10; // 属性在外部可以修改
```

### 命名函数表达式 NFE

```JS
let sayHi = function func(who) {
  if (who) alert(`Hello, ${who}`);
  else func("Guest"); // 使用 func 调用自己
};
```

命名函数表达式（Named Function Expression）是通过函数表达式的形式被声明的（不是在主代码流里），并且附带了名字的函数。

- 允许函数在内部引用自己（可靠的调用）
- 在外部不可见
- 在函数声明中不存在内部名

> 不直接使用 sayHi 是因为 sayHi 变量的值（需要在外部词法环境中获取）在外部有可能被修改，导致直接调用失效

## `new Function` 语法

```JS
let func = new Function ([arg1, arg2, ...argN], functionBody);

let sum = new Function('a', 'b', 'return a + b'); // 使用

alert( sum(1, 2) ); // 3
```

函数由 **运行时通过字符串参数创建** （任意字符串变为函数）

### `new function` 的闭包

- `new function` 创建的函数 `[[Environment]]` 变量不能指向当前词法环境，而是指向全局环境。
- 不能访问外部变量，只能访问全局变量
  - 压缩程序（minifier）情况：代码压缩会替换变量名，即使能够访问外部变量，其名称也是错误的
- 向 new Function 创建出的新函数传递数据时，必须显式地通过参数进行传递

## 调度：setTimeout 和 setInterval

- setTimeout 将函数推迟到一段时间间隔之后再执行。
- setInterval 重复运行一个函数，间隔一定的时间间隔，并连续重复运行该函数。（语法相同）

```JS
let timerId = setTimeout(func|code, [delay], [arg1], [arg2], ...)
// 函数，延迟执行时间，函数的参数，返回值是定时器标识符

function sayHi(phrase, who) {
  alert( phrase + ', ' + who );
}

setTimeout(sayHi, 1000, "Hello", "John"); // Hello, John
```

- `clearTimeout()` 取消调度
- 传入的函数会在 `setInterval/setTimeout` 内部创建引用（闭包），不会被回收（不再需要调度函数需要取消）
- 所有调度方法都不能保证准确的计时，计时器会因为cpu过载、浏览器在后台、省电模式等变慢

### 嵌套的 `setTimeout`

- 相同：实现周期性调度（同`setInterval`）
- 不同之处：
  - `setTimeout`可以自由设置下次调用时间间隔，更加精确
  - 嵌套调用保证函数执行结束后延时固定，而`setInterval`保证调用时间大于设定的时间（函数执行时间大于delay，则会立即执行，没有间隔）

### 零延时 `setTimeout`

- 让 func 尽快执行，但需要等待当前正在执行脚本结束
- 实际中延时并不为零（浏览器环境）
  - HTML5 标准 所讲：“经过 5 重嵌套定时器之后，时间间隔被强制设定为至少 4 毫秒”

## 装饰器模式和转发，call/applay

> 例子：透明缓存，使用包装器（wrapper）函数将函数的值缓存下来，避免重复计算
> **装饰器不会保留原始函数的属性**，包装器可以有自己的属性（计算函数运行次数、时间等）

- `func.call(context, arg1, arg2, ...)` 第一个参数为 this（上下文），后面作为参数
- `func.apply(context, args)` 使用类数组对象 args 作为参数列表
  > 区别：`call` 期望一个参数列表，`apply` 期望一个包含参数的类数组对象（call支持可迭代对象）

- 呼叫转移（call forwarding）：将所有参数连同上下文一起传递给另一个函数

```JS
let wrapper = function() {
  return func.apply(this, arguments);
};
```

- 方法借用（method borrowing）
  > 从常规数组中借用join方法，并用其在arguments的上下文中运行。`[].join.call(arguments)`（在join的源码中是允许任何类数组的）

## 函数绑定

> 当方法被传递到对象外后，this 存在丢失的情况

`let boundFunc = func.bind(context, ...args);`

- 方法返回函数 func 的绑定变体，绑定上下文 this，和参数（如果有）
- 绑定对象方法的 `this` 可以将其传递到其他地方使用

- 绑定一个现有的函数的某些参数时，绑定后的（不太通用的）函数被称为 partially applied 或 partial（偏函数）
- 一个函数不能被重复绑定（bind返回的绑定函数对象仅在创建的时候记忆上下文）

## 箭头函数

- 没有 this，不能用作构造器（使用 new 调用）
- 没有 arguments
- 没有 super

> 针对没有自己的上下文，但在当前上下文中起作用的短代码
