# Vue

Vue 是一个渐进式现代 JavaScript 框架，可以逐步集成到应用中

适用于 **单页应用程序 (SPAs)** 开发

## 快速开始

- 引入老项目方式：在 script 标签中引入 vue.js
- 构建复杂应用方式：
    前提：安装使用需要 Node.js, npm or yarn
    安装 vue 脚手架，并通过脚手架初始化应用

### 项目结构

- .eslintrc.js
    eslint 配置文件，管理语法校验规则。
- babel.config.js
    Babel 配置文件，转换JS代码为旧语法，使在开发中使用 JavaScript 的新特性。
- .browserslistrc
    Browserslist 的配置文件，可以通过它来控制需要对哪些浏览器进行支持和优化。
- package.json
    对项目或者模块包的描述，用于 node_modules资源部 和 启动、打包项目的 npm 命令管理。

文件夹：

- node_modules
    用于存放包管理工具 node 下载工具包的文件夹
- public
    存放公用文件，包含一些在 Webpack 编译过程中没有加工处理过的文件（有一个例外：index.html 会有一些处理）。
  - favicon.ico: 项目的图标。
  - index.html: 应用的模板文件，Vue 应用会通过这个 HTML 页面来运行，也可以通过 lodash 这种模板语法在这个文件里插值。

- src
    Vue 应用的核心代码目录
  - assets：img、css、js 等静态资源目录，但是因为它们属于代码目录下，所以可以用 webpack 来操作和处理。意思就是你可以使用一些预处理比如 Sass/SCSS 或者 Stylus。
  - components：自定义组件的目录。
  - router：保存各类路由的相关配置文件夹，vue-router
  - store：存放 vuex 为vue专门开发的状态管理器
  - view：视图文件夹

  - main.js
    应用的入口文件。目前它会初始化 Vue 应用并且制定将应用挂载到  index.html 文件中的哪个 HTML 元素上。通常还会做一些注册全局组件或者添额外的 Vue 库的操作。
  - App.vue
    Vue 应用的根节点组件，往下看可以了解更多关注 Vue 组件的信息。

### .vue文件

单文件组件，vue 鼓励将模板、脚本、CSS 整合放置在 .vue 文件中。

在 App.vue 中，由 `<template>`, `<script>` 和 `<style>` 三部分组成

- 使用标签 lang 属性 配置语言
- `<script>` 标签需要默认导出一个 JS 对象
- `<style>` 设置scoped属性 设置组件样式私有化

## 组件使用

1. 创建自己的组件
2. 在应用中使用组件
    在 `<script>` 中 import 组件
    >组件文件名及其在 JavaScript 中的表示方式总是用大写驼色（例如ToDoList）
    等价的自定义元素总是用连字符小写（例如`<to-do-list>`）

### props 组件动态化

在组件中添加 props 实现动态内容

注册 props 方法：

- 字符串数组列出 props
- 将 props 定义为一个对象

### 数据对象

使用 Vue 的 data 属性管理数据，用于更新组件

- data 属性是函数，为了保持运行时组件数据的唯一性
- v-bind 绑定 JS 表达式到 HTML 元素

### v-for 渲染列表

`v-for="item in items"` `iterms` 是要迭代的列表， `item` 是数组中当前元素的引用

- key 属性 用于帮助 Vue 标识列表中的元素
    标识需要是唯一的，数字或者字符串类型

### $emit 触发当前实例上的事件，附加参数传给监听器回调

- 父组件可以使用 props 把数据传给子组件。
- 子组件可以使用 $emit 触发父组件的自定义事件。
    `vm.$emit( event, […args] )` 子组件触发自定义事件
    `vm.$on( event, fn )` 父组件监听并调用方法

### v-bind 绑定事件

将一个或多个属性或者一个组件的 prop 动态绑定到表达式

### v-module 创建双向绑定

在表单元素上创建双向数据绑定，监听输入事件，根据控件类型自动选取正确的方法来更新元素。
*本质上是语法糖*

修饰符：

- `.lazy` 改变同步使用的事件为 change事件（减少同步数据次数）
- `.trim` 删除输入前后的空格

### v-on 监听事件

监听DOM事件，并在触发时运行javascript代码或方法（将方法绑定到事件上）。

### 计算属性

根据其他值所计算出来的，例如统计数组中符合条件的数量等
计算属性将结果缓存起来

```javascript
computed: {
  listSummary() {
    const numberFinishedItems = this.ToDoItems.filter(item =>item.done).length
    return `${numberFinishedItems} out of ${this.ToDoItems.length} items completed`
  }
}
```

### Vue 条件渲染

`v-if` `v-else` `v-else-if`

### 焦点管理


