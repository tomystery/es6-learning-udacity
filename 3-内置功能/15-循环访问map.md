## 循环访问 Map
你已经创建了 Map，添加了一些键值对，现在你想循环访问该 Map。幸运的是，可以通过以下三种方式循环访问：

1. 使用 Map 的默认迭代器循环访问每个键或值
1. 使用新的 `for...of `循环来循环访问每个键值对
1. 使用 Map 的 `.forEach()` 方法循环访问每个键值对

##  1.使用 MapIterator
在 Map 上使用 `.keys() `和 `.values()` 方法将返回新的迭代器对象，叫做 `MapIterator`。你可以将该迭代器对象存储在新的变量中，并使用 .next() 循环访问每个键或值。你所使用的方法将决定迭代器是否能够访问 Map 的键或值。

```
let iteratorObjForKeys = members.keys();
iteratorObjForKeys.next();
```

>Object {value: 'Evelyn', done: false}

使用 `.next()` 获得下个键值对。

```
iteratorObjForKeys.next();
```

>Object {value: 'Liam', done: false}
等等。

```
iteratorObjForKeys.next();
```

>Object {value: 'Sophia', done: false}

另一方面，使用 `.values()` 方法访问 Map 的值，然后重复同一流程。

```
let iteratorObjForValues = members.values();
iteratorObjForValues.next();
```

>Object {value: 75.68, done: false}

## 2. 使用 for...of 循环
Map 的第二种循环访问方式是使用 `for...of `循环。

```
for (const member of members) {
  console.log(member);
}
```

> ['Evelyn', 75.68]
> 
 ['Liam', 20.16]
>
 ['Sophia', 0]
> 
 ['Marcus', 10.25]

但是，在对 Map 使用 `for...of` 循环时，并不会得到一个键值或一个值。键值对会拆分为一个数组，第一个元素是键，第二个元素是值。有没有什么方法可以解决这一问题？

## 3. 使用 forEach 循环
最后一种循环访问 Map 的方式是使用 `.forEach()` 方法。

```
members.forEach((value, key) => console.log(value, key));
```

> 'Evelyn' 75.68
> 
 'Liam' 20.16
>
 'Sophia' 0
> s
 'Marcus' 10.25
 
 
 注意，在使用箭头函数后，`forEach` 循环是如何简单地读取数据的。对于 `members `中的每个 value 和 key，都会被输出到控制台中。