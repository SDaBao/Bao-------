# Document

## 浏览器环境

### DOM 文档对象模型

`document` 对象是页面的主要入口

- DOM 不只用于浏览器，还可用于服务端
- CSSOM 用于 CSS 规则和样式表，修改文档样式规则时，CSSOM 和 DOM 同时使用

### BOM 浏览器对象模型

浏览器（主机环境）提供的用于处理*除文档之外*的所有内容的其他对象

- HTML 规范的一部分

## DOM 树

每个 HTML 标签都是一个对象，所有这些对象都可以通过 JS 访问。

DOM 将 HTML 表示为标签的树形结构，

- 标签为元素节点
- 元素内文本为文本节点
- HTML 中的所有内容都在 DOM 中，包括注释、!DOCTYPE

> 特殊情况：head 前的空格和换行符均被忽略，body 标签结束后的内容会被移动到 body 内

## 遍历 DOM

`document` 对象是 DOM 的入口

`<html>` = `document.documentElement`

`<body>` = `document.body` （值可能为 null，例如在 head 中的 script 运行时浏览器还未解析到 body）

`<head>` = `document.head`

> 对于某些 DOM 元素，例如 table，提供了用于访问其内容的其他属性和集合

### 子节点

- `childNodes` 集合（类数组可迭代对象）列出所有子节点（包括文本节点）
- `firstChild` `lastChild` 属性，能够访问第一个和最后一个子元素
- `elem.hasChildNodes()` 用于检查节点是否有子节点

> DOM 集合是类数组可迭代对象，不能通过下标访问，也没有数组的方法，但可以使用 `Array.from()` 将其转化为数组。是只读的、实时的，不建议使用 `for...in` 遍历

### 兄弟节点和父节点

- 下一个兄弟节点 `nextSibling` 属性，上一个兄弟节点 `previousSibling`
- `parentNode` 访问父节点属性

### 元素节点

- `children` —— 仅那些作为元素节点的子代的节点
- `firstElementChild`，`lastElementChild` —— 第一个和最后一个子元素
- `previousElementSibling`，`nextElementSibling` —— 兄弟元素
- `parentElement` —— 父元素（与 `parentNode` 的区别仅在 `document.documentElement` 上，根节点的父节点是 `document`，但其不是元素节点）

## 搜索、检查元素

- getElement* 返回**实时**的集合
  - `elem.getElementsByTagName(tag)`
  - `elem.getElementsByClassName(className)`
  - `document.getElementById(name)`
  - `document.getElementsByName(name)`
- querySelector* 返回**静态**的集合
  - `elem.querySelector(css)` 匹配的第一个元素
  - `elem.querySelectorAll(css)` 匹配的所有元素
- `elem.matches(css)` 检查是否与选择器匹配（true/false）
- `elem.closest(css)` 查找与选择器匹配的最近祖先（包括自己）

## 节点属性

- DOM 节点是常规的 JS 对象，使用基于原型的类进行继承，其属性和方法都是继承的结果。
- 主要 DOM 节点属性：
  - `nodeType` 可以使用它来查看节点是文本节点还是元素节点。它具有一个数值型值（numeric value）：1 表示元素，3 表示文本节点，其他一些则代表其他节点类型。只读。
  - `nodeName/tagName` 用于元素名，标签名（除了 XML 模式，都要大写）。对于非元素节点，nodeName 描述了它是什么。只读。
  - `innerHTML` 元素的 HTML 内容。可以被修改。
  - `outerHTML` 元素的完整 HTML。对 elem.outerHTML 的写入操作不会触及 elem 本身。而是在外部上下文中将其替换为新的 HTML。
  - `nodeValue/data` 非元素节点（文本、注释）的内容。两者几乎一样，我们通常使用 data。可以被修改。
  - `textContent` 元素内的文本：HTML 减去所有 <tags>。写入文本会将文本放入元素内，所有特殊字符和标签均被视为文本。可以安全地插入用户生成的文本，并防止不必要的 HTML 插入。
  - `hidden` 当被设置为 true 时，执行与 CSS display:none 相同的事。

## DOM 的 Attributes & properties

特性（attribute）—— 写在 HTML 中的内容。
属性（property）—— DOM 对象中的内容。

- DOM 节点作为常规的 JS 对象，可以像常规对象一样添加属性和方法
- 解析 HTML 时，浏览器会辨别**标准的特性**并以此创建 DOM 属性
  - `elem.hasAttribute(name)` 检查特性是否存在
  - `elem.getAttribute(name)` 获取这个特性值
  - `elem.setAttribute(name, value)` 设置这个特性值
  - `elem.removeAttribute(name)` 移除这个特性
  - `elem.attributes` 所有特性的集合
- 特性（attribute）对大小写不敏感，值为字符串类型
- 属性和特性是同步的（特例除外，特性可更新属性，属性不一定影响特性）
- 特性是字符串类型，但属性不一定是字符串类型，也不一定完全相同（如 style, checked，a 标签的属性是完整的url，而特性可能是相对路径或哈希值）
- 非标准的特性（dataset）用于将自定义数据从 HTML 传递到 JS 或设置样式
  - 所有以 “data-” 开头的特性均被保留供程序员使用。它们可在 `dataset` 属性中使用。

## 修改文档

- 创建元素元素 `document.createElement(tag)`
- 创建文本节点 `document.createTextNode(text)`
- 插入方法（字符串自动转化为文本节点，且特殊字符会被转义）
  - `node.append(...nodes or strings)` 末尾 插入节点或字符串
  - `node.prepend(...nodes or strings)` 开头 插入节点或字符串
  - `node.before(...nodes or strings)` 前面 插入节点或字符串
  - `node.after(...nodes or strings)` 后面 插入节点或字符串
  - `node.replaceWith(...nodes or strings)` 替换为 节点或字符串
  - `elem.insertAdjacentHTML/Text/Element(where, html)`
    - `where` 属性值 `"beforebegin"` `"afterbegin"` `"beforeend"` `"afterend"` 与 node 插入位置对应
- 移除节点 `node.remove()`，移动节点不需要删除
- 克隆节点 `elem.cloneNode(true)` 深克隆（包括特性和子元素），false 则不包括子元素
- `DocumentFragment` 传递节点列表的包装器（wrapper）

- 旧式的方法：
  - parent.appendChild(node)
  - parent.insertBefore(node, nextSibling)
  - parent.removeChild(node)
  - parent.replaceChild(newElem, node)
- `document.write(html)` 页面加载完成前添加 HTML 到页面（加载完成后运行会擦除文档）

## 样式和类

