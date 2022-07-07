# 基础

## JavaScript特点

解释型语言
类似于C和Java的语法结构
动态语言
基于原型的面向对象

## JS组成

### ECMAScript

JavaScript语法，ES6-ES11

### DOM

Document_Object_Module（文档对象模型）

### BOM

Browser_Object_Module（浏览器对象模型）

## 语法

### 数据类型

> JavaScript 是一种弱类型语言（或者说动态语言）。不用提前声明变量类型，变量类型在运行过程中自动确定，并且JavaScript拥有动态类型，相同的变量的数据类型是可能发生变化的。

**6个基本数据类型：**

- **Number**
    >数字型包含整型和浮点型，默认值为0
    进制表示：八进制前加0，十六进制前加0x
    无穷值表示：Infinity（无穷大）
    NaN：Not_a_number，非数字。可以通过 isNaN() 函数判断。
- **String**
   >获取字符串长度：length属性
- **Boolean** 默认值为false
- **Undefined** 申明变量（未赋值）默认类型
- **Null** 空值
- **Object** 对象

**数据类型检测方法： `typeof`**

#### 字面量

源代码中一个固定值的表示方法。

#### 数据类型转换

转换为字符串类型

1. num.toString()
2. String(num)
3. num + '' // 隐式转换

转换为数字型

1. parseInt(str) // 转换成整数数值型（小数向下取整，可去除数字末尾单位）
2. parseFloat(str) // 转换成浮点数数值型
3. Number(str) // 转换成数字型
4. 运算符隐式转换（+ - * / %）// str - 0

转换为布尔型
Boolean(var) // 代表空、否定的值（''、0、NaN、null、undefined）转换为false

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

#### 运算符优先级
<!-- | 优先级 | 运算符 | 顺序 |
| -----| ---- | ---- |
| 1 | 小括号 | () |
| 2 | 一元运算符 | ++ -- ! |
| 3 | 算数运算符 | 
|4|||
|5||| -->

### 流程控制
#### 顺序结构
#### 分支结构
- if else else_if 三元表达式
- switch...case （全等匹配）
#### 循环结构
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
#### 申明
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


#### 返回值
- 函数没有返回值时 默认为undefined 

#### arguments
arguments对象存储了函数调用中传递的所有实参

arguments展示形式为一个伪数组
- 具有length属性
- 按索引方式存储数据
- 不具有数组的push，pop等方法

### 作用域


#### es6之前
##### 全局作用域
整个script
全局变量
函数内部直接赋值（未声明）的变量
##### 局部作用域
函数内部
局部变量
函数形参可以看做局部变量

##### 效率
- 全局变量浏览器关闭后才会销毁，比较占用内存资源
- 局部变量在代码块被执行时初始化，结束时销毁，节省内存

##### 作用域链
内部函数访问外部函数的变量，采取的是链式查找的方式来决定取哪一个值（就近原则）
#### es6
##### 块级作用域


### 预解析
JavaScript解析器运行JavaScript代码分为两步：
1. 预解析
变量提升&函数提升：ja引擎会把js中所有的变量申明和函数申明提升到当前作用域的最前面（变量提升优先于函数提升）
[Hoisting（变量提升）](https://developer.mozilla.org/zh-CN/docs/Glossary/Hoisting)

2. 代码执行
按照代码顺序自上而下执行

### JS对象
JavaScript中的对象分为三种：自定义对象、内置对象、浏览器对象（JS独有）

**对象调用**
调用属性 `obj.property` 或 `obj['property']`
调用方法 `obj.method()`
#### 自定义对象
1. 对象字面量创建对象
```javascript
var obj = {
    property: '',
    method: function() {
        ...
    }
}
```
- 对象中的属性和方法采用键值对的方式定义
- 多个属性或方法使用逗号隔开
- 方法使用匿名函数定义

2. 利用 new Object 创建对象
```javascript
var obj = new Object();
obj.property = '';
obj.method = function() {}
```
- 利用赋值语句添加对象属性和方法

3. 构造函数创建对象
```JavaScript
function Constructor(value) {
    this.prop = value;
    this.method = function() {}
}
var obj = new Constructor(value);
```
- 构造函数名首字母大写
- 构造函数名不需要 return 默认返回一个对象
- 调用构造函数必须使用 new
- 构造函数的属性和方法前面必须添加 this

**构造函数和对象区别**
- 构造函数，泛指某一大类，抽象了对象的公共部分，封装到了函数里面
- 对象特指一个具体的实物
- 利用构造函数创建对象的过程成为对象的实例化

**new关键字执行过程**
1. new 狗仔函数在内存中创建一个空的对象
2. 让 this 指向这个新的对象
3. 执行构造函数中的代码，给新对象添加属性和方法
4. 返回这个新对象

**遍历对象**
使用`for...in` 遍历对象
```javascript
for (var k in obj) {
    k; // 属性名
    obj[k]; // 属性值
}
```

#### 内置对象
JS语言中自带的一些对象，提供一些常用的或是基本而必要的功能（属性&方法）帮助快速开发
[MDN_WEB开发文档](https://developer.mozilla.org/zh-CN/)
- **Math对象**
[Math文档](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math)
Math数学对象不是一个构造函数
拥有基本数学函数功能
- **日期对象**
[Date文档](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date)
日期对象是一个构造函数，使用new创建日期对象
- **数组对象**
[数组Array文档](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array)

- **字符串对象**
基本包装类型：把 简单数据类型 包装成了 复杂数据类型
字符串不可变：字符串变量的重新赋值本质上是指针的改变（为了性能不要大幅拼接字符串）

### 数据类型
**简单数据类型**
简单类型又叫做基本数据类型或值类型
string, number, boolean, undefined, null
传参：深拷贝

**复杂数据类型**
又称为引用类型
通过new关键字创建的对象
传参：浅拷贝

### JavaScript内存管理
[JS内存管理](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Memory_Management)
JavaScript是在创建变量（对象，字符串等）时自动进行了分配内存，并且在不使用它们时“自动”释放

#### 垃圾回收
- **引用技术垃圾收集**
    > 此算法把“对象是否不再需要”简化定义为“对象有没有其他对象引用到它”。如果没有引用指向该对象（零引用），对象将被垃圾回收机制回收。
    **限制：循环引用**
    IE 6,7 使用，目前基本被淘汰

- **标记-清除算法**
    > 这个算法把“对象是否不再需要”简化定义为“对象是否可以获得”。（解决了循环引用问题）
    **限制：那些无法从根对象查询到的对象都将被清除（实际情况很少碰到）**
    广泛使用



