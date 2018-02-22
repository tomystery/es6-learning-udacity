# WeakSet
## 什么是 WeakSet（弱集合）？
WeakSet 和普通 Set 很像，但是具有以下关键区别：

1. WeakSet 只能包含对象
1. WeakSet 无法迭代，意味着不能循环访问其中的对象
1. WeakSet 没有 `.clear() `方法

你可以像创建普通 Set 那样创建 `WeakSet`，但是需要使用 WeakSet 构造函数。


```
const student1 = { name: 'James', age: 26, gender: 'male' };
const student2 = { name: 'Julia', age: 27, gender: 'female' };
const student3 = { name: 'Richard', age: 31, gender: 'male' };

const roster = new WeakSet([student1, student2, student3]);
console.log(roster);
```

>WeakSet {Object {name: 'Julia', age: 27, gender: 'female'}, Object {name: 'Richard', age: 31, gender: 'male'}, Object {name: 'James', age: 26, gender: 'male'}}

但是如果你尝试添加对象以外的内容，系统将报错！

```
roster.add('Amanda');
```

>Uncaught TypeError: Invalid value used in weak set(…)

这是预期到的行为，因为 WeakSet 只能包含对象。但是为何只能包含对象？如果普通 Set 可以包含对象和其他类型的数据，为何还要使用 WeakSet？这个问题的答案与为何 WeakSet 没有 .clear() 方法有很大的关系……
## 垃圾回收
在 JavaScript 中，创建新的值时会分配内存，并且当这些值不再需要时，将自动释放内存。这种内存不再需要后释放内存的过程称为**垃圾回收**。

WeakSet 通过专门使用对象作为键值来利用这一点。如果将对象设为 `null`，则本质上是删除该对象。当 JavaScript 的垃圾回收器运行时，该对象之前占用的内存将被释放，以便稍后在程序中使用。

```
student3 = null;
console.log(roster);
```

>WeakSet {Object {name: 'Julia', age: 27, gender: 'female'}, Object {name: 'James', age: 26, gender: 'male'}}

这种机制的好处在于你不用去担心要删掉对 WeakSet 中已删除对象的引用，JavaScript 会帮你删除！如果对象被删除，当垃圾回收器运行时，该对象也会从 WeakSet 中删除。这样的话，如果你想要一种高效、轻便的解决方法去创建一组对象，就可以使用 WeakSet。

垃圾回收的发生时间点取决于很多因素。请参阅[ MDN 的文档](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Memory_Management#垃圾回收)，详细了解用于处理 JavaScript 中的垃圾回收的算法。