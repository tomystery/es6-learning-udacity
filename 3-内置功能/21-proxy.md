# proxy

要创建 Proxy（代理）对象，我们使用 Proxy 构造函数 `new Proxy();`。Proxy 构造函数接收两个项目：

* 它将要代理的对象
* 包含将为被代理对象处理的方法列表的对象

第二个对象叫做**处理器**.

## Proxy 内的一个传递
创建 Proxy 的最简单方式是提供对象和空的 handler（处理器）对象。

```
var richard = {status: 'looking for work'};
var agent = new Proxy(richard, {});

agent.status; // returns 'looking for work'
```
上述代码并没有对 Proxy 执行任何特殊操作，只是将请求直接传递给源对象！如果我们希望 Proxy 对象截获请求，这就是 handler 对象的作用了！

让 Proxy 变得有用的关键是当做第二个对象传递给 Proxy 构造函数的 handler 对象。handler 对象由将用于访问属性的方法构成。我们看看 `get`：

## Get Trap（捕获器）
`get `用来截获对属性的调用：

```
const richard = {status: 'looking for work'};
const handler = {
    get(target, propName) {
        console.log(target); // the `richard` object, not `handler` and not `agent`
        console.log(propName); // the name of the property the proxy (`agent` in this case) is checking
    }
};
const agent = new Proxy(richard, handler);
agent.status; // logs out the richard object (not the agent object!) and the name of the property being accessed (`status`)
```
在上述代码中，`handler` 对象具有一个 `get` 方法（因为被用在 Proxy 中，所以将"function"（方法）称之为"trap"（捕获器））。当代码` agent.status;` 在最后一行运行时，因为存在 `get` 捕获器，它将截获该调用以获得 `status`（状态）属性并运行` get` 捕获器方法。这样将会输出 Proxy 的目标对象（`richard` 对象），然后输出被请求的属性（`status `属性）的名称。**它的作用就是这些！**它不会实际地输出属性！这很重要 —— `如果使用了捕获器，你需要确保为该捕获器提供所有的功能。`

## 从 Proxy 内部访问目标对象
如果我们想真正地提供真实的结果，我们需要返回目标对象的属性：

```
const richard = {status: 'looking for work'};
const handler = {
    get(target, propName) {
        console.log(target);
        console.log(propName);
        return target[propName];
    }
};
const agent = new Proxy(richard, handler);
agent.status; // (1)logs the richard object, (2)logs the property being accessed, (3)returns the text in richard.status
```

注意我们在 `get` trap 中添加了最后一行 `return target[propName];`，这样将会访问目标对象的属性并返回它。

## 直接获取 Proxy 的返回信息
此外，我们可以使用 Proxy 提供直接的反馈：

```
const richard = {status: 'looking for work'};
const handler = {
    get(target, propName) {
        return `He's following many leads, so you should offer a contract as soon as possible!`;
    }
};
const agent = new Proxy(richard, handler);
agent.status; // returns the text `He's following many leads, so you should offer a contract as soon as possible!`
```

对于上述代码，Proxy 甚至不会检查目标对象，直接对调用代码做出响应。

因此每当 Proxy 上的属性被访问，`get `trap 将接管任务。如果我们想截获调用以更改属性，则需要使用 `set `trap！

`set` trap 用来截获将更改属性的代码。`set` trap 将接收： 它代理的对象 被设置的属性 Proxy 的新值

```
const richard = {status: 'looking for work'};
const handler = {
    set(target, propName, value) {
        if (propName === 'payRate') { // if the pay is being set, take 15% as commission
            value = value * 0.85;
        }
        target[propName] = value;
    }
};
const agent = new Proxy(richard, handler);
agent.payRate = 1000; // set the actor's pay to $1,000
agent.payRate; // $850 the actor's actual pay
```

在上述代码中，注意 `set `trap 会检查是否设置了 `payRate` 属性。如果设置了，Proxy 就从中拿走 15% 的费用作为自己的佣金！当演员的薪酬是一千美元时，因为 `payRate `属性已设置，代码从中扣除 15% 的费用，并将实际 `payRate` 属性设为 `850`；
## 其他 Trap
我们查看了 `get `和 `set` trap（可能是你最常用到的 Trap），但是实际上总共有 13 种不同的 Trap，它们都可以用在处理程序中！

get trap - 使 proxy 能处理对属性访问权的调用
set trap - 使 proxy 能将属性设为新值
apply trap - 使 proxy 能被调用（被代理的对象是函数）
has trap - 使 proxy 能使用 in 运算符
deleteProperty trap - 使 proxy 能确定属性是否被删除
ownKeys trap - 使 proxy 能处理当所有键被请求时的情况
construct trap - 使 proxy 能处理 proxy 与 new 关键字一起使用当做构造函数的情形
defineProperty trap - 使 proxy 能处理当 defineProperty 被用于创建新的对象属性的情形
getOwnPropertyDescriptor trap - 使 proxy 能获得属性的描述符
preventExtenions trap - 使 proxy 能对 proxy 对象调用 Object.preventExtensions()
isExtensible trap - 使 proxy 能对 proxy 对象调用 Object.isExtensible
getPrototypeOf trap - 使 proxy 能对 proxy 对象调用 Object.getPrototypeOf
setPrototypeOf trap - 使 proxy 能对 proxy 对象调用 Object.setPrototypeOf
可以看出，有很多 trap 可以让 proxy 管理如何处理被代理的对象的调用。