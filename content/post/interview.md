---
title: "Frontend Interview"
date: 2023-02-20T14:08:56+08:00
draft: false # 是否为草稿

tags: ["interview"]
categories: ["technical"]
---

## 项目工程化

### cmd、umd、amd、commonjs、es6 模块化标准对比

1. **CommonJS：**

   CommonJS 是在 2009 年诞生的一个项目，目标是制定一个在 JavaScript 环境中包括模块、文件系统、二进制处理、buffer 等通用 API 的规范。Node.js 的模块系统就是参照了 CommonJS 规范实现的。

   CommonJS 规范主要用于服务器编程，包含一个模块创建、模块引用和模块标识三个部分。模块通过 require 方法来同步加载所需要的其他模块，通过 exports 或 module.exports 来导出模块中的方法或属性。

   由于服务器端模块文件都存储在本地硬盘，读取速度非常快，所以 CommonJS 规范采用了同步加载的方式。但是，这种方式在浏览器环境中的体验会较差，因为模块文件可能要经过网络传输才能获取。

2. **AMD (Asynchronous Module Definition)：**

   AMD 规范于 2011 年提出，是为解决在浏览器环境中异步加载模块而设计的规范。它使用 requireJS 作为主要的模块化工具，使用 define 函数定义模块，使用 require 函数加载模块。

   AMD 规范允许模块和其依赖可以并行加载，只有当依赖项全部加载完成后，回调函数才会被调用。这种方式在浏览器环境中可以避免网络等原因导致的加载延迟，从而导致阻塞问题。

3. **CMD (Common Module Definition)：**

   CMD 规范在 AMD 规范基础上改进而来，由国内的阿里巴巴团队于 2011 年左右提出并实现 seajs 库。CMD 推崇依赖就近，只在需要时进行 require，支持动态依赖。

   CMD 规范在设计上更加贴近实际的编程需求和习惯，对模块的依赖关系可以灵活处理，使得代码的编写和维护工作变得更加容易。

4. **UMD (Universal Module Definition)：**

   UMD 规范于 2013 年左右提出，设计目标是将 CommonJS 和 AMD 规范融合在一起，使得你的模块在所有的环境下都可以运行。

   使用 UMD 规范，可以使模块在服务器端（Node.js）和客户端（浏览器端）下都能运行，实现模块代码的复用。同时，UMD 还支持全局的引用方式，兼容老版本的浏览器。

5. **ES6 模块化标准：**

   ES6 在 2015 年发布，为 JavaScript 语言标准添加了模块功能。ES6 模块化不仅支持模块级作用域，同时支持从模块导入、导出功能和动态加载。

   ES6 模块化标准的出现，可以说是 JavaScript 模块化规范的一个重要里程碑。至此，JavaScript 已经有了官方的模块化解决方案。

## HTML

### get 和 post 有什么区别

GET 和 POST 最本质的区别是“约定和规范”上的区别，在规范中，定义 GET 请求是用来获取资源的，也就是进行查询操作的，而 POST 请求是用来传输实体对象的，因此会使用 POST 来进行添加、修改和删除等操作。

post 相对来说更安全，传递的数据不会作为 url 的一部分，不会被缓存、保存在服务器日志和浏览器记录中，

post 发送的数量更大 ，get 有 url 长度限制

post 能发送的数据种类更多，get 只能发送 ascii 字符

post 比 get 的速度慢 post 接收数据前会先将请求头发送给服务器确认，等服务器返回状态码 100 后，浏览器才开始发送数据

## JavaScript

### Map 和 Object 有什么区别

1. 键的类型：Map 的键是任意类型，object 的键类型只有字符串/symbol

2. 插入顺序： Map 保持插入顺序，Object 按照属性的一定规则排序（先整数后字符串和小数最后 symbol）

3. 迭代器：Map 是可迭代对象、支持 for-of 和 foreach，Object 默认不可迭代，使用 for-in 或方法循环（Object.keys(o)、values、entries)

4. 原型属性：Map 默认不会覆盖原型的值，Object 可覆盖

5. 操作方法：Map 使用 new 创建，omap.set("a",1) omap.get('a') omap.delete('a') omap.size() 获取长度

   Object 使用点语法或者[]，删除 delete obj.a 长度 Object.keys(obj).length

## GIT

### merge 和 rebase 有什么不同

marge 通过创建一个新的 commit，将冲突一次性处理后提交

rebase 核心是变基，找公共祖先，再把本地提交拼接在后面，逐一解决冲突
