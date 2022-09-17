# 原型

## `[[Prototype]]`

从 object 中读取一个缺失的属性时，JavaScript 会自动从原型中获取该属性。通过 `[[Prototype]]` 引用的对象被称为“原型”.

- 原型的引用不能闭环
- `[[Prototype]]` 属性的值只能是对象或null，`__proto__` 是 `[[Prototype]]` 的 `getter/setter`

- 原型共享（继承）的是方法，而不是对象状态（访问器对象会帮助维护继承的对象自己的状态），修改删除操作会直接在对象上进行（不使用原型）
- `this` 不受原型影响，始终是当前调用方法的对象
- `for..in` 会迭代继承的属性，`obj.hasOwnProperty(key)` 可以判断自有/继承属性（该方法是从 `Object.prototype` 中继承的，但由于其是不可枚举的，所以不会出现在`for..in`循环中）
- 所有其他的键/值获取方法仅对对象本身起作用

> JS 引擎会记住对象是从对象或者原型链中获取属性的，并且会根据内容更改自动更新缓存，所以调用对象的方法是无区别的

## `F.prototype`

如果 `F.prototype` 是一个对象，那么 new 操作符会使用它为新对象设置 `[[Prototype]]`。

**函数的prototype属性只是一个常规属性**，当且仅当作为构造函数调用（`new Func`），且属性值为对象时，为新对象的 `[[prototype]]` 属性赋值。

- 默认的 "prototype" 是一个只有属性 `constructor` 的对象，属性 `constructor` 指向函数自身（不建议替换默认的 prototype 属性，以保证 prototype 对象中 constructor 的值正确）

```JS
function Rabbit() {}
// 默认：
// Rabbit.prototype = { constructor: Rabbit }

let rabbit = new Rabbit(); // 继承自 {constructor: Rabbit}

alert(rabbit.constructor == Rabbit); // true (from prototype)
```

## 原生的原型

- `Object.prototype` 即原生的原型，是所有对象的原型
- `Object.prototype` 上方的链中没有更多的 `[[Prototype]]`，其原型为 null

### 其他内建原型

- 方法都存储在 prototype 中（Array.prototype、Object.prototype、Date.prototype 等）。
- 对象本身只存储数据（数组元素、对象属性、日期）。

*部分方法在原型上会重叠*

函数的原型 Function.prototype 继承自对象

基本数据类型：使用包装器调用原型上的方法。例如`Number.prototype`、`String.prototype` 和 `Boolean.prototype`

null 和 undefined 没有对象包装器，没有原型

### 修改原生原型

在开发中修改原生原型有可能引发冲突

- **在现代编程中，只有一种情况下允许修改原生原型。那就是 polyfilling。**

  > Polyfilling：某个方法在 JavaScript 规范中已存在，但是特定的 JavaScript 引擎尚不支持该方法，那么我们可以通过手动实现它，并用以填充内建原型

```JS
if (!String.prototype.repeat) { // 如果这儿没有这个方法
  // 那就在 prototype 中添加它

  String.prototype.repeat = function(n) {
    // 重复传入的字符串 n 次

    // 实际上，实现代码比这个要复杂一些（完整的方法可以在规范中找到）
    // 但即使是不够完美的 polyfill 也常常被认为是足够好的
    return new Array(n + 1).join(this);
  };
}

alert( "La".repeat(3) ); // LaLaLa
```

- 原型中的方法可以被借用

## 原型方法

> `obj.__proto__` 是被淘汰的设置原型方法（它仅适用于浏览器，与用于作为属性创建新对象）

获取、设置原型方法：

- `Object.getPrototypeOf(obj)` —— 返回对象 obj 的 `[[Prototype]]`。
- `Object.setPrototypeOf(obj, proto)` —— 将对象 obj 的 `[[Prototype]]` 设置为 proto
- `Object.create(proto, [descriptors])` —— 利用给定的 proto 作为 `[[Prototype]]` 和可选的属性描述来创建一个空对象。

```JS
// 对 obj 及其所有属性描述符进行真正准确的浅拷贝
let clone = Object.create(
  Object.getPrototypeOf(obj),
  Object.getOwnPropertyDescriptors(obj)
);
```

```JS
// 创建一个以 animal 为原型的新对象
let rabbit = Object.create(animal); // 与 {__proto__: animal} 相同

alert(rabbit.eats); // true

alert(Object.getPrototypeOf(rabbit) === animal); // true

Object.setPrototypeOf(rabbit, {}); // 将 rabbit 的原型修改为 {}
```

### "Very plain" objects 无原型对象

常用于字典，存储任意键

> 通常对象会从 `Object.prototype` 继承内建的方法和 `__proto__` getter/setter，会占用相应的键，导致副作用。只有原型为 null ，对象才是空的。

```JS
let obj = Object.create(null);
// 或者：obj = { __proto__: null }
```

创建的没有原型的空对象，该对象没有内建的对象的方法且原型为 null，但依然可以使用对象相关的方法（这些方法不在原型中），如 `Object.keys(obj)`
