##Web API
[Web_API 文档](https://developer.mozilla.org/zh-CN/docs/Web/API)
Web API 是浏览器提供的一套操作**浏览器功能**和**页面元素**的 API

##DOM
Document_Object_Module（文档对象模型）是W3C组织推荐的处理可扩展标记语言（HTML或XML）的标准编程接口。
通过DOM接口可以改变网页的内容、结构和样式
###DOM 树
- 文档 document：一个页面就是一个文档
- 元素 element：页面中的所有标签都是元素
- 节点 node：网页中的所有内容都是节点（标签、属性、文本、注释等）
DOM 把以上内容都看做对象

###获取元素（常用）
1. [getElementById()](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/getElementById)
2. [getElementsByTagName()](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/getElementsByTagName)
3. [getElementsByClassName()](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/getElementsByClassName) H5 新增
4. [querySelector('选择器')](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/querySelector) H5 新增
5. [querySelectorALL('选择器')](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/querySelectorAll) H5 新增
...

###事件
- 事件源
- 事件类型
- 事件处理程序

1. 获取事件源
2. 注册事件（绑定事件）
3. 添加事件处理程序（函数赋值）

####操作元素
- innerText （不识别HTML标签，非标准，去除空格和换行）
- innerHTML （识别HTML标签，W3C标准，保留空格和换行，使用最多）






