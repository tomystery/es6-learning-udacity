# 处理map
构建 Map 后，可以使用 `.has()` 方法并向其传入一个键来检查 Map 中是否存在该键值对。

```
const members = new Map();

members.set('Evelyn', 75.68);
members.set('Liam', 20.16);
members.set('Sophia', 0);
members.set('Marcus', 10.25);

console.log(members.has('Xavier'));
console.log(members.has('Marcus'));
```

>false

>true

还可以通过向 .get() 方法传入一个键，检索 Map 中的值。

console.log(members.get('Evelyn'));
75.68