# 使用set
## 使用set
## 查看长度
构建 Set 后，可以通过几个不同的属性和方法来处理 Set。

使用 `.size` 属性可以返回 Set 中的条目数：

```
const months = new Set(['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December']);
console.log(months.size);
```

>12

注意，不能像数组那样通过索引访问 Set，因此要使用 .size 属性，而不是 .length 属性来获取 Set 的大小。

## 检查是否存在某个条目
使用 `.has() `方法可以检查 Set 中是否存在某个条目。如果 Set 中有该条目，则 `.has()` 将返回 true。如果 Set 中不存在该条目，则 `.has() `将返回 `false`。

```
console.log(months.has('September'));
```

>true

## 检索所有值
最后，使用 `.values()` 方法可以返回 Set 中的值。`.values()` 方法的返回值是 `SetIterator` 对象。

```
console.log(months.values());
```

>SetIterator {'January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'}

稍后将讲解 `SetIterator `对象！

>提示：`.keys()` 方法将和 `.values()` 方法的行为完全一样：将 Set 的值返回到新的迭代器对象中。`.keys()` 方法是 `.values()` 方法的别名，和 Map（映射）中的类似。你稍后将在这节课的 Map 部分看到 `.keys()` 方法。