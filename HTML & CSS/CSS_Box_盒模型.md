# 盒模型
完整的 CSS 盒模型应用于块级盒子，内联盒子只使用盒模型中定义的部分内容。
>模型定义了盒的每个部分 —— margin, border, padding, and content —— 合在一起就可以创建我们在页面上看到的内容。
## 块级盒子（Block box） 和 内联盒子（Inline box）
在 CSS 中我们广泛地使用两种“盒子” —— **块级盒子 (block box)** 和 **内联盒子 (inline box)**。这两种盒子会在 **页面流 (page flow)** 和元素之间的关系方面表现出不同的行为：

**Block box 的行为：**

- 盒子会在内联的方向上扩展并占据父容器在该方向上的所有可用空间，在绝大数情况下意味着盒子会和父容器一样宽
- 每个盒子都会换行
- width 和 height 属性可以发挥作用
- 内边距（padding）, 外边距（margin）和 边框（border）会将其他元素从当前盒子周围“推开”

*除非特殊指定，诸如标题 (`<h1>`等) 和段落 (`<p>`) 默认情况下都是块级的盒子。*

**Inline box 的行为：**
- 盒子不会产生换行。
- width 和 height 属性将不起作用。
- 垂直方向的内边距、外边距以及边框会被应用但是不会把其他处于 inline 状态的盒子推开。
- 水平方向的内边距、外边距以及边框会被应用且会把其他处于 inline 状态的盒子推开。

*用做链接的 `<a>` 元素、 `<span>`、 `<em>` 以及 `<strong>` 都是默认处于 inline 状态的。*

## 内部和外部显示类型

> 我们通过对盒子 `display `属性的设置，比如 `inline` 或者 `block` ，来控制盒子的外部显示类型。

外部显示类型：决定盒子是块级还是内联。
内部显示类型：决定了盒子内部元素是如何布局的。
## 盒模型组成
- Content box: 这个区域是用来显示内容，大小可以通过设置 width 和 height.
- Padding box: 包围在内容区域外部的空白区域； 大小通过 padding 相关属性设置。
- Border box: 边框盒包裹内容和内边距。大小通过 border 相关属性设置。
- Margin box: 这是最外面的区域，是盒子和其他元素之间的空白区域。大小通过 margin 相关属性设置。
### 标准盒模型 *content box*
在标准模型中，如果你给盒设置 `width` 和 `height`，实际设置的是 content box。 
padding 和 border 再加上设置的宽高一起决定整个盒子的大小。

### IE（替代 / 怪异）盒模型 *border box*
内容宽度是该宽度减去边框和填充部分

设置所有box使用替代模式
```css
html {
  box-sizing: border-box;
}
*, *::before, *::after {
  box-sizing: inherit;
}
```

## 内外边距、边框
**外边距**是盒子周围一圈看不到的空间。它会把其他元素从盒子旁边推开。外边距属性值可以为正也可以为负。设置负值会导致和其他内容重叠。无论使用标准模型还是替代模型，外边距总是在计算可见部分后额外添加。
**外边距折叠**：如果你有两个外边距相接的元素，这些外边距将合并为一个外边距，即最大的单个外边距的大小。
```css
.box {
  margin-top: -40px;
  margin-right: 30px;
  margin-bottom: 40px;
  margin-left: 4em;
  /* 两种定义方式均可用 */
  margin:-40px 30px 40px 4em;
}
```

**边框**
可以使用 `border` 属性一次设置所有四个边框的宽度、颜色和样式。
也可以使用 `border-top` `border-right` `border-bottom` `border-left` 分别设置每一条边
也可以直接设置所有边的颜色、样式或宽度：`border-width` `border-style` `border-color`
以及全部单独设置，例如：`border-top-width`

**内边距**位于边框和内容区域之间。与外边距不同，您不能有负数量的内边距，所以值必须是 0 或正的值。应用于元素的任何背景都将显示在内边距后面，内边距通常用于将内容推离边框。
`padding-top` `padding-right` `padding-bottom` `padding-left`

## 内联盒子模型
部分方法使用，例如：边距、边框和内边距
*宽度、高度不适用*

### display: inline-block
- 设置 `width` 和 `height` 属性会生效。
- `padding`, `margin`, 以及 `border` 会推开其他元素。

*适用于导航栏中*