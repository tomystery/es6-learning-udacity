# 创建和修改map
## Map(映射)
如果说 Set 类似于数组，那么 Map 就类似于对象，因为 Map 存储键值对，和对象包含命名属性及值相类似。

本质上，Map 是一个可以存储键值对的对象，键和值都可以是对象、原始值或二者的结合。

## 如何创建 Map
要创建 Map，只需输入：

```
const employees = new Map();
console.log(employees);
```

>Map {}

这样就会创建空的 Map `employee`，没有键值对。
## 修改 Map
和 Set 不同，你无法使用值列表创建 Map；而是使用 Map 的 `.set()` 方法添加键值。

```
const employees = new Map();

employees.set('james.parkes@udacity.com', { 
    firstName: 'James',
    lastName: 'Parkes',
    role: 'Content Developer' 
});
employees.set('julia@udacity.com', {
    firstName: 'Julia',
    lastName: 'Van Cleve',
    role: 'Content Developer'
});
employees.set('richard@udacity.com', {
    firstName: 'Richard',
    lastName: 'Kalehoff',
    role: 'Content Developer'
});

console.log(employees);
```

>Map {'james.parkes@udacity.com' => Object {...}, 'julia@udacity.com' => Object {...}, 'richard@udacity.com' => Object {...}}

`.set() `方法有两个参数。第一个参数是键，用来引用第二个参数，即值。

要移除键值对，只需使用 `.delete()` 方法。

```
employees.delete('julia@udacity.com');
employees.delete('richard@udacity.com');
console.log(employees);
```

>Map {'james.parkes@udacity.com' => Object {firstName: 'James', lastName: 'Parkes', role: 'Course Developer'}}

同样，和 Set 类似，你可以使用` .clear() `方法从 Map 中删除所有键值对。

```
employees.clear()
console.log(employees);
```

>Map {}

>提示：如果你使用 `.set()` 向 Map 中添加键已存在的键值对，不会收到错误，但是该键值对将覆盖 Map 中的现有键值对。此外，如果尝试使用 `.delete()` 删除 Map 中不存在的键值，不会收到错误，而 Map 会保持不变。

如果成功地删除了键值对，`.delete()` 方法会返回 `true`，失败则返回 `false`。`.set()` 如果成功执行，则返回 `Map` 对象本身。