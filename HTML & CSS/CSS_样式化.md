# 样式化文字
## 字体样式
- **颜色** `color` 属性
- **字体种类** `font-family` 属性
    >[网页安全字体](https://zh.wikipedia.org/wiki/%E7%B6%B2%E9%A0%81%E6%A0%B8%E5%BF%83%E5%AD%97%E5%9E%8B)：可以应用到所以系统的字体。
    [网页安全字体查询网站](https://www.cssfontstack.com/)
    **默认字体**：serif（衬线字体）, sans-serif（无衬线字体）, monospace（等宽字体）, cursive（手写体）,和 fantasy（艺术、装饰体）
- **字体栈**
    提供**字体栈（font stack）**供浏览器选择可用字体
    ```css
    p {
        font-family: "Trebuchet MS", Verdana, sans-serif;
    }
    ```
- **字体大小** `font-size` 属性
- **字体样式** `font-style` 属性
    - `normal` 普通文字（取消斜体设置）
    - `italic` 设为斜体（不可以将使用 oblique 模拟斜体）
    - `oblique` 模拟斜体
- **字重** `font-weight` 属性 设置文本粗体大小
- **文本转换** `text-transform`
    - none 禁止转换
    - uppercase lowercase 转换为大小写
    - capitalize 首字母大写
    - full-width 转换为全角
- **文本装饰** `text-decoration` （可同时接收多个值）
    - none 取消装饰
    - underline overline 上、下划线
    - line-through 删除线
- **文本阴影** `text-shadow`
## 文本布局
常用属性
- 对齐 `text-align`
    - left right 左右对齐
    - center 居中对齐
    - justify 两端对齐
- 行间距 `line-height` *设置无单位的值表示行间距为字体大小倍数*
- 字母间距 `letter-spacing` `word-spacing`

...

## 列表
- 列表间距
- 列表样式 `list-style` 支持传入多个值
    - `list-style-type` ：设置用于列表的项目符号的类型，例如无序列表的方形或圆形项目符号，或有序列表的数字，字母或罗马数字。
    - `list-style-position` ：设置在每个项目开始之前，项目符号是出现在列表项内，还是出现在其外。
    - `list-style-image` ：允许您为项目符号使用自定义图片，而不是简单的方形或圆形。
- 列表计数管理
    - start 属性设置开始值
    - reversed 属性设置倒序
    - value 属性设置指定值
## 链接
- 链接状态 使用伪类应用样式
    - Link (没有访问过的)
    链接默认状态，可以使用 `:link` 伪类来应用样式。
    - Visited
    链接已经访问 (存在于浏览器的历史纪录), 可以使用 `:visited` 伪类来应用样式。
    - Hover: 鼠标光标停留在链接上时，可以使用 `:hover` 伪类来应用样式。
    - Focus
    被选中的时候 (比如通过键盘的 Tab 移动到这个链接的时候，或者使用编程的方法来选中这个链接 HTMLElement.focus() ) 可以使用 `:focus` 伪类来应用样式。
    - Active
    链接被激活的时候 (比如被点击的时候)，可以使用 `:active` 伪类来应用样式。
- 默认样式
- 链接中使用图标 `background`
- 样式化链接为按钮

## Web 字体
在线字体服务
在线字体应用
```css
@font-face {
  font-family: "myFont";
  src: url("myFont.ttf");
}

```




