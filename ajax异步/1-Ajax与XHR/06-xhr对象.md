#xhr对象

就像 JavaScript 引擎提供了 `document`，JavaScript 引擎还提供了发出异步 HTTP 请求的方式。我们通过 `XMLHttpRequest` 对象发出异步请求。我们可以使用提供的 `XMLHttpRequest` 构造函数创建这些对象。

最好的学习方式是自己去尝试编写代码！请转到 Unsplash 并打开开发者工具，然后在控制台上运行以下命令：

```
const asyncRequestObject = new XMLHttpRequest();
```

令人困惑的是，构造函数具有"XML”，但是它不限于 XML 文档。注意，”AJAX”的全称是”异步 JavaScript 和 XML （Asynchronous JavaScript and XML）”。因为最初进行异步数据交换的主要文件格式是 XML 文件，因此该函数称为 `XMLHttpRequest`！

XMLHttpRequest（通常缩写为 XHR 或 xhr）可以用来向 API 请求任何类型的文件（例如 txt 纯文本文件、HTML 文件、JSON 文件、图片文件等）或数据。
>注意：我们将探讨 `XMLHttpRequest` 对象。我们将学习如何创建它，需要使用什么方法和属性，以及如何发送异步请求。要详细了解如何使用 XHR 对象发出异步请求，请参阅以下链接：

* MDN 文档 - https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/open
* WHATWG 规范 - https://xhr.spec.whatwg.org/
* W3C 规范 - https://www.w3.org/TR/XMLHttpRequest/