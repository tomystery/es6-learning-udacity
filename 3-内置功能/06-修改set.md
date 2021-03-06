# 修改set
## 修改 Set
创建 Set 后，你可能想要添加或删除条目。如何操作呢？可以使用名称对应的 .add() 和 .delete() 方法：

```
const games = new Set(['Super Mario Bros.', 'Banjo-Kazooie', 'Mario Kart', 'Super Mario Bros.']);

games.add('Banjo-Tooie');
games.add('Age of Empires');
games.delete('Super Mario Bros.');

console.log(games);
```

>Set {'Banjo-Kazooie', 'Mario Kart', 'Banjo-Tooie', 'Age of Empires'}

另一方面，如果你想要删除 Set 中的所有条目，可以使用 `.clear()` 方法。

```
games.clear()
console.log(games);
```

>Set {}

>提示：如果你尝试向 Set 中 `.add()` 重复的条目，系统不会报错，但是该条目不会添加到 Set 中。此外，如果你尝试 `.delete()` Set 中不存在的条目，也不会报错，Set 保持不变。
`.add()` 添加不管成功与否，都会返回该 Set 对象。另一方面，`.delete()` 则会返回一个布尔值，该值取决于是否成功删除（即如果该元素存在，返回true，否则返回false）。