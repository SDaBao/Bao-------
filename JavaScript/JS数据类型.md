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
- Math.round
- Math.trunc
- num.toFixed
