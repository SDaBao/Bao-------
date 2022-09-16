# 原型

## `[[Prototype]]`

从 object 中读取一个缺失的属性时，JavaScript 会自动从原型中获取该属性

- 原型的引用不能闭环
- `__proto__` 的值只能是对象或null，`__proto__` 是 `[[Prototype]]` 的 `getter/setter`

