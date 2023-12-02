### When modifying the code in the development environment, multiple instances of the current component are added during hot reloading.

#### Steps to reproduce the issue in the current demo: Enter some content in the text box, then modify the content of the component and save it. Go back to the browser and examine the DOM structure of the component. You will notice duplicate rendering. However, if no content is entered in the text box, modifying the code does not cause any issues.

It seems that the issue lies in the transition section. Where did I make a mistake in the code?

---

![img](./public/1.png)

---

### 开发环境下修改代码，热更新时会添加多个当前的组件?

#### 当前 demo 复现方法：在文本框中输入内容，然后修改组件内容保存后回到浏览器，查看组件所在的 dom 结构，可以发现重复渲染。如果不在文本框输入内容，修改代码不会出现问题。

#### 目前看来应该是 transition 部分，我哪里代码写错了？
