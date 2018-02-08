要了解箭头函数中的 `this` 有何区别，让我们快速总结下标准函数中的 `this` 是如何使用的。如果你已经非常熟悉 this 的使用方法，可以跳过此部分。

`this` 关键字的价值完全取决于它的函数（或方法）是如何被调用的。`this `可以是以下任何内容：

### 1. 新的对象
如果函数使用 `new` 被调用：

```
const mySundae = new Sundae('Chocolate', ['Sprinkles', 'Hot Fudge']);
```
在上述代码中，Sundae 这个构造函数内的 this 的值是新的对象，因为它使用 new 被调用。

### 2. 指定的对象
如果函数使用 `call/apply` 被调用：

```
const result = obj1.printName.call(obj2);
```
在上述代码中，printName() 中的 this 的值将指的是 obj2，因为 call() 的第一个参数明确设定 this 指代的是什么。

### 3. 上下文对象
如果函数是对象方法：

`data.teleport();`
在上述代码中，`teleport()` 中的 `this` 的值将指代 `data`。

### 4. 全局对象或 undefined
如果函数被调用时没有上下文：

```
teleport();
```
在上述代码中，`teleport()` 中的 `this` 的值是全局对象，如果在严格模式下，是 `undefined`。

>提示：JavaScript 中的 this 是个很复杂的概念。我们只是快速复习了下，要详细了解如何判断 this，请参阅 this All Makes Sense Now!（来自 Kyle Simpson 的图书系列 《You Don't Know JS》