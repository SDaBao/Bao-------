# 对象
对象是一个包含相关数据和方法的集合。对象中的变量和函数被称为属性和方法。
## 表示方法
对象的名字表现为一个命名空间 (namespace)
### 点表示法
```javascript
person.age
person.interests[1]
person.bio()
```
**创建子命名空间**
```javascript
name : {
  first : 'Bob',
  last : 'Smith'
},

// 访问方法
person.name.first
person.name.last
```
### 括号表示法
```javascript
person['age']
person['name']['first']
```
## 设置对象成员
可以更新值，也可以创建
```javascript
person['eyes'] = 'hazel'
person.farewell = function() { alert("Bye everybody!") }
```

## “this” 的含义
关键字"this"指向了当前代码运行时的对象
“this” 保证了当代码的上下文 (context) 改变时变量的值的正确性
### 执行上下文
全局环境和函数环境所对应的**执行上下文**分别称为**全局上下文**和**函数上下文**。
执行上下文是以栈（一种 LIFO 的数据结构）的方式被存放起来的，我们称之为**执行上下文栈（Execution Context Stack）**。

> 在 JavaScript 代码开始执行时，首先进入全局环境，此时全局上下文被创建并入栈，之后当调用函数时则进入相应的函数环境，此时相应函数上下文被创建并入栈，当处于栈顶的执行上下文代码执行完毕后，则会将其出栈。

一个执行上下文的生命周期分为**创建**和**执行**阶段。
- 创建阶段主要工作是**生成变量对象**、**建立作用域链**和**确定 this 指向**。
- 执行阶段主要工作是**变量赋值**、**函数引用**以及**执行其它代码**等。

在一个执行上下文中，最重要的三个属性分别是**变量对象（Variable Object）**、**作用域链（Scope Chain）** 和 **this 指向**。

**变量对象**
1. **检索当前上下文中的参数**
该过程生成 Arguments 对象，并建立以形参变量名为属性名，形参变量值为属性值的属性；
2. **检索当前上下文中的函数声明**
该过程建立以函数名为属性名，函数所在内存地址引用为属性值的属性；
3. **检索当前上下文中的变量声明**
该过程建立以变量名为属性名，undefined 为属性值的属性（如果变量名跟已声明的形参变量名或函数名相同，则该变量声明不会干扰已经存在的这类属性）。

**作用域链**
**由当前上下文和上层上下文的一系列变量对象组成的层级链**。它保证了当前执行环境对符合访问权限的变量和函数的有序访问。
函数作用域在函数被声明的时候确定，`[[scope]]` 属性的值也是在函数申明时确定。
> 当函数被调用的时候，其执行上下文会被创建并入栈。在创建阶段生成其变量对象后，会将该变量对象添加到作用域链的顶端并将 `[[scope]]` 添加进该作用域链中。而在执行阶段，变量对象会变为活动对象，其相应属性会被赋值。

*因此，作用域链是由当前上下文变量对象及上层上下文变量对象组成的*

**this 指向**
在函数被调用的时候确定，或者说是在执行上下文被创建时确定的
- 全局上下文中的 `this` 指代全局对象
- 函数中的 `this` 
    - 被调用的函数，被某一个对象所拥有，那么其内部的 this 指向该对象；
    - 函数被独立调用，那么其内部的 this 指向 undefined（非严格模式下指向 window）
    - 构造函数，内部 this 指向新创建的对象实例


# 对象原型
> JavaScript 常被描述为一种**基于原型的语言 (prototype-based language)**——每个对象拥有一个**原型对象**，对象以其原型为模板、从原型继承方法和属性。原型对象也可能拥有原型，并从中继承方法和属性，一层一层、以此类推。这种关系常被称为**原型链 (prototype chain)**，它解释了为何一个对象会拥有定义在其他对象中的属性和方法。
## JavaScript 中的原型
在 javascript 中，每个函数都有一个特殊的属性叫作**原型（`prototype`）**
> **`Object.cerate()` 与 `new Object()` 区别**
Object.cerate() 创建的新对象的原型指向接收的参数本身
new Object() 创建的新对象的原型指向的是 Object 的 prototype

访问函数的属性会根据 `__proto__` 的层级顺序，从外往内层依次查找（直到找到或者未找到并判定为 `undefined`）

例如 `person1.valueOf()` 这个方法返回了被调用对象`person1`的值，过程如下：
- 浏览器首先检查，person1 对象是否具有可用的 `valueOf()` 方法。
- 如果没有，则检查 person1 对象的原型对象（即 `Person()` 构造函数的 prototype 属性所指向的对象）是否具有可用的 `valueof()` 方法。
- 如果也没有，则浏览器检查 `Person()` 构造函数的 prototype 属性所指向的对象的原型对象（即 Object构造函数的 prototype 属性所指向的对象）是否具有可用的 `valueOf()` 方法。这里有这个方法，于是该方法被调用。

## `prototype` 属性：继承成员被定义的地方

使用 `String`、`Date`、`Number` 和 `Array` 等等对象，创建变量时，通过原型链继承了全局对象的属性。
```javascript
var myString = 'This is my string.';
```
例如：定义字符串时，变量继承了字符串的方法，如 `split()`、`indexOf()`、`replace()` 等

## `constructor` 属性
每个实例对象都从原型中继承了一个 constructor 属性，该属性指向了用于构造此实例对象的构造函数。

## 原型的修改
构造器的原型可以动态添加、修改
```javascript
Person.prototype.farewell = function() {
  alert(this.name.first + ' has left the building. Bye for now!');
}

person1.farewell();
```
通过对构造器的 `prototype` 属性进行修改，为基于该构造器创建的对象更新、拓展了可用功能。

# 继承
JavaScript 与C++等语言不同，使用了另一套实现面向对象的方式，继承的对象函数并不是通过复制而来，而是通过原型链继承（通常被称为 **原型式继承 —— prototypal inheritance**）

`Teacher()` 构造函数里面使用 `call()` 函数运行了 `Person()` 构造函数，即 `Teacher` 继承了 `person` 的属性。
```javascript
function Teacher(first, last, age, gender, interests, subject) {
  Person.call(this, first, last, age, gender, interests);

  this.subject = subject;
}
```
## 原型和构造器引用的继承

```javascript
// 设置原型的继承
Teacher.prototype = Object.create(Person.prototype);
Teacher.prototype.constructor = Person();

Object.defineProperty(Teacher.prototype, 'constructor', {
    value: Teacher,
    enumerable: false, // so that it does not appear in 'for in' loop
    writable: true });
```
## 对象成员的四类属性或方法
1. 定义在构造器函数中，用于给予对象实例的属性或方法
2. 直接在构造函数上定义，仅在构造函数上可用的属性或方法
   > 通常仅在浏览器的内置对象中可用，并通过被直接链接到构造函数来识别，而不是实例。例如Object.keys()。它们一般被称作**静态属性或静态方法**
3. 在构造函数原型上定义，由所有实例和对象类继承的属性或方法
4. 在对象实例上可用的对象（例如实例化时创建的对象的方法）

## ECMAScript 2015 的类
es6中引入了class的方式创建类
[JavaScript Class](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Classes)
```javascript
class Person {
  constructor(first, last, age, gender, interests) {
    this.name = {
      first,
      last
    };
    this.age = age;
    this.gender = gender;
    this.interests = interests;
  }

  greeting() {
    console.log(`Hi! I'm ${this.name.first}`);
  };
}

let han = new Person('Han', 'Solo', 25, 'male', ['Smuggling']);
han.greeting();
```
在类中，依然可以创建构造函数，定义类方法与属性，并使用new实例化对象

>在 JS 引擎下，**类会被转换为原型继承模型**——这只是**语法糖（Syntactic sugar）**（对功能无影响，方便使用的语法）。

### 类语法的继承
使用 `extend` 继承父类
```javascript
class Teacher extends Person {
  constructor(first, last, age, gender, interests, subject, grade) {
    super(first, last, age, gender, interests);

    // subject and grade are specific to Teacher
    this.subject = subject;
    this.grade = grade;
  }
}
```

其中 `super()` 运算符实现了对父构造函数的调用，继承父类。

### getter & setter
规范变量（类属性）设置，实现对类中属性的访问

> JavaScript 由于原型链等特性的存在，在不同对象之间功能的共享通常被叫做 **委托** - 特殊的对象将功能委托给通用的对象类型完成。
*这也许比将其称之为继承更为贴切，因为“被继承”了的功能并没有被拷贝到正在“进行继承”的对象中，相反它仍存在于通用的对象中。*

# JSON 的使用
**JavaScript 对象表示法（JSON）** 是用于将结构化数据表示为 JavaScript 对象的标准格式
通常用于在网站上表示和传输数据（例如从服务器向客户端发送一些数据，因此可以将其显示在网页上）。

## JSON 结构
JSON 对象就是基于 JavaScript 对象
可以将 JS 对象写入 JSON 数据（如字符串，数字，数组，布尔还有其它的字面值对象）
访问对象内的数据与JS相同
```javascript
superHeroes.hometown
superHeroes["active"]
```
## JSON 数组
数组对象也是一种合法的 JSON 对象
```JSON
[
  {
    "name" : "Molecule Man",
    "age" : 29,
    "secretIdentity" : "Dan Jukes",
    "powers" : [
      "Radiation resistance",
      "Turning tiny",
      "Radiation blast"
    ]
  },
  {
    "name" : "Madame Uppercut",
    "age" : 39,
    "secretIdentity" : "Jane Wilson",
    "powers" : [
      "Million tonne punch",
      "Damage resistance",
      "Superhuman reflexes"
    ]
  }
]
```
## 注意事项
- JSON 是一种纯数据格式，它只包含属性，没有方法。
- JSON 要求在字符串和属性名称周围使用双引号，单引号无效。
- JSON 文件容易出错，可以使用检验工具检测格式。
- JSON 可以将任何标准合法的 JSON 数据格式化保存，不限于数组和对象。
- 与 JavaScript 代码中对象属性可以不加引号不同，JSON 中只有带引号的字符串可以用作属性。

## JSON 对象和字符串的转化
- `parse()`: 以文本字符串形式接受 JSON 对象作为参数，并返回相应的对象。
- `stringify()`: 接收一个对象作为参数，返回一个对应的 JSON 字符串。





