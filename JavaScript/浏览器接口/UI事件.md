# UI 事件

## 鼠标事件

- 事件类型
  - mousedown/mouseup 在元素上点击/释放鼠标按钮。
  - mouseover/mouseout 鼠标指针从一个元素上移入/移出。
  - mousemove 鼠标在元素上的每个移动都会触发此事件。
  - click 如果使用的是鼠标左键，则在同一个元素上的 mousedown 及 mouseup 相继触发后，触发该事件。
  - dblclick 在短时间内双击同一元素后触发。
  - contextmenu 在鼠标右键被按下时触发。（其他方法打开菜单也会触发）
- 鼠标按钮 `event.button` 属性：与点击相关事件都具有此属性，可以获取准确的鼠标按钮。
- 组合键：shift，alt，ctrl，meta
  - 组合键属性：`shiftKey` `altKey`（对于 Mac 是 Opt）`ctrlKey` `metaKey`（对于 Mac 是 Cmd）

  > Mac 上常用 Cmd 代替 Crtl，所以需要检查 `if (event.ctrlKey || event.metaKey)`
- 坐标
  - 相对于窗口的坐标：clientX 和 clientY。
  - 相对于文档的坐标：pageX 和 pageY。
- 防止双击的副作用（双击后会产生选中文本的副作用），阻止 mousedown 默认行为
- 防止复制：`oncopy` 事件

## 移动鼠标

- `mouseover` `mouseout`
  - `relatedTarger` 属性，两种事件中表示鼠标从一个元素到另一元素切换的另一元素（相对于 `event.target`）。
    - 值为 null 表示来自窗口外或离开窗口
  - 跳过元素：鼠标快速移动、突然出现在窗口上会导致移动时元素被跳过，如果出发了 `mouseover` 则必然会有 `mouseout`
  - 移动到子元素上的 `mouseover` 事件会冒泡到父元素上被处理
- `mouseenter/mouseleave`
  - 与 `mouseover/mouseout` 区别:
    - 元素内部与后代之间的转换不会产生影响
    - 事件不会冒泡
- 事件委托

## 拖放事件






