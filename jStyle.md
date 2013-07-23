# 书写具备一致风格、通俗易懂 JavaScript 的原则

#### 以下文档大多来自:
### [Idiomatic 风格](https://github.com/rwldrn/idiomatic.js/tree/master/translations/zh_CN)
### [Google JavaScript 编码规范指南](http://wyz.67ge.com/google-js/javascriptguide.xml)

### 基本原则: 无论有多少人在维护，所有在代码仓库中的代码理应看起来像同一个人写的。

### 下面的清单概括了JS代码编写的一些最佳实践。在项目中所有构建代码都必须遵循这些规则。

> ### "对风格的挑刺毫无意义可言。它们必须是指导原则，且你必须遵循。"
>_Rebecca_ _Murphey_

&nbsp;

> ### "成为一个优秀的成功项目管理者的一个条件是，明白按自己的偏好风格写代码是非常不好的做法。如果成千上万的人都在使用你的代码，那么请尽可能通俗易懂地写出你的代码，而非在规范之下自作聪明地使用自己偏好的风格。"
>_Idan_ _Gazit_

## 参考规范

### [ECMAScript 5.1 注解版](http://es5.github.com/)
### [EcmaScript 语言规范, 5.1 版](http://ecma-international.org/ecma-262/5.1/)

### 编译和部署

项目必须总是提供一些通用的方法来检验（can be linted）、测试和压缩源码以为产品阶段使用做准备。对于此类工作 Ben Alman 所写的 [grunt](https://github.com/cowboy/grunt) 可谓首屈一指，并已替代这个仓库的 “kits/” 目录作官方工具。

## 目录

 * [Whitespace](#whitespace)
 * [Beautiful Syntax](#spacing)
 * [Type Checking (Courtesy jQuery Core Style Guidelines)](#type)
 * [Conditional Evaluation](#cond)
 * [Practical Style](#practical)
 * [Naming](#naming)
 * [Misc](#misc)
 * [Native & Host Objects](#native)
 * [Comments](#comments)

------------------------------------------------

## 前言

下面的章节描述的是一个 _合理_ 的现代 JavaScript 开发风格指南，并非硬性规定。其想送出的核心理念是*高度统一的代码风格*（the law of code style consistency）。你为项目所择风格都应为最高准则。作为一个描述放置于你的项目中，并链接到这个文档作为代码风格一致性、可读性和可维护性的保证。

1. <a name="whitespace">空白</a>
  - 永远都不要混用空格和Tab。
  - 开始一个项目，在写代码之前，选择软缩进（空格）或者 Tab（作为缩进方式），并将其作为**最高准则**。
      - 为了可读, 我总是推荐在你的编辑中设计4个字母宽度的缩进 &mdash; 这等同于四个空格或者四个空格替代一个 Tab。
  - 如果你的编辑器支持，请总是打开 “显示不可见字符” 这个设置。好处是：
      - 保证一致性
      - 去掉行末的空格
      - 去掉空行的空格
      - 提交和对比更具可读性

2. <a name="spacing">美化语法</a>

    A. 花括号, 换行

    ```javascript

    // if/else/for/while/try 通常都有小括号、花括号和多行
    // 这有助于可读

    // 2.A.1.1
    // 以下是很糟糕的写法

    if(condition) doSomething();

    while(condition) iterating++;

    for(var i=0;i<100;i++) someIterativeFn();

    ```


    B. 赋值, 声明, 函数 (命名函数, 函数表达式, 构建函数)

    ```javascript

    // 2.B.1.1
    // 变量
    var foo = "bar",
      num = 1,
      undef;

    // 字面量标识:
    var array = [],
      object = {};


    // 2.B.1.2
    // 在一个作用域（函数）内只使用一个 `var` 有助于提升可读性
    // 并且让你的声明列表变得有条不紊 (还帮你省了几次键盘敲击)

    // 不好
    var foo = "";
    var bar = "";
    var qux;

    // 好
    var foo = "",
      bar = "",
      quux;

    // 或者..
    var // 对这些变量的注释
    foo = "",
    bar = "",
    quux;

    // 2.B.1.3
    // `var` 语句必须总是在各自作用域（函数）顶部
    // 同样适应于来自 ECMAScript 6 的常量

    // 不好
    function foo() {

      // 在变量前有语句

      var bar = "",
        qux;
    }

    // 好
    function foo() {
      var bar = "",
        qux;

      // 所有语句都在变量之后
    }
    ```

    D. 一致性（统一）总是笑到最后的（Consistency Always Wins）

    在 2.A-2.C 节，留白作为一个推荐方式被提出，基于单纯的、更高的目的：统一。值得注意的是格式化偏好，像“内部留白”必须是可选的，但在整个项目的源码中必须只存在着一种。

    ```javascript

    // 2.D.1.1

    if (condition) {
      // 语句
    }

    while (condition) {
      // 语句
    }

    for (var i = 0; i < 100; i++) {
      // 语句
    }

    if (true) {
      // 语句
    } else {
      // 语句
    }

    ```

    E. 引号

    无论你选择单引号还是双引号都无所谓，在 JavaScript 中它们在解析上没有区别。而**绝对需要**强制的是一致性。 **永远不要在同一个项目中混用两种引号，选择一种，并保持一致**。

    F. 行末和空行

    留白会破坏 diff 并使diff 结果变得更不可读。考虑包括一个预提交的 hook 自动删除行末和空行中的空格。

3. <a name="type">类型检测 (来源于 jQuery Core Style Guidelines)</a>

    A. 直接类型（实际类型，Actual Types）

    String:

        typeof variable === "string"

    Number:

        typeof variable === "number"

    Boolean:

        typeof variable === "boolean"

    Object:

        typeof variable === "object"

    Array:

        Array.isArray(arrayLikeObject)
        (如果可能的话)

    Node:

        elem.nodeType === 1

    null:

        variable === null

    null or undefined:

        variable == null

    undefined:

      全局变量:

        typeof variable === "undefined"

      局部变量:

        variable === undefined

      属性:

        object.prop === undefined
        object.hasOwnProperty(prop)
        "prop" in object

    B. 转换类型（强制类型，Coerced Types）

    考虑下面这个的含义...

    给定的 HTML:

    ```html

    <input type="text" id="foo-input" value="1">

    ```


    ```javascript

    // 3.B.1.1

    // `foo` 已经被赋予值 `0`，类型为 `number`
    var foo = 0;

    // typeof foo;
    // "number"
    ...

    // 在后续的代码中，你需要更新 `foo`，赋予在 input 元素中得到的新值

    foo = document.getElementById("foo-input").value;

    // 如果你现在测试 `typeof foo`, 结果将是 `string`
    // 这意味着你在 if 语句检测 `foo` 有类似于此的逻辑:

    if (foo === 1) {
      importantTask();
    }

    // `importantTask()` 将永远不会被执行，即使 `foo` 有一个值 "1"


    // 3.B.1.2

    // 你可以巧妙地使用 + / - 一元运算符强制转换类型以解决问题:

    foo = +document.getElementById("foo-input").value;
    //    ^ + 一元运算符将它右边的运算对象转换为 `number`

    // typeof foo;
    // "number"

    if (foo === 1) {
      importantTask();
    }

    // `importantTask()` 将被调用
    ```

    对于强制类型转换这里有几个例子:


    ```javascript

    // 3.B.2.1

    var number = 1,
      string = "1",
      bool = false;

    number;
    // 1

    number + "";
    // "1"

    string;
    // "1"

    +string;
    // 1

    +string++;
    // 1

    string;
    // 2

    bool;
    // false

    +bool;
    // 0

    bool + "";
    // "false"
    ```


    ```javascript
    // 3.B.2.2

    var number = 1,
      string = "1",
      bool = true;

    string === number;
    // false

    string === number + "";
    // true

    +string === number;
    // true

    bool === number;
    // false

    +bool === number;
    // true

    bool === string;
    // false

    bool === !!string;
    // true
    ```

    ```javascript
    // 3.B.2.3

    var num = 2.5;

    parseInt(num, 10);

    // 等价于...

    ~~num;

    num >> 0;

    num >>> 0;

    // 结果都是 2


    // 时刻牢记心底, 负值将被区别对待...

    var neg = -2.5;

    parseInt(neg, 10);

    // 等价于...

    ~~neg;

    neg >> 0;

    // 结果都是 -2
    // 但是...

    neg >>> 0;

    // 结果即是 4294967294

    ```

4. <a name="cond">对比运算</a>

    ```javascript

    // 4.1.1
    // 当只是判断一个 array 是否有长度，相对于使用这个:
    if (array.length > 0) ...

    // ...判断真伪, 请使用这种:
    if (array.length) ...


    // 4.1.2
    // 当只是判断一个 array 是否为空，相对于使用这个:
    if (array.length === 0) ...

    // ...判断真伪, 请使用这种:
    if (!array.length) ...


    // 4.1.3
    // 当只是判断一个 string 是否为空，相对于使用这个:
    if (string !== "") ...

    // ...判断真伪, 请使用这种:
    if (string) ...


    // 4.1.4
    // 当只是判断一个 string 是为空，相对于使用这个:
    if (string === "") ...

    // ...判断真伪, 请使用这种:
    if (!string) ...


    // 4.1.5
    // 当只是判断一个引用是为真，相对于使用这个:
    if (foo === true) ...

    // ...判断只需像你所想，享受内置功能的好处:
    if (foo) ...


    // 4.1.6
    // 当只是判断一个引用是为假，相对于使用这个:
    if (foo === false) ...

    // ...使用叹号将其转换为真
    if (!foo) ...

    // ...需要注意的是：这个将会匹配 0, "", null, undefined, NaN
    // 如果你 _必须_ 是布尔类型的 false，请这样用：
    if (foo === false) ...


    // 4.1.7
    // 如果想计算一个引用可能是 null 或者 undefined，但并不是 false, "" 或者 0,
    // 相对于使用这个：
    if (foo === null || foo === undefined) ...

    // ...享受 == 类型强制转换的好处，像这样:
    if (foo == null) ...

    // 谨记，使用 == 将会令 `null` 匹配 `null` 和 `undefined`
    // 但不是 `false`，"" 或者 0
    null == undefined

    ```
    总是判断最好、最精确的值，上述是指南而非教条。

    ```javascript

    // 4.2.1
    // 类型转换和对比运算说明

    // 首次 `===`，`==` 次之 (除非需要松散类型的对比)

    // `===` 总不做类型转换，这意味着:

    "1" === 1;
    // false

    // `==` 会转换类型，这意味着:

    "1" == 1;
    // true


    // 4.2.2
    // 布尔, 真 & 伪

    // 布尔:
    true, false

    // 真:
    "foo", 1

    // 伪:
    "", 0, null, undefined, NaN, void 0

    ```


5. <a name="practical">实用风格</a>

    ```javascript

    // 5.1.1
    // 一个实用的模块

    (function(global) {
      var Module = (function() {

        var data = "secret";

        return {
          // 这是一个布尔值
          bool: true,
          // 一个字符串
          string: "a string",
          // 一个数组
          array: [ 1, 2, 3, 4 ],
          // 一个对象
          object: {
            lang: "en-Us"
          },
          getData: function() {
            // 得到 `data` 的值
            return data;
          },
          setData: function(value) {
            // 返回赋值过的 `data` 的值
            return (data = value);
          }
        };
      })();

      // 其他一些将会出现在这里

      // 把你的模块变成全局对象
      global.Module = Module;

    })(this);

    ```

    ```javascript

    // 5.2.1
    // 一个实用的构建函数

    (function(global) {

      function Ctor(foo) {

        this.foo = foo;

        return this;
      }

      Ctor.prototype.getFoo = function() {
        return this.foo;
      };

      Ctor.prototype.setFoo = function(val) {
        return (this.foo = val);
      };


      // 不使用 `new` 来调用构建函数，你可能会这样做：
      var ctor = function(foo) {
        return new Ctor(foo);
      };


      // 把我们的构建函数变成全局对象
      global.ctor = ctor;

    })(this);

    ```

6. <a name="naming">命名</a>

    A. 你并不是一个人肉 编译器/压缩器，所以尝试去变身为其一。

    下面的代码是一个极糟命名的典范:

    ```javascript

    // 6.A.1.1
    // 糟糕命名的示例代码

    function q(s) {
      return document.querySelectorAll(s);
    }
    var i,a=[],els=q("#foo");
    for(i=0;i<els.length;i++){a.push(els[i]);}
    ```

    毫无疑问，你写过这样的代码 —— 希望从今天它不再出现。

    这里有一份相同逻辑的代码，但拥有更健壮、贴切的命名（和一个可读的结构）：

    ```javascript

    // 6.A.2.1
    // 改善过命名的示例代码

    function query(selector) {
      return document.querySelectorAll(selector);
    }

    var idx = 0,
      elements = [],
      matches = query("#foo"),
      length = matches.length;

    for (; idx < length; idx++) {
      elements.push(matches[ idx ]);
    }

    ```

    一些额外的命名提示：

    ```javascript

    // 6.A.3.1
    // 命名字符串

    `dog` 是一个 string

    // 6.A.3.2
    // 命名 arrays

    `['dogs']` 是一个包含 `dog 字符串的 array


    // 6.A.3.3
    // 命名函数、对象、实例，等

    camlCase; function 和 var 声明

    // 6.A.3.4
    // 命名构建器、原型，等

    PascalCase; 构建函数


    // 6.A.3.5
    // 命名正则表达式

    rDesc = //;


    // 6.A.3.6
    // 来自 Google Closure Library Style Guide

    functionNamesLikeThis;
    variableNamesLikeThis;
    ConstructorNamesLikeThis;
    EnumNamesLikeThis;
    methodNamesLikeThis;
    SYMBOLIC_CONSTANTS_LIKE_THIS;

    ```

    B. 面对 `this`

    除使用众所周知的 `call` 和 `apply` 外，总是优先选择 `.bind(this)` 或者一个功能上等价于它的。创建 `BoundFunction` 声明供后续调用，当没有更好的选择时才使用别名。

    ```javascript

    // 6.B.1
    function Device(opts) {

      this.value = null;

      // 新建一个异步的 stream，这个将被持续调用
      stream.read(opts.path, function(data) {

        // 使用 stream 返回 data 最新的值，更新实例的值
        this.value = data;

      }.bind(this));

      // 控制事件触发的频率
      setInterval(function() {

        // 发出一个被控制的事件
        this.emit("event");

      }.bind(this), opts.freq || 100);
    }

    // 假设我们已继承了事件发送器（EventEmitter） ;)

    ```

    当不能运行时，等价于 `.bind` 的功能在多数现代 JavaScript 库中都有提供。


    ```javascript
    // 6.B.2

    // 示例：lodash/underscore，_.bind()
    function Device(opts) {

      this.value = null;

      stream.read(opts.path, _.bind(function(data) {

        this.value = data;

      }, this));

      setInterval(_.bind(function() {

        this.emit("event");

      }, this), opts.freq || 100);
    }

    // 示例：jQuery.proxy
    function Device(opts) {

      this.value = null;

      stream.read(opts.path, jQuery.proxy(function(data) {

        this.value = data;

      }, this));

      setInterval(jQuery.proxy(function() {

        this.emit("event");

      }, this), opts.freq || 100);
    }

    // 示例：dojo.hitch
    function Device(opts) {

      this.value = null;

      stream.read(opts.path, dojo.hitch(this, function(data) {

        this.value = data;

      }));

      setInterval(dojo.hitch(this, function() {

        this.emit("event");

      }), opts.freq || 100);
    }

    ```

    提供一个候选，创建一个 `this` 的别名，以 `self` 作为标识符。这很有可能出 bug，应尽可能避免。

    ```javascript

    // 6.B.3

    function Device(opts) {
      var self = this;

      this.value = null;

      stream.read(opts.path, function(data) {

        self.value = data;

      });

      setInterval(function() {

        self.emit("event");

      }, opts.freq || 100);
    }

    ```


    C. 使用 `thisArg`

    好几个 ES 5.1 中的原型的方法都内置了一个特殊的 `thisArg` 标记，尽可能多地使用它

    ```javascript

    // 6.C.1

    var obj;

    obj = { f: "foo", b: "bar", q: "qux" };

    Object.keys(obj).forEach(function(key) {

      // |this| 现在是 `obj`

      console.log(this[ key ]);

    }, obj); // <-- 最后的参数是 `thisArg`

    // 打印出来...

    // "foo"
    // "bar"
    // "qux"

    ```

    `thisArg` 在 `Array.prototype.every`、 `Array.prototype.forEach`、 `Array.prototype.some`、 `Array.prototype.map`、 `Array.prototype.filter` 中都可以使用。

7. <a name="misc">Misc</a>

    这个部分将要说明的想法和理念都并非教条。相反更鼓励对现存实践保持好奇，以尝试提供完成一般 JavaScript 编程任务的更好方案。

    A. 提前返回值提升代码的可读性并且没有太多性能上的差别

    ```javascript

    // 7.B.1.1
    // 不好:
    function returnLate(foo) {
      var ret;

      if (foo) {
        ret = "foo";
      } else {
        ret = "quux";
      }
      return ret;
    }

    // 好:

    function returnEarly(foo) {

      if (foo) {
        return "foo";
      }
      return "quux";
    }

    // for循环遍历:
    for(var i = 0, l = arr.length; i < l; i++){
        // doSomething here
    }
    // 上面的方式优于:
    for(var i = 0; i < arr.length; i++){
        // doSomething here
    }
    // 前一种方式只会计算一次 arr 的长度，而后一种方式会计算 arr.length + 1 次，效率比较低

    ```

9. <a name="comments">注释</a>

  * 单行注释放于代码上方为首选
  * 多行也可以
  * 行末注释应被避免!
  * JSDoc 的方式也不错，但需要比较多的时间

## 附录

### 前置逗号（Comma First）

所有使用这个文档作为基本风格指南的项目都不允许前置逗号的代码格式，除非明确指定或者作者要求。
