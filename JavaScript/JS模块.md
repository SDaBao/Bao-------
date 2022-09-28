# 模块

JS 语言级的模块为 ES6 标准

历史上的模块系统：

- AMD —— 最古老的模块系统之一，最初由 require.js 库实现。
- CommonJS —— 为 Node.js 服务器创建的模块系统。
- UMD —— 另外一个模块系统，建议作为通用的模块系统，它与 AMD 和 CommonJS 都兼容。

## 模块功能

- export 关键字标记了可以从当前模块外部访问的变量和函数。
- import 关键字允许从其他模块导入功能。

- 使用方法：`<script type="module">`
- 模块只通过 HTTP(s) 工作

核心功能：

- 始终使用 “use strict” 严格模式
- 模块级作用域
  - 模块使用导入导出而不是依赖全局变量
  - 但也可以为 `window` 添加属性，将其作为全局变量
- 模块代码仅在第一次导入时被解析
  - 同一个模块被导入到多个位置，代码**只会执行一次**，并将导出的内容提供给进一步导入
- `import.meta` 对象包含关于当前模块的信息，内容取决于其所在环境
- 在模块中，顶级 this 是 undefined，而非模块脚本是全局对象

浏览器特定功能：

- 模块脚本是延迟的，与 `defer` 特性影响相同
- 模块脚本中 `async` 也适用于内联脚本
- 模块的外部脚本
  - 具有相同 src 的只运行一次
  - 从另一个源获取的外部脚本需要 CORS header
- 浏览器中 `import` 必须给出相对或绝对路径（不允许裸模块）
- 使用 `nomodule` 实现兼容旧浏览器（`type="module"` 未知类型的脚本会被忽略）

### 构建工具

浏览器模块通常使用 WebPack 等工具打包部署

打包工具优势：控制模块的解析方式、允许裸模块、提供更多功能如 CSS/HTML 模块

转化与优化：

- 删除无法访问的代码。
- 删除未使用的导出（“tree-shaking”）。
- 删除特定于开发的像 console 和 debugger 这样的语句。
- 可以使用 Babel 将前沿的现代的 JavaScript 语法转换为具有类似功能的旧的 JavaScript 语法。
- 代码压缩（删除空格，用短的名字替换变量等）。

## 导出和导入

- 在声明时添加 `export` 关键字导出
- 导出与声明分离，声明后导出
- `import {...} from ...` `import * from ...`
- `import as` `export as`
- `export default` 默认的导出
  > 用于导出实体，如 class 或 function（一个模块只有一个默认导出，可以不指定名称）
  - `default` 关键词可被用于引用默认导出

### 重新导出

```JS
import User from './user.js';
export {User};

// 简写形式
export {sayHi} from './say.js';

// 默认导出需要特殊处理
export * from './user.js'; // 重新导出命名的导出
export {default} from './user.js'; // 重新导出默认的导出
```

导入内容并立即导出，实现包文件的不同模块，在一个入口文件中能够统一导出。

## 动态导入

> 实现按需导入

`import(module)` 表达式加载模块并返回一个 promise，可以在异步函数中导入
