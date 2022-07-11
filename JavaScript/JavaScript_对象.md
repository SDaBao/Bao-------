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



