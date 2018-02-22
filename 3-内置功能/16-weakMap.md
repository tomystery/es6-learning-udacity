# weakMap
>提示：如果你已经看过 WeakSet 部分，那么这部分相当于复习了。WeakMap（弱映射）的行为和 WeakSet 的一样，只是 WeakMap 处理的是键值对，而不是单个条目。

## 什么是 WeakMap？
WeakMap 和普通 Map 很像，但是具有以下关键区别：

1. WeakMap 只能包含对象作为键，
1. WeakMap 无法迭代，意味着无法循环访问，并且
1. WeakMap 没有 .clear() 方法。

你可以像创建普通 Map 那样创建 WeakMap，但是需要使用 `WeakMap` 构造函数。

```
const book1 = { title: 'Pride and Prejudice', author: 'Jane Austen' };
const book2 = { title: 'The Catcher in the Rye', author: 'J.D. Salinger' };
const book3 = { title: 'Gulliver's Travels', author: 'Jonathan Swift' };

const library = new WeakMap();
library.set(book1, true);
library.set(book2, false);
library.set(book3, true);

console.log(library);
```

>WeakMap {Object {title: 'Pride and Prejudice', author: 'Jane Austen'} => true, Object {title: 'The Catcher in the Rye', author: 'J.D. Salinger'} => false, Object {title: 'Gulliver's Travels', author: 'Jonathan Swift'} => true}

但是如果你尝试添加对象以外的内容作为键，系统将报错！

```
library.set('The Grapes of Wrath', false);
```

>Uncaught TypeError: Invalid value used as weak map key(…)

这是可预期到的行为，因为 WeakMap 只能包含对象作为键。但是为何只能包含对象？同样，和 WeakSet 相似，WeakMap 利用垃圾回收机制让其可以更简单地使用和易维护。
### 垃圾回收
在 JavaScript 中，创建新的值时会分配内存，并且当这些值不再需要时，将自动释放内存。这种内存不再需要后释放内存的过程称为垃圾回收。

WeakMap 通过专门处理对象作为键来利用这一点。如果将对象设为 null，则本质上是删除该对象。当 JavaScript 的垃圾回收器运行时，该对象之前占用的内存将被释放，以便稍后在程序中使用。
```
book1 = null;
console.log(library);
```

>WeakMap {Object {title: 'The Catcher in the Rye', author: 'J.D. Salinger'} => false, Object {title: 'Gulliver’s Travels', author: 'Jonathan Swift'} => true}

这种机制的好处在于你不用去担心要删掉对 WeakMap 中已删除对象的引用键，JavaScript 会帮你删除！如果对象被删除，当垃圾回收器运行时，该对象键也会从弱映射中删除。这样的话，如果你想要一种高效、轻便的解决方法去创建一组具有元数据的对象，就可以使用 WeakMap。

垃圾回收的发生时间点取决于很多因素。请参阅 MDN 的文档，详细了解用于处理 JavaScript 中的垃圾回收的算法。