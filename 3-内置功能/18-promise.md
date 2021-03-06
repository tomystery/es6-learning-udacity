# Promise
JavaScript Promise 是用新的 Promise 构造函数 -` new Promise()` 创建而成的。promise 使你能够展开一些可以**异步**完成的工作，并回到常规工作。创建 promise 时，必须向其提供异步运行的代码。将该代码当做参数提供给构造函数：

```
new Promise(function () {
    window.setTimeout(function createSundae(flavor = 'chocolate') {
        const sundae = {};
        // request ice cream
        // get cone
        // warm up ice cream scoop
        // scoop generous portion into cone!
    }, Math.random() * 2000);
});
```

该代码在我发出请求时将会创建一个 promise，并且在几秒钟后启动。然后需要在 `createSundae `函数中执行几个步骤。

## 指示一个成功请求或者失败请求
但是完成这一切后，JavaScript 如何通知我们它已经完成操作，准备好让我们恢复工作？它通过向初始函数中传入两个函数来实现这一点，通常我们将这两个函数称为 `resolve` 和 `reject`。

该函数被传递给我们向 Promise 构造函数提供的函数 - 通常单词"resolve”用于表示当请求成功完成时，应该调用此函数。请注意第一行的 `resolve`：

```
new Promise(function (resolve, reject) {
    window.setTimeout(function createSundae(flavor = 'chocolate') {
        const sundae = {};
        // request ice cream
        // get cone
        // warm up ice cream scoop
        // scoop generous portion into cone!
        resolve(sundae);
    }, Math.random() * 2000);
});
```
当 sundae 被成功创建后，它会调用` resolve` 方法并向其传递我们要返回的数据，在本例中，返回的数据是完成的 sundae。因此 `resolve `方法用来表示请求已完成，并且成功完成了请求。

如果请求存在问题，无法完成请求，那么我们可以使用传递给该函数的第二个函数。通常，该函数存储在一个叫做"reject"的标识符中，表示如果请求因为某种原因失败了，应该使用该函数。请看看第一行的 `reject`：

```
new Promise(function (resolve, reject) {
    window.setTimeout(function createSundae(flavor = 'chocolate') {
        const sundae = {};
        // request ice cream
        // get cone
        // warm up ice cream scoop
        // scoop generous portion into cone!
        if ( /* iceCreamConeIsEmpty(flavor) */ ) {
            reject(`Sorry, we're out of that flavor :-(`);
        }
        resolve(sundae);
    }, Math.random() * 2000);
});
```

如果请求**无法完成**，则使用 `reject `方法。注意，即使请求失败了，我们依然可以返回数据，在本例中，我们只是返回了一段文字，表示没有我们想要的冰激凌口味。

Promise构造函数需要一个可以运行的函数，运行一段时间后，将成功完成（使用 `resolve` 方法）或失败（使用 `reject` 方法）。当结果最终确定时（请求成功完成或失败），现在 promise 已经**实现了**，并且将通知我们，这样我们便能决定将如何对结果做处理。

## Promise 立即返回对象
首先要注意的是，Promise 将立即返回一个对象。

```
const myPromiseObj = new Promise(function (resolve, reject) {
    // sundae creation code
});
```

该对象上具有一个 `.then()` 方法，我们可以让该方法通知我们 promise 中的请求成功与否。`.then() `方法会接收两个函数：

1. 请求成功完成时要运行的函数
1. 请求失败时要运行的函数

```
mySundae.then(function(sundae) {
    console.log(`Time to eat my delicious ${sundae}`);
}, function(msg) {
    console.log(msg);
    self.goCry(); // not a real method
});
```
可以看出，传递给 `.then()` 的第一个函数将被调用，并传入 Promise 的 resolve 函数需要使用的数据。这里，该函数将接收 `sundae `对象。第二个函数传入的数据会在 Promise 的 `reject` 函数被调用时使用。这里，该函数收到错误消息"Sorry, we're out of that flavor :-("，在上述 Promise 代码中，`reject` 函数被调用。