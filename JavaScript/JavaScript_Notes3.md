# WEB API
## JavaScript，API 和其他 JavaScript 工具
- **JavaScript**
一种内置于浏览器的高级脚本语言，您可以用来实现 Web 页面/应用中的功能。
- **客户端 API**
内置于浏览器的结构程序，位于 JavaScript 语言顶部，可以使开发者更容易地实现功能。
- **第三方 API**
置于第三方普通的结构程序，使开发者可以在自己的 Web 页面中使用那些平台的某些功能（例如在您的 Web 页面显示天气、地图等）。
- **JavaScript 库**
通常是包含具有特定功能的一个或多个 JavaScript 文件，把这些文件关联到您的 Web 页以快速或授权编写常见的功能。例如 jQuery 和 Mootools
- **JavaScript 框架**
从库开始的下一步，JavaScript 框架视图把 HTML、CSS、JavaScript 和其他安装的技术打包在一起，然后用来从头编写一个完整的 Web 应用。例如 Vue

## 常见的浏览器 API
- **操作文档的 API**
例如 DOM（文档对象模型）API，它允许您操作 HTML 和 CSS — 创建、移除以及修改 HTML，动态地将新样式应用到您的页面，等等。
- **从服务器获取数据的 API** 
用于更新网页的一小部分等功能。例如 Ajax，Fetch。您
- **用于绘制和操作图形的 API**
目前已被浏览器广泛支持，例如 Canvas 和 WebGL。实现绘制、动画、游戏等场景的搭建。
- **音频和视频 API**
例如HTMLMediaElement，Web Audio API和WebRTC，可以创建用于播放音频和视频的自定义 UI 控件，显示字幕字幕和您的视频，从网络摄像机抓取视频，或在网络会议中显示在别人的电脑上，或者添加音频效果等。
- **设备 API**
基本上是以对网络应用程序（webAPP）有用的方式操作和检索现代设备硬件中的数据的 API。例如，访问设备位置数据的地理定位 API，通过系统通知（参见Notifications API）或振动硬件（参见Vibration API）告诉用户 Web 应用程序有用的更新可用。
- **客户端存储 API**
可以使应用程序保存页面加载之间的状态，让设备在处于脱机状态时可用。例如使用Web Storage API 简单数据存储以及使用IndexedDB API 的更复杂的表格数据存储。

# DOM & BOM API
- `window` 是载入浏览器的标签
    >在 JavaScript 中用Window对象来表示，使用这个对象的可用方法，你可以返回窗口的大小（参见Window.innerWidth和Window.innerHeight），操作载入窗口的文档，存储客户端上文档的特殊数据（例如使用本地数据库或其他存储设备），为当前窗口绑定event handler，等等。
- `navigator` 表示浏览器存在于 web 上的状态和标识（即用户代理）
    >在 JavaScript 中，用Navigator来表示。你可以用这个对象获取一些信息，比如来自用户摄像头的地理信息、用户偏爱的语言、多媒体流等等。
- `document`（在浏览器中用 DOM 表示）是载入窗口的实际页面
    >在 JavaScript 中用Document 对象表示，你可以用这个对象来返回和操作文档中 HTML 和 CSS 上的信息。例如获取 DOM 中一个元素的引用，修改其文本内容，并应用新的样式，创建新的元素并添加为当前元素的子元素，甚至把他们一起删除。

## DOM
在浏览器标签中，当前载入的HTML文档用文本对象模型表示，是浏览器生成的**树结构**（DOM 树），便于编程语言访问。
文档中每个元素和文本在 DOM 树中都有它们自己的入口 — 称之为**节点**

- **元素节点**: 一个元素，存在于 DOM 中。
- **根节点**: 树中顶层节点，在 HTML 的情况下，总是一个HTML节点（其他标记词汇，如 SVG 和定制 XML 将有不同的根元素）。
- **子节点**: 直接位于另一个节点内的节点。
- **后代节点**: 位于另一个节点内任意位置的节点。
- **父节点**: 里面有另一个节点的节点。
- **兄弟节点**: DOM 树中位于同一等级的节点。
- **文本节点**: 包含文字串的节点

### 基于 DOM 的操作
**选择元素**
- `Document.querySelector()` 调用会匹配它在文档中遇到的第一个与选择器匹配的元素（可以使用多种选择器）
- `Document.querySelectorAll()` 可以选中所有匹配的元素标签，并存入数组中
- `Document.getElementById()`，选择一个id属性值已知的元素。
- `Document.getElementsByTagName()`，返回页面中包含的所有已知类型元素的数组

**创建结点**
- `Document.createElement()` 方法用于创建一个由标签名称 tagName 指定的 HTML 元素
- `Node.appendChild()` 方法将一个节点附加到指定父节点的子节点列表的末尾处。
    >如果被插入的节点已经存在于当前文档的文档树中，那么 appendChild() 只会将它从原先的位置移动到新的位置（不需要事先移除要移动的节点）
- `Document.createTextNode()` 创建一个新的文本节点。

**删除或移动元素**
- `Node.appendChild()` 被插入的节点已经存在于当前文档的文档树中，则为移动元素
- `Node.removeChild()` 方法从 DOM 中删除一个子节点。返回删除的节点。
- 删除仅自身引用的结点需要从父节点删除（先找到父节点，再删除该结点）

**操作 CSS 样式**
> 被放弃使用的方法 
使用 `Document.stylesheets` 返回 `CSSStyleSheet` 数组，获取绑定到文档的所有样式表的序列。然后添加/删除想要的样式。

常用的两种方法：
- `HTMLElement.style` 直接在想要动态设置样式的元素内部添加内联样式
- `Element.setAttribute()` 设置指定元素上的某个属性值，用于应用已定义的 CSS 样式 `para.setAttribute('class', 'highlight');`

## BOM 的操作
Window.innerWidth 和 Window.innerHeight 获取窗口大小


# Ajax API
通过网页请求获取数据的通用技术被称为Asynchronous JavaScript and XML（Ajax）

> 实现页面内容的部分加载，提高响应速度、节省带宽

```javascript
// XHR 方法
let request = new XMLHttpRequest();
request.open('GET', url);
request.responseType = 'text';

request.onload = function() {
  poemDisplay.textContent = request.response;
};

request.send();

// Fetch 方法
fetch(url).then(function(response) {
  response.text().then(function(text) {
    poemDisplay.textContent = text;
  });
});
```
# 客户端存储
大多数现代的 web 站点是动态的
> 在服务端使用各种类型的数据库来存储数据 (服务端存储), 之后通过运行服务端（server-side）代码来重新获取需要的数据，把其数据插入到静态页面的模板中，并且生成出 HTML 渲染到用户浏览上。

客户端存储可以用于：
- 个性化网站偏好（比如显示一个用户选择的窗口小部件，颜色主题，或者字体）。
- 保存之前的站点行为 (比如从先前的 session 中获取购物车中的内容， 记住用户是否之前已经登陆过)。
- 本地化保存数据和静态资源可以使一个站点更快（至少让资源变少）的下载， 甚至可以在网络失去链接的时候变得暂时可用。
- 保存 web 已经生产的文档可以在离线状态下访问。

存储工具：
- [cookies](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/cookie)
    是网络上最早最常用的客户端存储形式
    因为安全性、泛用性逐渐被弃用
- Web Storage API
    语法简单，用于存储和检索较小的、由名称和相应值组成的数据项。
    用于存储一些简单的数据，比如用户的名字，用户是否登录，屏幕背景使用了什么颜色等等。
- IndexedDB API
    为浏览器提供了一个完整的数据库系统来存储复杂的数据。
    可以用于存储从完整的用户记录到甚至是复杂的数据类型，如音频或视频文件。
- Cashe API
    存储特定 HTTP 请求的响应文件
    用于存储离线网站文件

## Web storage
所有的 web storage 数据都包含在浏览器内两个类似于对象的结构中： 
- sessionStorage
    关闭浏览器时数据会丢失
- localStorage
    会一直保存数据

Storage.setItem() 方法允许您在存储中保存一个数据项
Storage.getItem() 方法接受一个参数，检索数据项的名称，并返回数据项的值
Storage.removeItem() 方法接受一个参数，删除选中的数据项
```javascript
localStorage.setItem('name','Chris');
var myName = localStorage.getItem('name');
myName

localStorage.removeItem('name');
var myName = localStorage.getItem('name');
myName
```
## IndexedDB API
- 文本存储
- 音视频图像文件存储

## 离线存储
serviceWorker


