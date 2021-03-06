#xhr的.open方法
我们构建了一个叫做 `asyncRequestObject `的 XHR 对象。我们可以使用多种方法。最重要的一个方法是 `open 方法`。

```
asyncRequestObject.open();
```

`.open() `具有多个参数，但是最重要的参数是前两个参数：

HTTP 方法

要发送请求的 URL

如果我们要向热门高分辨率图片网站 Unsplash 发出首页异步请求，我们需要使用 GET 请求并提供相关 URL：

```
asyncRequestObject.open('GET', 'https://unsplash.com');
```

## 不太记得 HTTP 方法了？

你将主要使用以下两个方法：

*  GET - 检索数据
*  POST - 发送数据

要了解详情，请参阅我们的[HTTP 和网络服务器课程！](https://classroom.udacity.com/courses/ud303) 

>**警告**：出于安全原因，你只能在将加载数据的同一网域中发出资源和数据请求。例如，要向 google.com 发出异步数据请求，浏览器需要位于 google.com 上。这称为**同源策略**。这一限制似乎太严格了，的确是！

这一限制的原因是 JavaScript 对网页上的太多信息具有控制权。它可以访问所有的 Cookie，并且能够判断密码，因为它可以追踪用户按的是哪个键。但是，如果所有信息都只限定在一个位置，网络就不会有今天的发展壮大了。规避相同来源策略的方式是使用 **CORS **(Cross-Origin Resource Sharing)。CORS 是必须在服务器上实现的技术。提供 API 的服务使用 CORS 让开发者能够规避相同来源策略并访问这些服务器上的信息。

## 练习题
XHR 对象的 .open() 方法可以接受多个参数。请参阅此文档 并解释以下代码的作用：

```
const myAsyncRequest = new XMLHttpRequest();
myAsyncRequest.open('GET', 'https://udacity.com/', false);
```

>将 false 传递为第三个参数使 XHR 请求变成异步请求。这将导致 JavaScript 引擎暂停并等待返回该请求，然后再继续。这种“暂停并等待”也称为“阻止”。这是种很糟糕的做法，完全与异步行为的目的相违背。请勿如此设置你的 XHR 对象！要么将第三个参数设为 true 或留空（默认第变成 true）。