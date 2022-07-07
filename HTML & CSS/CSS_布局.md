# CSS 布局
## 正常布局流（normal flow）
正常布局流 (normal flow) 是指在不对页面进行任何布局控制时，**浏览器默认的 HTML 布局方式**。
### 默认情况下如何布局
**块级元素**：内容宽度是其父元素的 100%，其高度与其内容高度一致。
> 块级元素按照基于其父元素的书写顺序（默认值： horizontal-tb）的块流动方向（block flow direction）放置
> 每个块级元素会在上一个元素下面另起一行，它们会根据设置好的 margin 值分隔。
> 例如在中文，或者其他水平书写、自上而下从左往右的书写模式中，块级元素是垂直组织的。

**内联元素**： `height` `width` 与内容一致（无法设置，除非更改`display`属性为block或inline-block）
> 内联元素只其父级块级元素的宽度内有足够的空间，则会与其他内联元素、相邻的文本内容（或者被包裹的）被安排在同一行。
> 如果空间不够，溢出的文本或元素将移到新的一行。


### display 属性
**在 css 中实现页面布局的主要方法**
正常流中的所有内容都有一个`display`的值，用作元素的默认行为方式。
- 通过更改这一默认值，使元素成为内联元素或块级元素
- 使用 `display:flex` 和 `display:grid` 等属性，应用不同的布局模式

## 弹性盒子（Flexbox）
专用于创建横向或是纵向（行与列）的一维页面布局方法
使元素可以膨胀以填充额外的空间，收缩以适应更小的空间。
> CSS 布局中唯一可靠且跨浏览器兼容的创建工具只有 **浮动 `floats`** 和 **定位`positioning`**，但其在某些方面具有一定局限性。
>
>    **局限在于：**（难以或不能方便灵活地实现）
>- 在父内容里面垂直居中一个块内容。
>- 使容器的所有子项占用等量的可用宽度/高度，而不管有多少宽度/高度可用。
>- 使多列布局中的所有列采用相同的高度，即使它们包含的内容量不同。

### flex 模型
**flex 容器（flex container）**：设置了 `display: flex` 的元素（一般为父元素） 
**flex 项（flex item）**：在 flex 容器中表现为柔性的盒子的元素

当元素表现为 flex 框时，它们沿着两个轴来布局：
- **主轴（main axis）** 是沿着 flex 元素放置的方向延伸的轴（比如页面上的横向的行、纵向的列）
该轴的开始和结束被称为 main start 和 main end。
- **交叉轴（cross axis）** 是垂直于 flex 元素放置方向的轴。该轴的开始和结束被称为 cross start 和 cross end。

**`flex-direction` 属性**：指定主轴的方向，默认值是 `row`（按照默认语言方向排列，例如中英文为从左至右）

**弹性盒子换行实现**（解决内容行向溢出问题）：
- `flex-wrap: wrap;` 容器设置换行属性 
- `flex: 200px;` 子元素固定宽度

> *`flex-direction` 和 `flex-wrap` 的缩写形式 `flex-flow`*

### 动态尺寸
共有三个article元素，则利用下面的css样式会在满足最小宽度为200px的前提下，平均分配 1/4, 1/4, 2/4 的可用宽度。
```css
article {
  flex: 1 200px;
}

article:nth-of-type(3) {
  flex: 2 200px;
}
```
**[flex](https://developer.mozilla.org/zh-CN/docs/Web/CSS/flex) 属性缩写**，最多可以指定三个不同值。
- 无单位比例，`flex-grow`，flex 项 主尺寸 的 flex 增长系数。
- 无单位比例，`flex-shrink`，flex 元素的收缩规则。（一般用于溢出容器的 flex 项）
- 最小值，`flex-basis` ，flex 元素在主轴方向上的初始大小。

**实现水平垂直对齐（居中）**：
```css
/* div 元素垂直水平居中 */
div {
  display: flex;
  align-items: center; /* 垂直方向 */
  justify-content: space-around; /* 水平方向 */
}
```
`align-items` 控制 flex 项在交叉轴上的位置：
- 默认值 `stretch`，使所有 flex 项沿着交叉轴方向拉伸填充父容器。（父容器没有固定高度，会保持所有项高度一致）
- `center` 值使项保持其原有的高度，并在交叉轴居中。
- `flex-start` 或 `flex-end` 使 flex 项对齐交叉轴的开头或末尾。

`justify-content` 控制 flex 项在主轴上的位置
- 默认值 `flex-start`，这会使所有 flex 项都位于主轴的开始处对齐。
- `flex-end` ，使 flex 项向末尾对齐。
- `center` ，让 flex 项在主轴居中（元素四周不留空间）。
- `space-around` 使所有 flex 项沿着主轴均匀分布（在元素四周均匀留有一定空间）。
- `space-between`，类似于`space-around` ，但不在两端留下任何空间。

### flex 项排序
可以通过 `order` 改变 flex 项排布顺序（不影响DOM树）
> 所有 flex 项默认的 order 值是 0
order 值大的 flex 项比 order 值小的在显示顺序中更靠后

### flex 嵌套
设置一个元素为 flex 项，这一元素成为 flex 容器，它的孩子 (直接子节点) 也表现为 flexible box

### 浏览器兼容性
支持大多数浏览器
部分老旧的浏览器不支持弹性盒子（或只支持老旧版本的弹性盒子）
**需要测试，避免布局的不可用**

## 网格布局 Grid
CSS 网格是一个用于 web 的二维布局系统。
利用网格，可以把内容按照行与列的格式进行排版。
网格通常具有许多的**列（column）**与**行（row）**，以及行与行、列与列之间的间隙（通常被称为**沟槽（gutter）**）
> 网格排版框架一般由 12 到 16 列的网格构成
可以通过网格系统直接实现

### 定义网格 `display: grid;`
> 网页并不会因为变为网格布局而发生变化，定义只创建了一个单列的网格，子项在表现形式上依然是 Normal Flow

添加列的定义：`grid-template-columns: 200px 200px 200px;`，则子项会被排进新定义的网格中

**fr 网格单位**
使用 `fr` 单位可以灵活定义网格行与列的大小（表示可用空间的比例）
```css
.container {
    display: grid;
    grid-template-columns: 2fr 1fr 1fr;
    /* 按照 2:1:1 的比例排布网格 */
}
```
**网格间隙**
`grid-gap: 20px;` 定义网格间的距离
- grid-column-gap  定义列间隙
- grid-row-gap 来定义行间隙

*在曾经的标准中 `gap` 属性有 `grid-` 前缀，可以写上两个属性保障代码的泛用性*

**使用 `repeat()` 构建重复的行列**
```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-gap: 20px;
}
```
第一个传入 repeat 函数的值（3）表明了后续列宽的配置要重复多少次
第二个值可以传入多个长度设定（传入的设定会被重复 n 次）

**显式网格与隐式网格**
显式网格：用 `grid-template-columns` 或 `grid-template-rows` 属性创建的
隐式网格：当有内容被放到网格外时才会生成的
> 隐式网格中生成的行/列大小是参数默认是 `auto`（大小自动调整，也可以手动设置`grid-auto-rows`和`grid-auto-columns`）

**minmax() 函数**
`grid-auto-rows: minmax(100px, auto);`
设置尺寸至少为 100px ，超过则自动调整

`grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));`
实现多列的自动填充

### 基于线放置元素
根据这些分隔线来放置元素，通过以下属性来指定从那条线开始到哪条线结束。
- `grid-column`
    - `grid-column-start`
    - `grid-column-end`
- `grid-row`
    - `grid-row-start`
    - `grid-row-end`

*使用缩写形式开始与结束的线的序号要使用`/`符号分开*
```css
header {
    /* 占据网格第1行的1-3列 */
    grid-row: 1;
    grid-column: 1 / 3;
}
```

### 使用 `grid-template-areas` 属性放置元素
`grid-template-areas` 属性的使用规则：

- 你需要填满网格的每个格子
- 对于某个横跨多个格子的元素，重复写上那个元素 `grid-area` 属性定义的区域名字
- 所有名字只能出现在一个连续的区域，不能在不同的位置出现
- 一个连续的区域必须是一个矩形
- 使用 `.` 符号，让一个格子留空
```css
.container {
  display: grid;
  grid-template-areas:
      "header header"
      "sidebar content"
      "footer footer";
  grid-template-columns: 1fr 3fr;
  grid-gap: 20px;
}

header {
  grid-area: header;
}

article {
  grid-area: content;
}

aside {
  grid-area: sidebar;
}

footer {
  grid-area: footer;
}
```

## 浮动布局
`float` 属性最初只用于在成块的文本内浮动图像，但是现在它已成为在网页上创建多列布局的最常用工具之一。
**浮动元素**会脱离正常的文档布局流，并吸附到其父容器的左边。
*浮动元素遵循盒子模型中的外边距和边界规则*

实现段落首字下沉：
```css
/* 实现段落的首字母字体放大2倍下沉 */
p::first-letter {
    font-size: 2em;
    float: left;
    /*padding: 2px;
    margin-right: 4px;
    border: 1px solid black;
    background: red; */
}
```
### 多列浮动布局
浮动通常用于创建多个列布局，并被浏览器广泛支持
**两列、三列布局**
布局样式：36% + 4% +30% + 4% + 26% = 100%
```css
div:nth-of-type(1) {
    width: 36%;
    float: left;
}

div:nth-of-type(2) {
    width: 30%;
    float: left;
    margin-left: 4%;
}

div:nth-of-type(3) {
    width: 26%;
    float: right;
}
```

### 清除浮动
使用浮动属性会使浮动元素下方不浮动的内容围绕浮动元素排布，导致排版错乱
例如：footer元素，需要清除浮动
```CSS
footer {
  clear: both;
}
```
`clear` 属性：
- `left`：停止任何活动的左浮动
- `right`：停止任何活动的右浮动
- `both`：停止任何活动的左右浮动

### 浮动的问题
- 导致宽度难以计算
- 浮动项目的背景高度不固定，不同列高度不统一，会根据页面变化
- 布局复杂后，清除浮动会变复杂

## 定位
定位可以使在正常的文档流布局中的元素，具有不同的行为。
例如放在另一个元素的上面，或者始终保持在浏览器视窗内的同一位置。

### 文档流
盒模型
Normal Flow
内联元素与块级元素
外边距折叠
### 定位实现
定位的思想是允许我们实现覆盖基本文档流行为
`position` 属性

- **静态定位 `position: static;`**
静态定位是默认的

- **相对定位 `position: relative;`**
行为类似于静态定位，依靠 `top`, `bottom`, `left`, 和 `right` 属性精确定位
位移一定相对距离

- **绝对定位 `position: absolute;`**
绝对定位的元素不再存在于正常文档布局流中
用于创建不干扰其他元素的 UI

**定位上下文**
如果所有的父元素都没有显式地定义 position 属性，即所有的父元素默认 position 属性都是 static。那么，绝对定位元素会被包含在**初始块容器**中。
> 初始块容器有着和浏览器视口一样的尺寸

可以通过改变**定位上下文**（绝对定位的元素的相对位置元素）
如：设置父元素的定位属性为相对定位，那么子元素的定位是相对于父元素的绝对定位。

### 改变层次顺序 `z-index`
元素开始重叠后，决定元素上下层次的因素
默认顺序：DOM 顺序中，排序较后的元素将位于之前的元素的上方

定位的元素都具有 z-index 为 auto，实际上为 0
修改以改变堆叠顺序： `z-index: 1;` 
- z-index 只接受无单位索引值
- 较高的值在层次上将高于较低的值

### 固定定位 `position: fixed;`
**与绝对定位区别：**
绝对定位固定元素：相对于 HTML 元素或其最近的定位祖先
固定定位固定元素：相对于浏览器视口本身

### `position: sticky`
*较新的功能*
允许被定位的元素表现得像相对定位一样，直到它滚动到某个阈值点为止，变为固定。
例如：使导航栏在页面滚动到特定点后，固定在页面顶部

## 多列式布局
创建一个三列的布局，具有弹性宽度，浏览器自动计算分配空间
```css
.container {
  column-count: 3;
}
```
`column-width: 200px;` 设定列宽度，浏览器会根据页面宽度创建尽可能多的列

**其他多列样式**
- 使用 `column-gap` 改变列间间隙。
- 用 `column-rule` 在列间加入一条分割线。
- `break-inside: avoid;` 或 `page-break-inside: avoid;` 避免元素在分列中折断