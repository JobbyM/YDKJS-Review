# 你不懂JS: *this* 与对象原型
# 第三章：对象

## 复习

JS 中的对象拥有字面形式（比如 `var a = { .. }`）和构造形式（比如 `var a = new Array(..)`）。字面形式几乎总是首选，但在某些情况下，构造形式提供更多的构建选项。

许多人声称“Javascript 中的一切都是对象”，这是不对的。对象是六种（或七中，看你从哪个方面说）基本类型之一。对象有子类型，包括 `function`，还可以被行为特化，比如 `[object Array]` 作为内部的标签表示子类型数组。

对象是键/值对的集合。通过 `.propName` 或 `["propName"]` 语法，值可以作为属性访问。不管属性什么时候被访问，引擎实际上会调用内部默认的 `[[Get]]` 操作（在设置值时调用 `[[Put]]` 操作），它不仅直接在对象上查找属性，在没有找到时还会遍历 `[[Prototype]]` 链（见第五章）。

属性有一些可以通过属性描述符控制的特定性质，比如 `writable` 和 `configurable`。另外，对象拥有它的不可变性（它们的属性也有），可以通过使用 `Object.preventExtensions(..)`、`Object.seal(..)`、和 `Object.freeze(..)` 来控制几种不同等级的不可变性。

属性不必非要包含值 —— 它们也可以是带有 getter/setter 的“访问器属性”。它们也可以是可枚举或不可枚举的，这控制它们是否会在 `for..in` 这样的循环迭代中出现。

你也可以使用 ES6 的 `for..of` 语法，在数据结构（数组，对象等）中迭代 **值**，它寻找一个内建或自定义的 `@@iterator` 对象，这个对象由一个 `next()` 方法组成，通过这个 `next()` 方法每次迭代一个数据。