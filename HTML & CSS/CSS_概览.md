# CSS（层叠样式表）

层叠样式表 (Cascading Style Sheets，缩写为 CSS），是一种 样式表 语言，用来描述 HTML 或 XML（包括如 SVG、MathML、XHTML 之类的 XML 分支语言）文档的呈现。CSS 描述了在屏幕、纸质、音频等其它媒体上的元素应该如何被渲染的问题。

### 级联规则和专用规则

## CSS 属性和值

- 属性：人类可读的标识符，指示您想要更改的样式特征(例如font-size, width, background-color) 你想改变。
- 值：每个指定的属性都有一个值，该值指示您希望如何更改这些样式特性(例如，要将字体、宽度或背景色更改为。)

### 函数

*CSS 中属性的值可能以函数的形式出现*
例如：`calc()` 函数，`rotate()` 函数

## @规则

> @rules 是一些特殊的规则，为 CSS提供了一些关于如何表现的指导.
```css
/* 将额外的样式表导入主CSS样式表 */
@import 'styles2.css';
```
>@media，它允许您使用 媒体查询 来应用CSS，仅当某些条件成立(例如，当屏幕分辨率高于某一数量，或屏幕宽度大于某一宽度时)。

## 速记属性

>一些属性，如 font, background, padding, border, and margin 等属性称为速记属性--这是因为它们允许您在一行中设置多个属性值，从而节省时间并使代码更整洁。

```css
background: red url(bg-graphic.png) 10px 10px repeat-x fixed;
/* 上下部分代码等价 */
background-color: red;
background-image: url(bg-graphic.png);
background-position: 10px 10px;
background-repeat: repeat-x;
background-attachment: fixed;
```

## CSS工作方式

1. 浏览器载入HTML文件（比如从网络上获取）。
2. 将HTML文件转化成一个DOM（Document Object Model），DOM是文件在计算机内存中的表现形式，下一节将更加详细的解释DOM。
3. 接下来，浏览器会拉取该HTML相关的大部分资源，比如嵌入到页面的图片、视频和CSS样式。JavaScript则会稍后进行处理，简单起见，同时此节主讲CSS，所以这里对如何加载JavaScript不会展开叙述。
4. 浏览器拉取到CSS之后会进行解析，根据选择器的不同类型（比如element、class、id等等）把他们分到不同的“桶”中。浏览器基于它找到的不同的选择器，将不同的规则（基于选择器的规则，如元素选择器、类选择器、id选择器等）应用在对应的DOM的节点中，并添加节点依赖的样式（这个中间步骤称为渲染树）。
5. 上述的规则应用于渲染树之后，渲染树会依照应该出现的结构进行布局。
6. 网页展示在屏幕上（这一步被称为着色）。

## DOM 树形结构
>一个DOM有一个树形结构，标记语言中的每一个元素、属性以及每一段文字都对应着结构树中的一个节点（Node/DOM或DOM node）。节点由节点本身和其他DOM节点的关系定义，有些节点有父节点，有些节点有兄弟节点（同级节点）。

## 无法解析的CSS如何处理
>浏览器并不会同时实现所有的新CSS，此外很多人也不会使用最新版本的浏览器。鉴于CSS一直不断的开发，因此领先于浏览器可以识别的范围

**浏览器什么也不会做，继续解析下一个CSS样式**
同理，浏览器遇到无法解析的选择器，或直接忽略整个选择器规则
*错误的代码、不支持的代码，均会直接忽略，**不会报错***

# 层叠与构建
## 冲突规则
> 在某些时候，在做一个项目过程中你会发现一些应该产生效果的样式没有生效。通常的原因是你创建了两个应用于同一个元素的规则。**cascade**, 和它密切相关的概念是 **specificity**，决定在发生冲突的时候应该使用哪条规则。

*在默认情况下，一些 css 属性继承当前元素的父元素上设置的值，有些则不继承*

**1、层叠**
> **Stylesheets cascade（样式表层叠）**
简单的说，css规则的顺序很重要；当应用两条同级别的规则到一个元素的时候，写在后面的就是实际使用的规则。

**2、优先级**
- 一个元素选择器不是很具体，会选择页面上该类型的所有元素 
所以它的优先级就会低一些。
- 一个类选择器稍微具体点，它会选择该页面中有特定 `class` 属性值的元素
所以它的优先级就要高一点。

**3、继承**
*一些设置在父元素上的css属性是可以被子元素继承的，有些则不能*

例如：
- `color` `font-family` 属性，子元素继承
- `width` 属性不继承

## 继承
### 继承控制
控制继承通用属性值：
- inherit
设置该属性会使子元素属性和父元素相同。实际上，就是 "开启继承".
- initial
设置属性值和浏览器默认样式相同。如果浏览器默认样式中未设置且该属性是自然继承的，那么会设置为 inherit 。
- unset
将属性重置为自然值，也就是如果属性是自然继承那么就是 inherit，否则和 initial一样
- revert
将属性值还原为未更改时的值。*很少被浏览器支持*

## 层叠
出现冲突时，应用css规则影响因素：
1. 重要程度
2. 优先级
3. 资源顺序

**优先级计算**
一个选择器的优先级可以说是由四个部分相加 (分量)，可以认为是“个十百千” — 四位数的四个位数：

1. **千位**： 如果声明在 style 的属性（内联样式）则该位得一分。这样的声明没有选择器，所以它得分总是1000。
2. **百位**： 选择器中包含ID选择器则该位得一分。
3. **十位**： 选择器中包含类选择器、属性选择器或者伪类则该位得一分。
4. **个位**：选择器中包含元素、伪元素选择器则该位得一分。

| 选择器 | 千位 |	百位 |	十位 | 个位 |	优先级|
|--|:---:|:---:|:---:|:---:|:----:|
|h1|	0|	0|	0|  1|0001|
|h1 + p::first-letter|	0|	0|	0|	3|	0003|
|li > a[href*="en-US"] > .inline-warning|	0|	0|	2|	2|	0022|
|#identifier|	0|	1|	0|	0|	0100|
|内联样式|	1|	0|	0|	0|	1000|

**特殊的 CSS  `!important`**
用于覆盖优先级计算，在 CSS 样式定义后添加 *非特殊情况不使用*
```css
.better {
    background-color: gray;
    border: none !important;
}
```
> 覆盖 `!important` 唯一的办法就是另一个 `!important` 具有 相同优先级 而且顺序靠后，或者更高优先级。

## CSS位置的影响
>CSS声明的重要性取决于样式表中指定的——它让用户可以设置自定义样式表来覆盖开发人员定义的样式。

**相互冲突的声明将按以下顺序适用，后一种声明将覆盖前一种声明：**
1. 用户代理样式表中的声明(例如，浏览器的默认样式，在没有设置其他样式时使用)。
2. 用户样式表中的常规声明(由用户设置的自定义样式)。
3. 作者样式表中的常规声明(这些是我们web开发人员设置的样式)。
4. 作者样式表中的`!important`声明
5. 用户样式表中的`!important `声明


# 背景和边框
## 背景样式
- **颜色 `background-color`**
- **背景图片 `background-image`**

透明背景图片可同时显示背景颜色
```css
.b {
  background-image: url(star.png);
  background-color:red;

}
```
- **控制背景平铺 `background-repeat`**
  属性值用于控制背景图像平铺行为：
  - no-repeat — 不重复。
  - repeat-x —水平重复。
  - repeat-y —垂直重复。
  - repeat — 在两个方向重复。
- **背景图像大小 `background-size`**
  - 设置长度或百分比值，来调整图像的大小以适应背景
  - `cover` 关键字
  *等比缩放，使图像完全覆盖盒子区，图像可能显示不全*
  - `contain` 关键字
  *等比缩放，使盒子完全包围图像，盒子周围可能存在空隙*
- **背景图像定位 `background-position`**
  使用水平值、垂直值或相应关键字定位
- **渐变背景**
  使用像图像一样的 `background-image` 属性设置
  [CSS渐变生成器](https://cssgradient.io/)
- **[多个背景图像](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/Building_blocks/Backgrounds_and_borders#%E5%A4%9A%E4%B8%AA%E8%83%8C%E6%99%AF%E5%9B%BE%E5%83%8F)**
- **背景附加 `background-attachment`**
  控制背景的内容滚动效果
- **使用内容简写 `background`**
- **内容可访问性**
  图像/背景上文字内容的对比度
  图像指定背景颜色，保证图像未加载时文本清晰
  网页内容不能作为背景，背景仅提供装饰作用

## 边框
- 简写定义 `border`
- 边定义 `border-top`
- 细粒度定义 `border-top-width`
- 圆角实现 `border-radius`

# 文本处理
## [书写模式](https://developer.mozilla.org/zh-CN/docs/Web/CSS/writing-mode)
指定文本排列方向（上至下，左至右，右至左）
修改书写模式会影响内联布局和块级布局的表现形式
## [逻辑属性和逻辑值](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/Building_blocks/Handling_different_text_directions#%E9%80%BB%E8%BE%91%E5%B1%9E%E6%80%A7%E5%92%8C%E9%80%BB%E8%BE%91%E5%80%BC)
映射属性使用逻辑（logical）和相对变化（flow relative）代替了像宽`width`和高`height`一样的物理属性
**实现在不同书写模式下样式的匹配**

## 溢出
当盒子中的内容超过盒子的大小时会发生**溢出**
CSS 为了减少数据损失，不会隐藏盒子中的内容
> **溢出建立了块级排版上下文**
使用诸如scroll或者auto的时候，就建立了一个块级排版上下文

### `overflow`属性
属性默认值为 `visible` ，即显示溢出的内容
设为 `overflow: hidden` ，则隐藏溢出内容
`overflow: scroll` 则提供滚动条展示溢出内容
- 设置 `overflow-y: scroll` 仅在 y 轴方向滚动，x 轴同理
- 使用 `overflow: auto` ，浏览器自动判断内容溢出，添加滚动条

# [CSS的值与单位](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/Building_blocks/Values_and_units)
- 数字
  \<interger> 整数
  \<number> 小数
  \<dimension> 带附加单位的\<number>
  \<percentage> 百分比
- 长度
  - 绝对长度
    cm, mm, px ...
  - 相对长度
    em, ex, ch ...
    > em：父元素的字体大小（在列表中可被继承）
    rem：根元素的字体大小
- 百分比
  设为父元素大小百分比
- 颜色
  - 16进制RGB
  - RGB & RGBA 颜色（alpha通道）
  - HSL & HSLA 的值
- 图片
  - 图像文件
  - 渐变色
- 位置
  表示 2D 坐标，用于定位元素
- 字符串和标识符
  例如：使用标识符 `red` 表示颜色，生成内容 `content` 中的字符串
- CSS 函数
  例如：`url()`, `rgb()`, `calc()` ...

# CSS 尺寸
## 原始尺寸
图像的长宽会被作为原始尺寸
空的 `div` 标签没有尺寸
**元素的固有尺寸 — 由其所包含的内容决定**
## 设置具体尺寸
- 使用 `height` `width` 具体值（固定值或百分数）
- 使用百分数
*使用百分比设置内外边距时，值是以包含块的**内联尺寸**进行计算的，也就是元素的水平宽度*
## 设置最大最小值（min-和 max-尺寸）
例如：`max-width` 的常见用法为，在没有足够空间以原有宽度展示图像时，让图像缩小，同时确保它们不会比这一宽度大。

## 视口单位 view_port
使用 `vw` `vh` 单位，随用户窗口大小改变
*`1vh` 等于视口高度的 1%，`1vw`则为视口宽度的 1%*

# 图像、媒体和表单元素
## 替换元素
图像和视频被描述为**替换元素**，CSS 不能影响这些元素的内部布局，仅影响它们在页面上于其他元素中的位置
*替换元素在成为网格或者弹性布局的一部分时，有不同的默认行为*
## 调整图像大小
- 设置 `max-width: 100%`
- 使用 `object-fit` 属性，`cover` `contain` 值
## form 表单元素
[HTML Forms module](https://developer.mozilla.org/zh-CN/docs/Learn/Forms)
表单元素默认不会继承字体样式，需要设置继承属性才能继承父元素属性

```css
/* 表单初始化样式 */
button,
input,
select,
textarea {
  /* 开启父元素继承 */
  font-family: inherit;
  font-size: 100%;
  /* 实现统一体验 */
  box-sizing: border-box;
  padding: 0; margin: 0;
}

textarea {
  /* 防止IE默认显示滚动条 */
  overflow: auto;
} 
```

## 响应式设计
响应式网页设计（responsive web design，RWD）使Web页面更好地适应不同的屏幕尺寸
- 液态网格
- 液态图像
- 媒体查询

**响应式图像**
```css
img {
  max-width: 100%:
} 
```
**响应式排版**
- 媒体查询
- 视口单位

**视口 Meta 标签**
```HTML
<meta name="viewport" content="width=device-width,initial-scale=1">
```

### [媒体查询](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/CSS_layout/Media_queries)
```css
/* 仅在宽度大于800px的设备上应用样式 */
@media screen and (min-width: 800px) {
  .container {
    margin: 1em 2em;
  }
} 
```
### 灵活网格
在 float 布局中，通过使用像素并把布局转化为百分数的方式设计：
```css
/* target / context = result  */
.col {
  width: 6.25%; /* 60 / 960 = 0.0625 */
} 

```
### 现代布局技术
- 多列布局
- 弹性布局
- 网格布局

## 旧浏览器CSS支持
https://developer.mozilla.org/zh-CN/docs/Learn/CSS/CSS_layout/Supporting_Older_Browsers



# 其他
[HTML表格的样式化](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/Building_blocks/Styling_tables)
[调试CSS](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/Building_blocks/Debugging_CSS)
[组织CSS方法规范与部分工具](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/Building_blocks/Organizing)
[Sass——广泛应用的CSS扩展语言](https://www.sass.hk/)








