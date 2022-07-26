# CSS 选择器

> CSS选择器是CSS规则的第一部分.它是元素和其他部分组合起来告诉浏览器哪个HTML元素应当是被选为应用规则中的CSS属性值的方式。
选择器所选择的元素，叫做“选择器的对象”.

## CSS 选择器种类

选择器和选择符可以同时使用

### [类型、类和 id 选择器](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/Building_blocks/Selectors/Type_Class_and_ID_Selectors)

标签（类型 / 元素）选择器

```css
/* 同时选择 p 标签和 li 标签 */
p, li {
    color: green;
}
```

类选择器

```CSS
.special {
  color: orange;
  font-weight: bold;
}
```

id选择器

```CSS
#intro {
    font-weight:bold;
}
```

通配选择器全局选择器
选择全部元素

```CSS
* {
    font-weight:bold;
}
```

### [标签属性选择器](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/Building_blocks/Selectors/Attribute_selectors)

根据一个元素上的某个标签的属性是否存在以选择元素，或者根据一个有特定值的标签属性是否存在来选择
存在与否、值选择器，子字符串匹配选择器，是否大小写敏感

### [伪类与伪元素](https://developer.mozilla.org/zh-CN/docs/Learn/CSS/Building_blocks/Selectors/Pseudo-classes_and_pseudo-elements)

**伪类选择器用于样式化一个元素的特定状态**
简单伪类、用户行为伪类；

:hover伪类会在鼠标指针悬浮到一个元素上的时候选择这个元素

```css
/* 鼠标悬停移除下划线 */
a:hover {
  text-decoration: none;
}
```

**伪元素用于选择一个元素的某个部分而不是元素自己**
::first-line是会选择一个元素中的第一行

**使用`::before` `::after` 生成内容**
在内容前后插入`content`，实现“生成内容”

### 关系选择器 / 选择运算符

>使用关系选择器，选择文档中的明确部分，会导致 CSS 规则*难以复用*。通常使用建立类的方法，应用到元素上。
关系选择器适合用于无法编辑 HTML 的情况。

**后代运算符/包含选择符** `article p`

```css
/* 仅选择嵌套在 <li> 元素内的 <em> */
li em {
  color: rebeccapurple;
}
```

**子代选择符** `article > p`
选择直接子元素

**邻接兄弟**选择符 `h1 + p`
选择恰好处于另一个在继承关系上同级的元素旁边的物件

```css
/* 选择紧紧相邻的两个标签元素中的 第二个元素 的样式 */
h1 + p {
  font-size: 200%;
}
```

**通用兄弟**选择器 `h1 ~ p`
选择一个元素的兄弟元素
