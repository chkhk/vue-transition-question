# vue 开发环境下修改代码，热更新时会添加多个当前的组件?

### 复现方法：在文本框中输入内容，然后修改组件内容后回到浏览器，查看组件所在的 dom 结构，可以发现重复渲染。如果不在文本框输入内容，修改代码不会出现问题。

### 目前看来应该是 transition 的问题？
