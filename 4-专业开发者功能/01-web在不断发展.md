# web在不断发展
在这门课中，我们将帮助你为在不断变化的web环境中部署es6做好准备，如果你在旧版本中使用es6情况将变得具有挑战性，你应该如何编写es6同时又支持旧版浏览器呢？

#6 Polyfill
polyfill是一种填补墙的一个品牌，具有填补的功能，polyfill就是通过复制某些浏览器没有的原生功能来修复这些缺失的javascript文件.
#7 使用polyfill
注意，polyfill 用来弥补缺少的功能。如果浏览器支持 ES6 并且具有原生 startsWith 方法，那么就没必要再添加 polyfill 代码了。如果不存在此方法，则此 polyfill 将覆盖原生实现。

## polyfill 示例
以下代码是新的 ES6 String 方法 `startsWith()` 的 polyfill：

```
if (!String.prototype.startsWith) {
  String.prototype.startsWith = function (searchString, position) {
    position = position || 0;
    return this.substr(position, searchString.length) === searchString;
  };
}
```

可以看出，polyfill 只是普通的 JavaScript。

## 8 polyfill步骤讲解

记住polyfill用于填补尚未支持该原生功能的浏览器，这个polyfill会首先检查 是否有原生startWith方法，为什么？因为如果存在我们便不需要用该文件覆盖原生版本。传入的第二个对象position是字符串开始匹配的位置 或者默认为字符串的第一个字符，然后他将返回true或false,判断传入的字符串和我们所看到的字符串是否一样。

##9 ployfill的其他用途

**Polyfills 不仅仅用来修补 JavaScript 功能**
JavaScript 是用来创建 polyfill 的语言，但是 polyfill 不仅仅用来填补缺失的 JavaScript 功能！有针对各种浏览器功能的 polyfill：

* SVG
* Canvas
* 网络存储（本地存储/会话存储）
* 视频
* HTML5 元素
* 无障碍功能
* Web Sockets
* 等等！

要获得更完整的 polyfill 列表，请访问此[链接](https://github.com/Modernizr/Modernizr/wiki/HTML5-Cross-Browser-Polyfills)


##10 转译
complier 编译 是将源代码转换为更低级的语言。转译是编译的一个子集，它接受源代码并将其转换为目标代码，和编译器一样。但是源代码和目标代码属于同一个抽象级别，基本上来说 如果源代码是人类可读，那么输出语言也将是人类可读的，但是我们为什么要这样做。我们刚看到旧浏览器并不完全支持es6但是它们支持es5代码。这样我们可以使用es6语法和功能来编写js然后使用转译器将其从es6代啊转换为es5代码，这样我们就可以使用最强大的语言编写代码，然后进行转换，使他在任何地方都可以运行。

##11 使用babel

最热门的 JavaScript 转译器是 Babel。

Babel 的原始名称更具描述性——6to5。这是因为，一开始 Babel 专门将 ES6 代码转换为 ES5 代码，但是现在 Babel 具有更多功能了。它可以将 ES6 转换为 ES5、将 JSX 转换为 JavaScript，并将 Flow 转换为 JavaScript。

在计算机上查看转译代码之前，我们快速做个测验，直接在 Babel 网站上将一些 ES6 代码转译为 ES5 代码。请参阅 Babel 的 REPL(英)，并将以下代码粘贴到左侧部分：

```
class Student {
  constructor (name, major) {
    this.name = name;
    this.major = major;
  }

  displayInfo() {
    console.log(`${this.name} is a ${this.major} student.`);
  }
}

const richard = new Student('Richard', 'Music');
const james = new Student('James', 'Electrical Engineering');
```

##12 转移步骤详解
```package.json
{
  "name": "es6",
  "version": "1.0.0",
  "description": "Simple app that demos transpiling ES6 code to ES5 code with Babel.",
  "main": "",
  "scripts": {
    "build": "babel ES6 -d ES5"
  },
  "author": "Richard Kalehoff",
  "license": "MIT",
  "devDependencies": {
    "babel-cli": "^6.16.0",
    "babel-preset-es2015": "^6.16.0"
  }
}

```

项目package.json文件列出了此项目。这个项目依赖babel-cli、banel-preset-es2015 这两个是所有es6插件的一个集合，插件全部装好后，我们需要告诉babel-cli应该用那个插件来将行转译，cli工具会检查.babelrc文件来确定要使用那个插件和presets,所以package.json文件列出应该安装什么。而。babelrc文件告诉babel在进行转译时需要使用什么插件。现在babel知道要用babel-preset-es2015插件，我们需要告诉它去转译代码，为此我们添加了一个build脚本 告诉babel去获取es6目录中的文件，使用es2015 preset转译它们，然后将转译代码放在es5目录中，

```.babelrc
{
    "presets": ["es2015"]
}

```

##13 转译小结

>注意：在制作本课程时（大约为 2016 年冬），当前的浏览器版本支持大多数的 ES6。但只是大多数功能，并非全部功能。并且指的是当前浏览器。有大量的旧浏览器不支持很多 ES6 新增功能。但是可以肯定的是，几乎每个浏览器都支持该语言的上一个版本 (ES5.1)。


及时掌握 JavaScript 的所有变化很重要。最佳方式是开始使用新增的功能。问题是并非所有浏览器都支持这些新功能。鱼与熊掌不可兼得，你可以用 ES6 编写代码，然后使用转译器将其转译为 ES5 代码。这样可以将项目代码库转换为最新版本的语言，同时能够到处运行。当你的代码需要运行在上面的所有浏览器都完全支持 ES6 代码后，你就不用再转译你的代码，直接提供 ES6 代码即可！