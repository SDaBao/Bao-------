# JS数据类型

## 原始类型

七种原始类型：除 Object 以外的所有基本数据类型。

### 对象包装器

为原始类型提供对象方法的访问方式。（null 与 undefined 没有任何方法）

```javascript
let str = "Hello";

alert( str.toUpperCase() ); // HELLO
```

- 字符串 `str` 是一个原始值。因此，在访问其属性时，会创建一个包含字符串字面值的特殊对象，并且具有可用的方法，例如 `toUpperCase()`。
- 该方法运行并返回一个新的字符串（由 `alert` 显示）。
- 特殊对象被销毁，只留下原始值 `str`。

## 数字类型

存储方式：

- Number 64位的双精度浮点数
- BigInt 任意长度整数

语法糖写法：`num = 1_000_000` `num = 1e9` `num = 0xff`

### toString(base)

```javascript
alert( 123456..toString(36) ); // 2n9c（表达式第一个点表示小数点，用于在数字上调用方法）
```

用36进制（最大进制，所有数以 [0-9a-Z] 表示）

### 小数计算

- Math.floor
- Math.ceil
- Math.round 舍入
- Math.trunc 省略小数
- num.toFixed 保留 n 位小数并舍入

双精度浮点数（64位，符号1位、阶码11位、尾数52位）

> 在接近16位十进制数时，js仍会使用双精度浮点数表示数字，会出现精度丢失。
  数字内部存在 `0` 与 `-0` 表示数字 0

### 常规数字检测 NaN 与 Infinity

- `Infinity` `-Infinity` 特殊数值
- `NaN` 代表 error ，不等于任何东西

都属于 number 类型，但不是普通数字

比较数字

- isNaN 判断数字是否为 NaN
- isFinite 判断数字是否为常规数字
- Object.is(a, b) 判断值相等，可以用于判断 NaN，不能判断两种 0 的表示

### 数字类型转换 parseInt parseFloat

- 加号 + 或 Number() 的数字转换是严格的，出错即为 NaN
- parseInt 从字符串中读取数，直到不为整数为止（第二个参数为进制数[2 - 36]）
- parseFloat 从字符串中读取数，直到不为小数为止

### Math 内建对象

## 字符串

内部格式：`UTF-16`

- 字符串长度 length
- 字符串访问方法
- 在内存中表现形式，不可直接改变（拼接字符串本质上是创建新字符串）
- 大小写改变 `toLowerCase/toUpperCase`
- 查找字符串 `indexOf` 或 `includes/startsWith/endsWith`
- 获取字符串 下标访问 子字符串：`slice()` `substring()`
- 字符串比较 （基于原始值）
  - `str.codePointAt(pos)` 获取值
  - `String.fromCodePoint(code)` 通过值创建字符
  - `str.localeCompare(str2)` 根据语言规则返回顺序结果

### Unicode 编码

- 代理对
- 组合字符（变音符）

## 数组

- 创建数组两种方法： `new Array(n)` `arr = []`，length是数组长度，是最后一个数字索引+1，会根据数组方法自动调整
- 获取元素方法：下标访问 `arr.at()`
- 双端队列方法：`push` `pop` `shift` `unshift` （后两项性能较低，涉及到数组整体移动）
- 遍历数组方法：`for`（效率最高） `for...of`（只访问items） `for...in`（不建议使用，会遍历所有属性，适用于普通对象，用于数组速度慢）
- 不能使用 == 比较数组

数组方法：

- 删除元素： `splice` `delete`（只删除值，对应索引不会删除）
- slice 返回新数组（浅拷贝）
- concat 合并创建新数组（浅拷贝），类数组对象具有 `Symbol.isConcatSpreadable` 属性才可被合并
- 搜索元素：`indexOf/lastIndexOf(item, pos)` `includes(val)` `find/filter(func)` `findIndex find`
- 遍历元素：`forEach(func)`
- 转换数组：`map(func)` `sort(func)` `reverse()` `split/join` `reduce/reduceRight(func, initial)`
- 判断数组：`Array.isArray(value)`
- 检查数组：`arr.some(fn)/arr.every(fn)` some判断是否有元素是否符合要求，every判断所有元素是否符合要求
- `arr.fill(value, start, end)` 从索引 start 到 end，用重复的 value 填充数组
- `arr.copyWithin(target, start, end)` 复制到目标位置并覆盖
- `arr.flat(depth)/arr.flatMap(fn)` 数组扁平化
- `arr.of()`

## Iterable object（可迭代对象）

可迭代对象是可在 `for...of` 循环中使用的对象。（任何对象都可以被定制为可迭代对象）

- 可迭代对象必须实现 `Symbol.iterator` 方法
  - obj[Symbol.iterator]() 的结果被称为 迭代器（iterator）
  - 迭代器必须有 `next()` 方法，返回一个 `{done: Boolean, value: any}` 对象
- `Symbol.iterator` 方法可以被 `for...of` 自动调用，也可以手动调用
- 字符串迭代器能够识别代理对（utf-16拓展字符）

类数组对象：有索引属性和 `length` 属性的对象

**`Array.from` 将可迭代对象或类数组对象转化为真正的数组，使其可以应用数组方法。**

## Map 与 Set

### Map

- map 可以使用对象作为键，比较键的方式：`SameValueZero 算法` 类似于全等于，但可以比较 NaN
- 迭代方法：`map.keys()` `map.values()` `map.entries()`（[key, value]）`forEach`
- 创建 Map：`[key, value]` 数组 `Object.entries(obj)`（返回键值对数组）
- 由 Map 创建对象：`Object.fromEntries()`（map转换成键值对数组，由键值对数组创建）

### Set

- 值不重复
- 迭代方法：`for..of` 或 `forEach`，map 中的方法通用支持。
- 大部分方法兼容 Map，并相同。