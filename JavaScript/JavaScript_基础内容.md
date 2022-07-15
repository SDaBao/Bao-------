# 概述

## JavaScript特点

解释型语言
类似于C和Java的语法结构
动态语言
基于 **原型** 的面向对象

## JS 组成

- ECMAScript
JavaScript语法，ES6-ES11
- DOM
Document_Object_Module（文档对象模型）
- BOM
Browser_Object_Module（浏览器对象模型）

## 语法

### 数据类型

> JavaScript 是一种弱类型语言（或者说动态语言）。不用提前声明变量类型，变量类型在运行过程中自动确定，并且JavaScript拥有动态类型，相同的变量的数据类型是可能发生变化的。

**八种基本类型：**

- **Number**
    >数字型包含整型和浮点型，默认值为0
    进制表示：八进制前加0，十六进制前加0x
    无穷值表示：Infinity（无穷大）
    NaN：Not_a_number，非数字。可以通过 isNaN() 函数判断。
- **bigint**
表示任意长度的整数，在数字后添加n `const bigInt = 1234n;`
*最近被添加* 不能在与number类型计算时隐式转换
- **String**
   >获取字符串长度：length属性
- **Boolean** 默认值为false
- **symbol** 用于唯一标识符
- **Undefined** 申明变量（未赋值）默认类型
- **Null** 空值
- **Object** 对象

**数据类型检测方法： `typeof`**

字面量：源代码中一个固定值的表示方法。

#### 数据类型转换

**转换为字符串类型：**

1. num.toString()
2. String(num)
3. num + '' // 隐式转换

**转换为数字型：**

1. `parseInt(str)`
 转换成整数数值型（小数向下取整，可去除数字末尾单位）
2. `parseFloat(str)`
转换成浮点数数值型
3. `Number(str)` 转换成数字型
4. 运算符隐式转换（+ - * / %）
字符与数字类型进行运算等，JS会自动进行类型转换

**转换为布尔型：**
`Boolean(var)`
>代表空、否定的值（''、0、NaN、null、undefined）转换为false

### 变量

- var：声明的变量参与变量提升，作用域范围为函数作用域。
- let：声明的变量不会被提升，在声明之前存在**暂时性死区**，作用域范围为块作用域，let 不能被重复声明。
- const：声明常量，行为与 let 基本相同，声明时需要被初始化，不可被修改，常用于存放引用类型。

使用 var 在全局作用域中声明的变量会成为 window 对象的属性，let 和 const 声明的变量则不会。

常见面试题：三者区别

```javascript
for (var i = 0; i < 5; i++) {
    setTimeout( () => {
        console.log(i); // 5 5 5 5 5
    }, 0 )
}

for (let i = 0; i < 5; i++) {
    setTimeout( () => {
        console.log(i); // 0、1、2、3、4
    }, 0 )
}
```

### 运算符

1. **算数运算符**
   - 浮点数精度 puzzle: (0.1 + 0.2 == 0.3) is false
   - 支持前置/后置递增运算符
2. **比较运算符**
   - == 判断等于默认转换类型，比如数字型和字符串型==比较
   - === !== 全等符号，判断值与类型是否相等
3. **逻辑运算符**
   - **短路运算（逻辑中断）**
      - 表达式1 && 表达式2
      - 表达式1 || 表达式2 // 进行逻辑判断后，返回值为表达式的原值，中断后的语句不执行
4. **赋值运算符**
   - 支持 = += -= *= /= %=

其他运算符：

- 三元运算符
- 空值合并运算符（新增）
    `a ?? b` 的结果是：
  - 如果 a 是已定义的，则结果为 a，
  - 如果 a 不是已定义的，则结果为 b。

**[运算符优先级](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence#Table)：** 与其他编程语言基本相同

<!-- | 优先级 | 运算符 | 顺序 |
| -----| ---- | ---- |
| 1 | 小括号 | () |
| 2 | 一元运算符 | ++ -- ! |
| 3 | 算数运算符 | 
|4|||
|5||| -->

### 流程控制

结构化编程思想：所有程序的功能都可以使用 **顺序、循环、分支** 三种方式实现。用于提升代码质量

- 顺序结构
- 分支结构
  - if else else_if 三元表达式
  - switch...case （全等匹配）
- 循环结构
  - for
  - while
  - do...while

### 数组

```javascript
var arr = new Array();
var arr = [];
```

数组length属性是动态的，可以修改扩容数组

### 函数

**申明：**

```javascript
// 命名函数
function doSomething ( var1, var2 ) {
    ...
}
var fun = function() { } // 匿名函数
doSomething(1,2,3);
```

- 实参个数过于形参，取决于形参数量
- 实参少于形参，没有接受值的形参为 undefined

**返回值：**

- 函数没有返回值时 默认为undefined

**arguments对象：**

arguments对象存储了函数调用中传递的所有实参

arguments展示形式为一个 **伪数组**

- 具有length属性
- 按索引方式存储数据
- 不具有数组的push，pop等方法

**箭头函数：**

```javascript
let sum = (a, b) => a + b;

// 多行
let sum = (a, b) => {
  let result = a + b;
  return result; 
  // 使用了花括号，需要一个显式的 “return”
};

/* 这个箭头函数是下面这个函数的更短的版本：

let sum = function(a, b) {
  return a + b;
};
*/

alert( sum(1, 2) ); // 3
```

## 关于JS严格模式

`'use strict'` ES5特性
用于明确激活使用新特性，启用后无法撤销
使用 class module 的代码会自动启用严格模式
*浏览器控制台默认不启用*
