#xhr的.send()方法

要实际地发送请求，我们需要使用 send 方法：

```
const asyncRequestObject=new XMLHttpRequest();
asyncRequestObject.open('GET','https://unsplash.com');
asyncRequestObject.send();
```
我们来看看会发生什么：请求被发送，但是我们没有看到任何内容，这就相当于订了蛋糕却没有把蛋糕拿回来。

## 处理成功的请求
要处理 XHR 请求的成功响应，我们将对象上的 **onload 属性**设为将处理它的函数：

```
 function handleSuccess() {
    // in the function, the `this` value is the XHR object
    // this.responseText holds the response from the server

    console.log(this.responseText); // the HTML of https://unsplash.com/
}

asyncRequestObject.onload = handleSuccess;
```

正如我们所看到的，如果未设置 `onload`，则请求的确会返回，但是它什么也不会发生。
**处理错误**

你可能已经知道，如果请求成功，则调用 **onload**。如果请求出现问题，无法实现请求，则我们需要使用 **onerror 属性**：

```
function handleError () {
    // in the function, the `this` value is the XHR object
    console.log( 'An error occurred 😞' );
}

asyncRequestObject.onerror = handleError;
```

和 `onload `一样，如果 `onerror` 未设置，并且出现错误，则该错误将继续发生，但是没有任何提示，你的代码（以及用户）将不知道发生了什么问题，也不知道如何恢复。