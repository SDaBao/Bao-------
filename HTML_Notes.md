[HTML入门](https://developer.mozilla.org/zh-CN/docs/Learn/HTML/Introduction_to_HTML/Getting_started)


HTML解释器会将连续出现的空白字符减少为一个单独的空格符
在HTML中，字符 <, >,",' 和 & 是特殊字符，可以通过等价字符引用代表


\<b>, \<i>, 和 \<u> 的情况却有点复杂。它们出现于人们要在文本中使用粗体、斜体、下划线但CSS仍然不被完全支持的时期。像这样的元素，仅仅影响表象而且没有语义，被称为表象元素（presentational elements）并且不应该再被使用



###描述列表
描述列表使用与其他列表类型不同的闭合标签— `<dl>`
此外，每一项都用 `<dt> `(description term) 元素闭合
每个描述都用` <dd> `(description definition) 元素闭合
```html
<dl>
  <dt>内心独白</dt>
    <dd>戏剧中，某个角色对自己的内心活动或感受进行念白表演，这些台词只面向观众，而其他角色不会听到。</dd>
</dl>
```
浏览器的默认样式会在描述列表的描述部分（description definition）和描述术语（description terms）之间产生缩进。

###引用
**块引用：**
[\<blockquote>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/blockquote) 代表其中的文字是引用内容
- cite 属性：标注引用的信息的来源文档或者相关信息的 URL

**行内引用：**
[\<q>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/q) 表示一个封闭的并且是短的行内引用的文本（长文本用 blockquote）
- cite 属性：值是 URL，意在指出被引用的文本的源文档或者源信息

[\<cite>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/cite) 表示一个作品的引用，且必须包含作品的标题
###缩略语
[\<abbr>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/abbr) 用来包裹一个缩略语或缩写
- title 属性：包含对一个缩写的扩写或者描述解释
###联系方式
[\<address>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/address) 标记编写HTML文档的人的联系方式
###上标下标
[\<sup>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/sup) 上标
[\<sub>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/sub) 下标
###计算机代码
- [\<code>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/code): 用于标记计算机通用代码。
- [\<pre>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/pre): 用于保留空白字符（通常用于代码块）——如果您在文本中使用缩进或多余的空白，浏览器将忽略它，您将不会在呈现的页面上看到它。但是，如果您将文本包含在`<pre></pre>`标签中，那么空白将会以与你在文本编辑器中看到的相同的方式渲染出来。
- [\<var>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/var): 用于标记具体变量名。
- [\<kbd>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/kbd): 用于标记输入电脑的键盘（或其他类型）输入。
- [\<samp>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/samp): 用于标记计算机程序的输出。
###时间日期
[\<time>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/time)
##文档&网站架构
###基本组成
- 页眉
- 导航栏
- 主内容
- 侧边栏
- 页脚
###构建内容的 HTML
- [\<header>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/header)：页眉
- [\<nav>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/nav)：导航栏
- [\<main>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/main)：主内容。主内容中还可以有各种子内容区段，可用`<article>`、`<section>` 和 `<div>` 等元素表示
- [\<aside>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/aside)：侧边栏，经常嵌套在 `<main>` 中
- [\<footer>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/footer)：页脚

###布局细节
[HTML 元素参考](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element)
**主要元素意义：**
>- `<main>` 存放每个页面独有的内容。每个页面上只能用一次 `<main>`，且直接位于 `<body>` 中。最好不要把它嵌套进其它元素。
>- `<article>` 包围的内容即一篇文章，与页面其它部分无关（比如一篇博文）。
>- `<section>` 与 `<article>` 类似，但 `<section>` 更适用于组织页面使其按功能（比如迷你地图、一组文章标题和摘要）分块。
一般的最佳用法是：以 标题 作为开头
>   - 也可以把一篇 `<article>` 分成若干部分并分别置于不同的 `<section>` 中
>   - 也可以把一个区段 `<section>` 分成若干部分并分别置于不同的 `<article>` 中，取决于上下文。
>- `<aside>` 包含一些间接信息（术语条目、作者简介、相关链接，等等）。
>- `<header>` 是简介形式的内容。如果它是 `<body>` 的子元素，那么就是网站的全局页眉。如果它是 `<article>` 或`<section>` 的子元素，那么它是这些部分特有的页眉（此 `<header>` 非彼 标题）。
>- `<nav>` 包含页面主导航功能。其中不应包含二级链接等内容。
>- `<footer>` 包含了页面的页脚部分。

**无语义元素**
- 内联无语义元素：[\<span>]()
- 块级无语义元素：[\<div>]()

**换行与水平分割线**
- 换行：\<br>
- 分割线：\<hr>

##HTML 调试
[Markup Validation Service](https://validator.w3.org/)
由 W3C（制定 HTML、CSS 和其他网络技术标准的组织） 创立并维护的标记验证服务。把一个 HTML 文档加载至本网页并运行 ，网页会返回一个错误报告。
#多媒体与嵌入
##图片
[\<img>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/img) 将一份图像嵌入文档
- src 属性：图片文件路径（必须）
- alt 属性：对图片的文本描述
- width&height 属性：为图片预留宽高
- title 属性：鼠标悬停提示
>像`<img>`和`<video>`这样的元素有时被称之为替换元素，因为这样的元素的内容和尺寸由外部资源（像是一个图片或视频文件）所定义，而不是元素自身
###文字说明
- [\<figure>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/figure) 代表一段独立的内容，经常与说明（caption） `<figcaption>` 配合使用，并且作为一个独立的引用单元
- [\<figcaption>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/figcaption) 与其相关联的图片的说明/标题，用于描述其父节点 `<figure>` 元素里的其他数据

**说明文字和 `alt` 的内容不应该一样**
###CSS 背景图片
```CSS
// 使用 CSS 嵌入图片
p {
  background-image: url("images/dinosaur.jpg");
}
```
CSS图片和HTML图片的区别：CSS图片用于装饰（没有语义上的意义，可以更好控制图片和设置图片位置；图像对内容有意义则应使用HTML图像

##音频和视频
- [\<audio>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/audio)
- [\<video>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/video)

##从对象到iframe - 其他嵌入技术
###早期流行使用框架创建网站
>嵌入如Flash、Java_Applet等技术是通过诸如`<object>`和较少使用`<embed>`的元素来实现的
但存在可访问性、安全性、文件大小等问题，大部分技术已经过时了

##iframe
[\<iframe>](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe) 提供了一种将整个web页嵌入到另一个网页的方法
```HTML
<iframe src="https://developer.mozilla.org/en-US/docs/Glossary"
        width="100%" height="500" frameborder="0"
        allowfullscreen sandbox>
  <p> <a href="https://developer.mozilla.org/en-US/docs/Glossary">
    Fallback link for browsers that don't support iframes
  </a> </p>
</iframe>
```
**基本属性**
- allowfullscreen
    >如果设置，`<iframe>`则可以通过全屏API设置为全屏模式（稍微超出本文的范围）。
- frameborder
    >如果设置为1，则会告诉浏览器在此框架和其他框架之间绘制边框，这是默认行为。0删除边框。不推荐这样设置，因为在CSS中可以更好地实现相同的效果。border: none;
- src
    >该属性与`<video>/<img>`一样包含指向要嵌入文档的URL路径。
- width 和 height
    >这些属性指定您想要的iframe的宽度和高度。
- 备选内容
    >与`<video>`等其他类似元素相同，您可以在`<iframe></iframe>`标签之间包含备选内容，如果浏览器不支持`<iframe>`，将会显示备选内容，这种情况下，我们已经添加了一个到该页面的链接。现在几乎不可能遇到任何不支持`<iframe>`的浏览器。
- sandbox
    >该属性需要在已经支持其他`<iframe>`功能（例如IE 10及更高版本）但稍微更现代的浏览器上才能工作，该属性可以提高安全性设置。

###iframe的安全问题
1. 只在必要时嵌入（安全与版权问题）
2. 使用HTTPS
    > HTTPS减少了远程内容在传输过程中被篡改的机会
    > HTTPS防止嵌入式内容访问您的父文档中的内容，反之亦然
    *绝对不能使用HTTP嵌入第三方内容，即src使用https链接*
3. 始终使用`sandbox`属性
    > 一个允许包含在其里的代码以适当的方式执行或者用于测试，但不能对其他代码库（意外或恶意）造成任何损害的容器称为**沙盒**
    > *永远不应该同时添加allow-scripts和allow-same-origin到你的sandbox属性中*
       > >在这种情况下，嵌入式内容可以绕过阻止站点执行脚本的同源安全策略，并使用JavaScript完全关闭沙盒
4. 配置CSP指令
    > CSP代表内容安全策略，它提供一组HTTP标头（由web服务器发送时与元数据一起发送的元数据），旨在提高HTML文档的安全性.
    > *将服务器配置为发送适当的X-Frame-Options 标题，这样可以防止其他网站在其网页中嵌入您的内容*

##\<embed>和\<object>元素
*用来嵌入多种类型的外部内容的通用嵌入工具。*
> 例如：Java小程序和 Flash，PDF 等插件技术。
> > **插件**是一种对浏览器原生无法读取的内容提供访问权限的软件

**插件属于近年来不常用的技术**

#矢量图形
##什么是矢量图形
**位图与矢量图比较：**
- **位图**使用像素网格来定义 — 一个位图文件精确得包含了每个像素的位置和它的色彩信息。流行的位图格式包括 Bitmap (.bmp), PNG (.png), JPEG (.jpg), and GIF (.gif.)
- **矢量图**使用算法来定义 — 一个矢量图文件包含了图形和路径的定义，电脑可以根据这些定义计算出当它们在屏幕上渲染时应该呈现的样子。 SVG 格式可以让我们创造用于 Web 的精彩的矢量图形。

##SVG格式
> SVG 是用于描述矢量图像的XML语言
SVG 用于标记图形，而不是内容

光栅图形与SVG
- SVG 优点：
    - 矢量图像中的文本仍然可访问（这也有利于 SEO）。
    - SVG 可以很好地适应样式/脚本，因为图像的每个组件都是可以通过CSS或通过JavaScript编写的样式的元素

- 缺点（对比光栅）：
    - SVG非常容易变得复杂，这意味着文件大小会增加; 复杂的SVG也会在浏览器中占用很长的处理时间。
    - SVG可能比栅格图像更难创建，具体取决于您尝试创建哪种图像。
    - 旧版浏览器不支持SVG，因此如果您需要在网站上支持旧版本的 IE，则可能不适合（SVG从IE9开始得到支持）。

*光栅图形更适合照片那样复杂精密的图像*

##添加SVG
###\<img> 标签嵌入
优点：
- 快速，熟悉的图像语法与`alt`属性中提供的内置文本等效。
- 可以通过在`<a>`元素嵌套`<img>`，使图像轻松地成为超链接。

缺点：
- 无法使用JavaScript操作图像。
- 如果要使用CSS控制SVG内容，则必须在SVG代码中包含内联CSS样式。 （从SVG文件调用的外部样式表不起作用）
- 不能用CSS伪类来重设图像样式（如:focus）。

###HTML 引入
*直接贴入，内联SVG*

优点：
- 将 SVG 内联减少 HTTP 请求，可以减少加载时间。
- 您可以为 SVG 元素分配`class`和`id`，并使用 CSS 修改样式，无论是在SVG中，还是 HTML 文档中的 CSS 样式规则。 实际上，您可以使用任何 SVG外观属性 作为CSS属性。
- 内联SVG是唯一可以让您在SVG图像上使用CSS交互（如`:focus`）和CSS动画的方法（即使在常规样式表中）。
- 您可以通过将 SVG 标记包在`<a>`元素中，使其成为超链接。

缺点:
- 这种方法只适用于在一个地方使用的SVG。多次使用会导致资源密集型维护（resource-intensive maintenance）。
- 额外的 SVG 代码会增加HTML文件的大小。
- 浏览器不能像缓存普通图片一样缓存内联SVG。
- 您可能会在`<foreignObject>` 元素中包含回退，但支持 SVG 的浏览器仍然会下载任何后备图像。你需要考虑仅仅为支持过时的浏览器，而增加额外开销是否真的值得。

###使用\<iframe>嵌入
缺点：
- 如你所知， `iframe`有一个回退机制，如果浏览器不支持`iframe`，则只会显示回退。
- 此外，除非 SVG 和您当前的网页具有相同的 origin，否则你不能在主页面上使用 JavaScript 来操纵 SVG。

#响应式图片
> 一种可以在不同的屏幕尺寸和分辨率的设备上都能良好工作以及其他特性的图片
CSS 比 HTML 更加适合做响应式设计
*响应式图片仅仅只是响应式web设计的一部分（奠定了响应式web设计的良好基础）*

##创建自适应图片
###使用 srcset 和 sizes 属性
```HTML
<!-- 实现分辨率切换 -->
<!-- 老旧的浏览器会忽略这些属性，并使用src加载图片 -->
<img srcset="elva-fairy-320w.jpg 320w,
             elva-fairy-480w.jpg 480w,
             elva-fairy-800w.jpg 800w"
     sizes="(max-width: 320px) 280px,
            (max-width: 480px) 440px,
            800px"
     src="elva-fairy-800w.jpg" alt="Elva dressed as a fairy">
```
###srcset 和 x 语法结合
```HTML

<!-- 浏览器计算显示器分辨率，选择合适图像 -->
<img srcset="elva-fairy-320w.jpg,
             elva-fairy-480w.jpg 1.5x,
             elva-fairy-640w.jpg 2x"
     src="elva-fairy-640w.jpg" alt="Elva dressed as a fairy">
```
###改用\<picture> *美术设计问题*
```HTML
<!-- <picture>素包含了一些<source>元素，使浏览器在不同资源间做出选择 -->
<picture>
  <source media="(max-width: 799px)" srcset="elva-480w-close-portrait.jpg">
  <source media="(min-width: 800px)" srcset="elva-800w.jpg">
  <img src="elva-800w.jpg" alt="Chris standing up holding his daughter Elva">
</picture>
```
**为什么我们不能使用 CSS 或 JavaScript 来做到这一效果?**
>当浏览器开始加载一个页面, 它会在主解析器开始加载和解析页面的 CSS 和 JavaScript 之前先下载 (预加载) 任意的图片。这是一个非常有用的技巧，平均下来减少了页面加载时间的20%。但是, 这对响应式图片一点帮助都没有, 所以需要类似 `srcset` 的实现方法。因为你不能先加载好 `<img>` 元素后, 再用 JavaScript 检测可视窗口的宽度，如果觉得大小不合适，再动态地加载小的图片替换已经加载好的图片，这样的话, 原始的图像已经被加载了, 然后你又加载了小的图像, 这样的做法对于响应式图像的理念来说，是很糟糕的。

**大胆使用现代图像格式**
> \<picture> 满足老式浏览器的需要，能立即拒绝其不支持的文件类型
```HTML
<picture>
  <source type="image/svg+xml" srcset="pyramid.svg">
  <source type="image/webp" srcset="pyramid.webp">
  <img src="pyramid.png" alt="regular pyramid built from four equilateral triangles">
</picture>
```
#HTML 表格
[\<table>](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/table) 表格标签
[\<td>](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/td) 单元格标签
[\<tr>](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/tr) table row 标签
[\<th>](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/th) （table header）标题标签


##单元格跨越多行/多列
使用 `colspan` 和 `rowspan` 属性

- colspan：
    包含一个正整数表示了每单元格中扩展单元格**宽度**的数量
- rowspan：
    包含一个正整数表示了每单元格中扩展单元格**高度**的数量

##列使用相同样式
使用 `<col>` 和 `<colgroup>` 元素
[\<col>](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/col)
[\<colgroup>](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/colgroup)

##其他表格元素
[\<caption>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/caption) 表格标题
[\<thead>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/thead) 定义了一组定义表格的列头的行
[\<tfoot>](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/tfoot) 一组表格中各列的汇总行
[\<tbody>](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/tbody) 封装一组`<tr>`元素，构成表格正文

##嵌套表格
在`<td>`元素中添加`<table>`
##视力受损优化
- `<th>`元素的`scope`属性
- `<th>`元素的`id`属性和`<td>`元素的`headers`属性
