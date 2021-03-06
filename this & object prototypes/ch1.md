# 你不懂JS: *this* 与对象原型
# 第一章: `this` 是什么？

## 复习

对于那些没有花时间学习 `this` 绑定机制如何工作的 JavaScript 开发者来说，`this` 绑定一直是困惑的根源。对于 `this` 这么重要的机制来说，猜测、试错、或者盲目地从 Stack Overflow 的回答中复制粘贴，都不是有效或正确利用它的方法。

为了学习 `this`，你必须首先学习 `this`*不是* 什么，不论是哪种把你误导至何处的臆测或误解。`this` 既不是函数自身的引用，也不是函数 *词法* 作用域的引用。

`this` 实际上是在函数被调用时建立的一个绑定，它指向 *什么* 是完全由函数被调用的调用点来决定的。
