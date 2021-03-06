#set
## 数学意义上的集合（Set）
回忆下之前的数学知识，Set 就是唯一项的集合。例如，`{2, 4, 5, 6}` 是 Set，因为每个数字都是唯一的，只出现一次。但是，`{1, 1, 2, 4}` 不是 Set，因为它包含重复的项目（1 出现了两次！）。

在 JavaScript 中，我们已经可以使用数组表示类似于数学意义上的集合。

```
const nums = [2, 4, 5, 6];
```
但是，数组并不要求项目必须唯一。如果我们尝试向 nums 中添加一个 2，JavaScript 不会报错，会正常添加这个 2。

```
nums.push(2);
console.log(nums);
```

>[2, 4, 5, 6, 2]

现在，`nums` 不再是数学意义上的集合。

## Set（集合）

在 ES6 中，有一个新的内置对象的行为和数学意义上的集合相同，使用起来类似于数组。这个新对象就叫做“Set”。Set 与数组之间的最大区别是：

* Set 不基于索引，不能根据集合中的条目在集合中的位置引用这些条目
* Set 中的条目不能单独被访问

基本上，Set 是让你可以存储唯一条目的对象。你可以向 Set 中添加条目，删除条目，并循环访问 Set。这些条目可以是原始值或对象。

## 如何创建 Set
可以通过几种不同的方式创建 Set。第一种很简单：

```
const games = new Set();
console.log(games);
```

>Set {}
此代码会创建空的 Set games，其中没有条目。

如果你想根据值列表创建 Set，则使用数组：

```
const games = new Set(['Super Mario Bros.', 'Banjo-Kazooie', 'Mario Kart', 'Super Mario Bros.']);
console.log(games);
```

>Set {'Super Mario Bros.', 'Banjo-Kazooie', 'Mario Kart'}

注意上述示例在创建 Set 时，会自动移除重复的条目 `"Super Mario Bros."`，很整洁！