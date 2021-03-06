# 你不懂JS：作用域与闭包
# 第一章：什么是作用域？

## 复习

作用域是一组规则，它决定了一个变量（标识符）在哪里和如何被查找。这种查询也许是为了向这个变量赋值，这时变量是一个 LHS（左手边）引用，或者是为取得它的值，这时变量是一个 RHS（右手边）引用。

LHS 引用得自赋值操作。*作用域* 相关的赋值可以通过 `=` 操作符发生，也可以通过向函数参数传递（赋予）参数值发生。

JavaScript *引擎* 在执行代码之前首先会编译它，因此，它将 `var a = 2;` 这样的语句分割为两个分离的步骤：

1. 首先，`var a` 在当前 *作用域* 中声明。这是在最开始，代码执行之前实施的。

2. 稍后，`a = 2` 查找这个变量（LHS 引用），并且如果找到就向它赋值。

LHS 和 RHS 引用查询都从当前执行中的 *作用域* 开始，如果有需要（也就是，它们在这里没能找到它们要找的东西），它们会在嵌套的 *作用域* 中一路向上，一次一个作用域（层）地查找这个标识符，直到它们到达全局作用域（顶层）并停止，既可能找到也可能没找到。

未被满足的 RHS 引用会导致 `ReferenceError` 被抛出。未被满足的 LHS 引用会导致一个自动的，隐含地创建的同名全局变量（如果不是“Strict模式”[^note-strictmode]），或者一个 `ReferenceError`（如果是“Strict模式”[^note-strictmode]）。

### 小测验答案

```js
function foo(a) {
	var b = a;
	return a + b;
}

var c = foo( 2 );
```

1. 找出所有的 LHS 查询（有3处！）。

	**`c = ..`, `a = 2`（隐含的参数赋值）和 `b = ..`**

2. 找出所有的 RHS 查询（有4处！）。

    **`foo(2..`, `= a;`, `a + ..` 和 `.. + b`**

[^note-strictmode]: MDN: [Strict Mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions_and_function_scope/Strict_mode)
