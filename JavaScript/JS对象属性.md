# 对象属性配置

## 属性标志和描述符

对象属性标志：

- value：对象属性值
- writable：如果为 true，则值可以被修改，否则它是只可读的。
- enumerable：如果为 true，则会被在循环中列出，否则不会被列出。
- configurable：如果为 true，则此属性可以被删除，这些特性也可以被修改，否则不可以。

- `Object.getOwnPropertyDescriptor(obj, propertyName)` 获取有关属性标志信息
- `Object.defineProperty(obj, propertyName, descriptor)` 修改标志信息（新属性需要定义为true，默认为false）
- `Object.defineProperties(obj, descriptors)` 一次定义多个属性
- `Object.getOwnPropertyDescriptors(obj)` 一次获取多个属性描述符

### 克隆对象

```JS
let clone = Object.defineProperties({}, Object.getOwnPropertyDescriptors(obj));
```

### 其他方法

- Object.preventExtensions(obj) 禁止向对象添加新属性。
- Object.seal(obj) 禁止添加/删除属性。为所有现有的属性设置 configurable: false。
- Object.freeze(obj) 禁止添加/删除/更改属性。为所有现有的属性设置 configurable: false, writable: false。

- Object.isExtensible(obj)
- Object.isSealed(obj)
- Object.isFrozen(obj)

## getter 与 setter

> 对象有两种属性类型：数据属性和**访问器属性**（获取与设置值的函数，访问器不能有value）

```JS
let obj = {
  get propName() {
    // 当读取 obj.propName 时，getter 起作用
  },

  set propName(value) {
    // 当执行 obj.propName = value 操作时，setter 起作用
  }
};
```

访问器属性：

- get —— 一个没有参数的函数，在读取属性时工作，
- set —— 带有一个参数的函数，当属性被设置时调用，
- enumerable —— 与数据属性的相同，
- configurable —— 与数据属性的相同。


