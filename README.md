
# JavaScript 编码规范指南

#### 以下文档大多来自:
* [Google JavaScript 编码规范指南](http://wyz.67ge.com/google-js/javascriptguide.xml)
* [Idiomatic 风格](https://github.com/rwldrn/idiomatic.js/tree/master/translations/zh_CN)

#### 参考规范

* [airbnb/javascript](https://github.com/airbnb/javascript)
* [ECMAScript 5.1 注解版](http://es5.github.com/)
* [EcmaScript 语言规范, 5.1 版](http://ecma-international.org/ecma-262/5.1/)

#### 基本原则: 无论有多少人在维护，所有在代码仓库中的代码理应看起来像同一个人写的。

## 目录


------------------------------------------------

## 前言

下面的章节描述的是一个 _合理_ 的现代 JavaScript 开发风格指南，并非硬性规定。其想送出的核心理念是*高度统一的代码风格*（the law of code style consistency）。你为项目所择风格都应为最高准则。作为一个描述放置于你的项目中，并链接到这个文档作为代码风格一致性、可读性和可维护性的保证。

### 项目约定

#### 项目规范

1. JS/CSS 文件编码统一采用 UTF8编码
1. 代码缩进使用4个空格缩进替代 `tab` 缩进
1. 一行代码长度尽量保持80列左右
1. 如果编辑器支持在文件保存的时候自动删除行末和空行中的空格(注意:要么全部采用，要么全不采用，否则会产生过多的diff信息)
1. JS/CSS 最终发布到产品中的时候需要被压缩，以减小静态资源文件大小，提升页面加载速度
1. JS里声明变量必须加上 `var` 关键字，推荐一个 `var` 同时声明多个变量，或者一组有逻辑关系的变量，避免一个变量一个 `var`.
1. 使用 `Array` 和 `Object` 语法直接声明并将其初始化,更易读且性能更好, 而不使用 `Array` 和 `Object` 构造器.
1. JS里使用单引号 (`'`) 优于双引号 (`"`).
1. JS代码结尾统一约定加';'
1. JSON对象的最后一个字段、数组最后一个元素后面都不能加',',在IE8下会报错：所以`{a:1,b:2,}/[1,2,]` 都是不对的.
1. 没有特殊原因避免使用 `with`/`eval`
1. 对于`if`/`else`等后面的语句即使只有一行代码也需要在该行代码的首尾加上'{}'. 对于`switch`语句要给出`default:`情况的处理逻辑.
1. 字符串拼接在少量(次数为个位数)的情况下可以使用'+', 大量的时候使用数组 `join()`, 或者尽可能采用模板引擎渲染：比如`jsRender`等, 如果是`Extjs`可以采用`XTemplate`.
1. `for`循环遍历：`for(var i = 0, l = arr.length; i < l; i++){// doSomething here }` 采用这种方式而不是 `i < arr.length`, 前一种方式只会计算一次 `arr` 的长度，而后一种方式会计算数组长度 `arr.length + 1` 次，效率比较低
1. 字符串转换为整数，推荐使用 `parseInt(num, 10)` 这种方式，`+num` 写法简单，在操作次数极少的情况下也可以酌情使用。
1. 变量比较的时候总是判断最好、最精确的值，推荐使用`===`少用`==`(可以参考[jQuery](https://github.com/jquery/jquery/blob/master/src/core.js)代码里面, 可以看到只有在`== null`的时候才可能使用`==`，其他情况一律使用的是`===`).
1. JS里变量命名规范使用 `functionNamesLikeThis`, `variableNamesLikeThis`, `ClassNamesLikeThis`, `EnumNamesLikeThis`, `methodNamesLikeThis`, 和 `SYMBOLIC_CONSTANTS_LIKE_THIS`, 尤其不要跟`python`里面的变量命名方式混淆了.
1. JS模块里面私有的方法前面可以加`_`,公有方法不加，但是函数内的局部变量就没必要加`_`了；
1. JS文件名应该使用小写字符, 以避免在有些系统平台上不识别大小写的命名方式. 文件名以.js结尾, 不要包含除 `-` 和 `_` 外的标点符号(使用 `-` 优于 `_`), 我们约定统一使用`js-file-name.js`这种类型，对于`template`文件命名方式为 `template_name.html`形式.
1. 所有的html DOM里面的id, Extjs配置项里面的id 以及所有样式里面的 class命名使用中划线，如`id-name`/`class-name`.
1. 代表jQuery对象的变量前面可以加个`$`,这样一眼就能看出来是个jQuery对象。
1. 这几篇文章要好好读下——[jQuery最佳实践](http://www.ruanyifeng.com/blog/2011/08/jquery_best_practices.html)、[Coding Standards & Best Practices](http://lab.abhinayrathore.com/jquery-standards/)
1. jQuery事件绑定:优先使用`on`/`off`绑定或者解除绑定事件，因为从jQuery 1.7以后`.bind()`, `.delegate()` 都是调用 `on` 的, `live`和`die`已经废弃了；
1. HTML DOM节点上原则上不允许有内嵌的style，样式要尽可能抽出来共用。有些样式定义可以成为全局的，比如字体颜色、大小之类的；有些样式不能公用则应当给相应的页面一个class命名空间，任何针对这个页面的样式都应该在这个命名空间下面定义，这样不至于影响到其他页面。
1. 公共的js第三方类库放在static/js/common/lib下，jQuery相关类库放在static/js/common/lib/jQplugin下，我们自己开发的公共类库放在static/js/common下
1. 鉴于有很多代码是复制粘贴过来的，所以大家要保证自己的代码风格良好且易于阅读，不然别人拷过去后不好的风格就蔓延开了，而且会导致其他人效仿。
1. 对于复制粘贴然后做相应修改以实现功能的代码，请务必清理干净，不要有'忘了删除的不影响逻辑的代码'，同时记得将变量名改成适合当前业务场景的有意义的变量名, 不要因为不影响逻辑就保留原来的不适合当前场景的名字
1. 对于系统中出现的大段注释的、过时的、废弃的代码务必及时清理干净，谁制造谁清理，否则其他人也不敢清理，越积越多
1. 不要使用魔法数字，尽量定义一个常量来表示该数字，并加上相应的注释，否则后期可能出现因为数字变化而导致牵一发而动全身，需要到处修改，增加维护成本
1. 注释尽量采用jsdoc的代码注释风格，普通业务代码不做要求，不过通用js类库要求尽量详尽以方便其他人阅读使用
1. 在开发相应功能的时候尽量抽象化、组件化、通用化：考虑这个东西其他地方会不会用到，能不能做成一个组件？而不是类似的代码到处复制、修改或者让大家都去写一遍
1. 类似地，在解决问题的时候要考虑下其他地方会不会存在同样的问题？能不能统一解决掉？尤其对于类似ExtJs的Bug这种，能不能做最少的改动解决所有同样的问题,类似于全局补丁.
1. 代码风格跟其他JS文件的代码风格保持一致;
1. 代码提交前用`JSHint`或者`ESlint`检查一下;
1. 另外补充一点：减少不必要的代码嵌套, 比如以下代码：
```javascript
  function(){
    if(condition){
      // Block A: Do something here
    }else{
      // Block B: A lot of things to do here
    }
  }
```
  可以考虑改成如下形式, 将相对简单的逻辑放在if块里面，执行完毕后立即返回，复杂的逻辑放在外面：
```javascript
  function(){
    if(condition){
      // Block A: Do something here
      return false;
    }
    // Block B: A lot of things to do here
  }
```


#### 前端资源Build

项目必须总是提供一些通用的方法来检验（can be linted）、测试和压缩源码以为产品阶段使用做准备。对于此类工作可以使用`Grunt`或者`Gulp`配合相应的插件来实现。通过简单的配置即可完成自动对CSS进行检查/压缩/合并，对JS进行检查/压缩/合并，对html文件进行压缩，删除创建目录，拷贝文件，压缩打包等，十分方便。


### 规范详情

#### JavaScript 编码风格

##### 空白

  - 永远都不要混用空格和Tab。
  - 开始一个项目，在写代码之前，选择软缩进（空格）或者 Tab（作为缩进方式），并将其作为**最高准则**。
      - 为了可读, 我总是推荐在你的编辑中设计4个字母宽度的缩进 &mdash; 这等同于四个空格或者四个空格替代一个 Tab。
  - 如果你的编辑器支持，请总是打开 “显示不可见字符” 这个设置。好处是：
      - 保证一致性
      - 去掉行末的空格
      - 去掉空行的空格
      - 提交和对比更具可读性

##### 行末和空行

留白会破坏 diff 并使diff 结果变得更不可读。考虑包括一个预提交的 hook 自动删除行末和空行中的空格。

##### 花括号, 换行

```javascript

    // if/else/for/while/try 通常都有小括号、花括号和多行
    // 这有助于可读, 以下是很糟糕的写法

    if(condition) doSomething();

    while(condition) iterating++;

    for(var i=0;i<100;i++) someIterativeFn();
```

##### 命名

通常, 使用 functionNamesLikeThis, variableNamesLikeThis, ClassNamesLikeThis, EnumNamesLikeThis, methodNamesLikeThis, 和 SYMBOLIC_CONSTANTS_LIKE_THIS.

###### 属性和方法

文件或类中的 私有 属性, 变量和方法名应该以下划线 "_" 开头.
保护 属性, 变量和方法名不需要下划线开头, 和公共变量名一样.

###### 方法和函数参数

可选参数以 opt_ 开头.

函数的参数个数不固定时, 应该添加最后一个参数 var_args 为参数的个数. 你也可以不设置 var_args而取代使用 arguments.

可选和可变参数应该在 @param 标记中说明清楚. 虽然这两个规定对编译器没有任何影响, 但还是请尽量遵守

###### Getters 和 Setters

Getters 和 setters 并不是必要的. 但只要使用它们了, 就请将 getters 命名成 getFoo() 形式, 将 setters 命名成 setFoo(value) 形式. (对于布尔类型的 getters, 使用 isFoo() 也可.)

##### 命名空间

JavaScript 不支持包和命名空间.
不容易发现和调试全局命名的冲突, 多个系统集成时还可能因为命名冲突导致很严重的问题. 为了提高 JavaScript 代码复用率, 我们遵循下面的约定以避免冲突.

###### 为全局代码使用命名空间

在全局作用域上, 使用一个唯一的, 与工程/库相关的名字作为前缀标识. 比如, 你的工程是 "Project Sloth", 那么命名空间前缀可取为 sloth.*.

```javascript
var sloth = {};

sloth.sleep = function() {
  ...
};
```

许多 JavaScript 库, 包括 the Closure Library and Dojo toolkit 为你提供了声明你自己的命名空间的函数. 比如:

```javascript
goog.provide('sloth');

sloth.sleep = function() {
  ...
};
```

###### 明确命名空间所有权

当选择了一个子命名空间, 请确保父命名空间的负责人知道你在用哪个子命名空间, 比如说, 你为工程 'sloths' 创建一个 'hats' 子命名空间, 那确保 Sloth 团队人员知道你在使用 sloth.hats.

###### 外部代码和内部代码使用不同的命名空间

"外部代码" 是指来自于你代码体系的外部, 可以独立编译. 内外部命名应该严格保持独立. 如果你使用了外部库, 他的所有对象都在 foo.hats.* 下, 那么你自己的代码不能在 foo.hats.*下命名, 因为很有可能其他团队也在其中命名.

```javascript
foo.require('foo.hats');

/**
 * WRONG -- Do NOT do this.
 * @constructor
 * @extend {foo.hats.RoundHat}
 */
foo.hats.BowlerHat = function() {
};
```


##### 重命名那些名字很长的变量, 提高可读性

主要是为了提高可读性. 局部空间中的变量别名只需要取原名字的最后部分.

```javascript
/**
 * @constructor
 */
some.long.namespace.MyClass = function() {
};

/**
 * @param {some.long.namespace.MyClass} a
 */
some.long.namespace.MyClass.staticHelper = function(a) {
  ...
};

myapp.main = function() {
  var MyClass = some.long.namespace.MyClass;
  var staticHelper = some.long.namespace.MyClass.staticHelper;
  staticHelper(new MyClass());
};
```

##### 除非是枚举类型, 不然不要访问别名变量的属性.

```javascript
/** @enum {string} */
some.long.namespace.Fruit = {
  APPLE: 'a',
  BANANA: 'b'
};

myapp.main = function() {
  var Fruit = some.long.namespace.Fruit;
  switch (fruit) {
    case Fruit.APPLE:
      ...
    case Fruit.BANANA:
      ...
  }
};
myapp.main = function() {
  var MyClass = some.long.namespace.MyClass;
  MyClass.staticHelper(null);
};
```
不要在全局范围内创建别名, 而仅在函数块作用域中使用.

##### 文件名

文件名应该使用小写字符, 以避免在有些系统平台上不识别大小写的命名方式. 文件名以.js结尾, 不要包含除 - 和 _ 外的标点符号(使用 - 优于 _).

##### 自定义 toString() 方法

应该总是成功调用且不要抛异常.
可自定义 toString() 方法, 但确保你的实现方法满足: (1) 总是成功 (2) 没有其他负面影响. 如果不满足这两个条件, 那么可能会导致严重的问题, 比如, 如果 toString() 调用了包含 assert 的函数, assert 输出导致失败的对象, 这在 toString() 也会被调用.

##### 延迟初始化

可以
没必要在每次声明变量时就将其初始化.

##### 明确作用域

任何时候都需要
任何时候都要明确作用域 - 提高可移植性和清晰度. 例如, 不要依赖于作用域链中的 window 对象. 可能在其他应用中, 你函数中的 window 不是指之前的那个窗口对象.

##### 代码格式化

###### 大括号

分号会被隐式插入到代码中, 所以你务必在同一行上插入大括号. 例如:

```javascript
  if (something) {
    // ...
  } else {
    // ...
  }
```

###### 数组和对象的初始化

如果初始值不是很长, 就保持写在单行上:

```javascript
var arr = [1, 2, 3];  // No space after [ or before ].
var obj = {a: 1, b: 2, c: 3};  // No space after { or before }.
```

初始值占用多行时, 缩进2个空格.

```javascript
// Object initializer.
var inset = {
  top: 10,
  right: 20,
  bottom: 15,
  left: 12
};

// Array initializer.
this.rows_ = [
  '"Slartibartfast" <fjordmaster@magrathea.com>',
  '"Zaphod Beeblebrox" <theprez@universe.gov>',
  '"Ford Prefect" <ford@theguide.com>',
  '"Arthur Dent" <has.no.tea@gmail.com>',
  '"Marvin the Paranoid Android" <marv@googlemail.com>',
  'the.mice@magrathea.com'
];

// Used in a method call.
goog.dom.createDom(goog.dom.TagName.DIV, {
  id: 'foo',
  className: 'some-css-class',
  style: 'display:none'
}, 'Hello, world!');
```

###### 函数参数

尽量让函数参数在同一行上. 如果一行超过 80 字符, 每个参数独占一行, 并以4个空格缩进, 或者与括号对齐, 以提高可读性. 尽可能不要让每行超过80个字符. 比如下面这样:

```javascript
// Four-space, wrap at 80.  Works with very long function names, survives
// renaming without reindenting, low on space.
goog.foo.bar.doThingThatIsVeryDifficultToExplain = function(
    veryDescriptiveArgumentNumberOne, veryDescriptiveArgumentTwo,
    tableModelEventHandlerProxy, artichokeDescriptorAdapterIterator) {
  // ...
};

// Four-space, one argument per line.  Works with long function names,
// survives renaming, and emphasizes each argument.
goog.foo.bar.doThingThatIsVeryDifficultToExplain = function(
    veryDescriptiveArgumentNumberOne,
    veryDescriptiveArgumentTwo,
    tableModelEventHandlerProxy,
    artichokeDescriptorAdapterIterator) {
  // ...
};

// Parenthesis-aligned indentation, wrap at 80.  Visually groups arguments,
// low on space.
function foo(veryDescriptiveArgumentNumberOne, veryDescriptiveArgumentTwo,
             tableModelEventHandlerProxy, artichokeDescriptorAdapterIterator) {
  // ...
}

// Parenthesis-aligned, one argument per line.  Visually groups and
// emphasizes each individual argument.
function bar(veryDescriptiveArgumentNumberOne,
             veryDescriptiveArgumentTwo,
             tableModelEventHandlerProxy,
             artichokeDescriptorAdapterIterator) {
  // ...
}
```

###### 传递匿名函数

如果参数中有匿名函数, 函数体从调用该函数的左边开始缩进2个空格, 而不是从 function 这个关键字开始. 这让匿名函数更加易读 (不要增加很多没必要的缩进让函数体显示在屏幕的右侧).

```javascript
var names = items.map(function(item) {
                        return item.name;
                      });

prefix.something.reallyLongFunctionName('whatever', function(a1, a2) {
  if (a1.equals(a2)) {
    someOtherLongFunctionName(a1);
  } else {
    andNowForSomethingCompletelyDifferent(a2.parrot);
  }
});
```

###### 更多的缩进

事实上, 除了 初始化数组和对象 , 和传递匿名函数外, 所有被拆开的多行文本要么选择与之前的表达式左对齐, 要么以4个(而不是2个)空格作为一缩进层次.

```javascript
someWonderfulHtml = '' +
                    getEvenMoreHtml(someReallyInterestingValues, moreValues,
                                    evenMoreParams, 'a duck', true, 72,
                                    slightlyMoreMonkeys(0xfff)) +
                    '';

thisIsAVeryLongVariableName =
    hereIsAnEvenLongerOtherFunctionNameThatWillNotFitOnPrevLine();

thisIsAVeryLongVariableName = 'expressionPartOne' + someMethodThatIsLong() +
    thisIsAnEvenLongerOtherFunctionNameThatCannotBeIndentedMore();

someValue = this.foo(
    shortArg,
    'Some really long string arg - this is a pretty common case, actually.',
    shorty2,
    this.bar());

if (searchableCollection(allYourStuff).contains(theStuffYouWant) &&
    !ambientNotification.isActive() && (client.isAmbientSupported() ||
                                        client.alwaysTryAmbientAnyways()) {
  ambientNotification.activate();
}
```

###### 空行

使用空行来划分一组逻辑上相关联的代码片段.

```javascript
doSomethingTo(x);
doSomethingElseTo(x);
andThen(x);

nowDoSomethingWith(y);

andNowWith(z);
```

###### 二元和三元操作符

操作符始终跟随着前行, 这样就不用顾虑分号的隐式插入问题. 如果一行实在放不下, 还是按照上述的缩进风格来换行.

```javascript
var x = a ? b : c;  // All on one line if it will fit.

// Indentation +4 is OK.
var y = a ?
    longButSimpleOperandB : longButSimpleOperandC;

// Indenting to the line position of the first operand is also OK.
var z = a ?
        moreComplicatedB :
        moreComplicatedC;
```

###### 括号

只在需要的时候使用
不要滥用括号, 只在必要的时候使用它.

对于一元操作符(如delete, typeof 和 void ), 或是在某些关键词(如 return, throw, case, new )之后, 不要使用括号.

###### 字符串

使用 ' 优于 "
无论你选择单引号还是双引号都无所谓，在 JavaScript 中它们在解析上没有区别。而**绝对需要**强制的是一致性。 **永远不要在同一个项目中混用两种引号，选择一种，并保持一致**。

单引号 (') 优于双引号 ("). 当你创建一个包含 HTML 代码的字符串时就知道它的好处了.

```javascript
var msg = 'This is some HTML';
```

###### 前置逗号（Comma First）

请勿使用。所有使用这个文档作为基本风格指南的项目都不允许前置逗号的代码格式，除非明确指定或者作者要求。

###### 注释

  * 单行注释放于代码上方为首选
  * 多行也可以
  * 行末注释应被避免!
  * JSDoc 的方式也不错，但需要比较多的时间

###### 使用 JSDoc

我们使用 JSDoc 中的注释风格. 行内注释使用 // 变量 的形式. 另外, 我们也遵循 C++ 代码注释风格 . 这也就是说你需要:

* 版权和著作权的信息,
* 文件注释中应该写明该文件的基本信息(如, 这段代码的功能摘要, 如何使用, 与哪些东西相关), 来告诉那些不熟悉代码的读者.
* 类, 函数, 变量和必要的注释,
* 期望在哪些浏览器中执行,
* 正确的大小写, 标点和拼写.
* 为了避免出现句子片段, 请以合适的大/小写单词开头, 并以合适的标点符号结束这个句子.

现在假设维护这段代码的是一位初学者. 这可能正好是这样的!

目前很多编译器可从 JSDoc 中提取类型信息, 来对代码进行验证, 删除和压缩. 因此, 你很有必要去熟悉正确完整的 JSDoc .


###### 顶层/文件注释

顶层注释用于告诉不熟悉这段代码的读者这个文件中包含哪些东西. 应该提供文件的大体内容, 它的作者, 依赖关系和兼容性信息. 如下:

```javascript
// Copyright 2009 Google Inc. All Rights Reserved.

/**
 * @fileoverview Description of file, its uses and information
 * about its dependencies.
 * @author user@google.com (Firstname Lastname)
 */
```

###### 类注释

每个类的定义都要附带一份注释, 描述类的功能和用法. 也需要说明构造器参数. 如果该类继承自其它类, 应该使用 @extends 标记. 如果该类是对接口的实现, 应该使用 @implements 标记.

```javascript
/**
 * Class making something fun and easy.
 * @param {string} arg1 An argument that makes this more interesting.
 * @param {Array.<number>} arg2 List of numbers to be processed.
 * @constructor
 * @extends {goog.Disposable}
 */
project.MyClass = function(arg1, arg2) {
  // ...
};
goog.inherits(project.MyClass, goog.Disposable);
```

###### 方法与函数的注释

提供参数的说明. 使用完整的句子, 并用第三人称来书写方法说明.

```javascript
/**
 * Converts text to some completely different text.
 * @param {string} arg1 An argument that makes this more interesting.
 * @return {string} Some return value.
 */
project.MyClass.prototype.someMethod = function(arg1) {
  // ...
};

/**
 * Operates on an instance of MyClass and returns something.
 * @param {project.MyClass} obj Instance of MyClass which leads to a long
 *     comment that needs to be wrapped to two lines.
 * @return {boolean} Whether something occured.
 */
function PR_someMethod(obj) {
  // ...
}
```

对于一些简单的, 不带参数的 getters, 说明可以忽略.

```javascript
/**
 * @return {Element} The element for the component.
 */
goog.ui.Component.prototype.getElement = function() {
  return this.element_;
};
```

###### 属性注释

也需要对属性进行注释.

```javascript
/**
 * Maximum number of things per pane.
 * @type {number}
 */
project.MyClass.prototype.someProperty = 4;
```

###### JSDoc 缩进

如果你在 @param, @return, @supported, @this 或 @deprecated 中断行, 需要像在代码中一样, 使用4个空格作为一个缩进层次.

```javascript
/**
 * Illustrates line wrapping for long param/return descriptions.
 * @param {string} foo This is a param with a description too long to fit in
 *     one line.
 * @return {number} This returns something that has a description too long to
 *     fit in one line.
 */
project.MyClass.prototype.method = function(foo) {
  return 5;
};
```

不要在 @fileoverview 标记中进行缩进.

虽然不建议, 但也可对说明文字进行适当的排版对齐. 不过, 这样带来一些负面影响, 就是当你每次修改变量名时, 都得重新排版说明文字以保持和变量名对齐.

```javascript
/**
 * This is NOT the preferred indentation method.
 * @param {string} foo This is a param with a description too long to fit in
 *                     one line.
 * @return {number} This returns something that has a description too long to
 *                  fit in one line.
 */
project.MyClass.prototype.method = function(foo) {
  return 5;
};
```

###### 枚举

```javascript
/**
 * Enum for tri-state values.
 * @enum {number}
 */
project.TriState = {
  TRUE: 1,
  FALSE: -1,
  MAYBE: 0
};
```

注意一下, 枚举也具有有效类型, 所以可以当成参数类型来用.

```javascript
/**
 * Sets project state.
 * @param {project.TriState} state New project state.
 */
project.setState = function(state) {
  // ...
};
```


#### JavaScript 语言规范

##### 变量

声明变量必须加上 var 关键字.
当你没有写 var, 变量就会暴露在全局上下文中, 这样很可能会和现有变量冲突. 另外, 如果没有加上, 很难明确该变量的作用域是什么, 变量也很可能像在局部作用域中, 很轻易地泄漏到 Document 或者 Window 中, 所以务必用 var 去声明变量.

```javascript

  // 变量
  var foo = "bar",
    num = 1,
    undef;

  // 字面量标识:
  var array = [],
    object = {};

  // 在一个作用域（函数）内只使用一个 `var` 有助于提升可读性
  // 并且让你的声明列表变得有条不紊 (还帮你省了几次键盘敲击)

  // 不好
  var foo = "";
  var bar = "";
  var qux;

  // 好的做法
  var foo = "",
    bar = "",
    quux;

  // 或者..
  var // 对这些变量的注释
  foo = "",
  bar = "",
  quux;

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

##### 常量

常量的形式如: NAMES_LIKE_THIS, 即使用大写字符, 并用下划线分隔. 你也可用 @const 标记来指明它是一个常量. 但请永远不要使用 const 关键词.

Decision:
对于基本类型的常量, 只需转换命名.

```javascript

  /**
   * The number of seconds in a minute.
   * @type {number}
   */
  goog.example.SECONDS_IN_A_MINUTE = 60;

```
对于非基本类型, 使用 @const 标记.

  ```javascript

  /**
   * The number of seconds in each of the given units.
   * @type {Object.<number>}
   * @const
   */
  goog.example.SECONDS_TABLE = {
    minute: 60,
    hour: 60 * 60,
    day: 60 * 60 * 24
  }

  ```
这标记告诉编译器它是常量.

至于关键词 const, 因为 IE 不能识别, 所以不要使用.

##### 分号

总是使用分号.

如果仅依靠语句间的隐式分隔, 有时会很麻烦. 你自己更能清楚哪里是语句的起止. 而且有些情况下, 漏掉分号会很危险，可能会导致代码合并错误等，又比如:

  ```javascript

    // 1.
    MyClass.prototype.myMethod = function() {
      return 42;
    }  // No semicolon here.

    (function() {
      // Some initialization code wrapped in a function to create a scope for locals.
    })();

    var THINGS_TO_EAT = [apples, oysters, sprayOnCheese]  // No semicolon here.

    // 2. conditional execution a la bash
    -1 == resultOfOperation() || die();

  ```
这段代码会发生些什么诡异事呢?

1. 报 JavaScript 错误 - 例子1上的语句会解释成, 一个函数带一匿名函数作为参数而被调用, 返回42后, 又一次被"调用", 这就导致了错误.
1. 当 resultOfOperation() 返回非 NaN 时, 就会调用die, 其结果也会赋给 THINGS_TO_EAT.
为什么?

JavaScript 的语句以分号作为结束符, 除非可以非常准确推断某结束位置才会省略分号. 上面的例子产出错误, 均是在语句中声明了函数/对象/数组直接量, 但 闭括号('}'或']')并不足以表示该语句的结束. 在 JavaScript 中, 只有当语句后的下一个符号是后缀或括号运算符时, 才会认为该语句的结束. 参考：[JS分号自动插入机制](http://justjavac.iteye.com/blog/1852405)

遗漏分号有时会出现很奇怪的结果, 所以确保语句以分号结束.

##### 块内函数声明

不要在块内声明一个函数，不要写成:

```javascript
  if (x) {
    function foo() {}
  }
```
虽然很多 JS 引擎都支持块内声明函数, 但它不属于 ECMAScript 规范 (见 [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm), 第13和14条). 各个浏览器糟糕的实现相互不兼容, 有些也与未来 ECMAScript 草案相违背. ECMAScript 只允许在脚本的根语句或函数中声明函数. 如果确实需要在块中定义函数, 建议使用函数表达式来初始化变量:

```javascript
  if (x) {
    var foo = function() {}
  }
```
##### 标准特性

标准特性总是优于非标准特性.
最大化可移植性和兼容性, 尽量使用标准方法而不是用非标准方法, (比如, 优先用string.charAt(3) 而不用 string[3] , 通过 DOM 原生函数访问元素, 而不是使用应用封装好的快速接口.

##### 不要封装基本类型

没有任何理由去封装基本类型, 另外还存在一些风险:

```javascript
  var x = new Boolean(false);
  if (x) {
    alert('hi');  // Shows 'hi'.
  }
```
除非明确用于类型转换, 其他情况请千万不要这样做！

```javascript
  var x = Boolean(0);
  if (x) {
    alert('hi');  // This will never be alerted.
  }
  typeof Boolean(0) == 'boolean';
  typeof new Boolean(0) == 'object';
```
有时用作 number, string 或 boolean时, 类型的转换会非常实用.


##### 闭包

可以, 但小心使用.
闭包也许是 JS 中最有用的特性了. 有一份比较好的介绍闭包原理的[文档](http://jibbering.com/faq/notes/closures/).

有一点需要牢记, 闭包保留了一个指向它封闭作用域的指针, 所以, 在给 DOM 元素附加闭包时, 很可能会产生循环引用, 进一步导致内存泄漏. 比如下面的代码:

```javascript
  function foo(element, a, b) {
    element.onclick = function() { /* uses a and b */ };
  }
```
这里, 即使没有使用 element, 闭包也保留了 element, a 和 b 的引用, 由于 element 也保留了对闭包的引用, 这就产生了循环引用, 这就不能被 GC 回收. 这种情况下, 可将代码重构为:

```javascript
  function foo(element, a, b) {
    element.onclick = bar(a, b);
  }

  function bar(a, b) {
    return function() { /* uses a and b */ }
  }
```

##### eval()

只用于解析序列化串 (如: 解析 RPC 响应), 而且解析序列号字符串用JSON.parse()会更好，所以最好放弃使用 eval().
eval() 会让程序执行的比较混乱, 当 eval() 里面包含用户输入的话就更加危险. 可以用其他更佳的, 更清晰, 更安全的方式写你的代码, 所以一般情况下请不要使用 eval(). 当碰到一些需要解析序列化串的情况下(如, 计算 RPC 响应), 使用 eval 很容易实现.

解析序列化串是指将字节流转换成内存中的数据结构. 比如, 你可能会将一个对象输出成文件形式:

```javascript
  users = [
    {
      name: 'Eric',
      id: 37824,
      email: 'jellyvore@myway.com'
    },
    {
      name: 'xtof',
      id: 31337,
      email: 'b4d455h4x0r@google.com'
    },
    ...
  ];
```

很简单地调用 eval 后, 把表示成文件的数据读取回内存中.

类似的, eval() 对 RPC 响应值进行解码. 例如, 你在使用 XMLHttpRequest 发出一个 RPC 请求后, 通过 eval () 将服务端的响应文本转成 JavaScript 对象:

```javascript
  var userOnline = false;
  var user = 'nusrat';
  var xmlhttp = new XMLHttpRequest();
  xmlhttp.open('GET', 'http://chat.google.com/isUserOnline?user=' + user, false);
  xmlhttp.send('');
  // Server returns:
  // userOnline = true;
  if (xmlhttp.status == 200) {
    eval(xmlhttp.responseText);
  }
  // userOnline is now true.
```

##### with() {}

不要使用
使用 with 让你的代码在语义上变得不清晰. 因为 with 的对象, 可能会与局部变量产生冲突, 从而改变你程序原本的用义. 下面的代码是干嘛的?

```javascript
  with (foo) {
    var x = 3;
    return x;
  }
```

答案: 任何事. 局部变量 x 可能被 foo 的属性覆盖, 当它定义一个 setter 时, 在赋值 3 后会执行很多其他代码. 所以不要使用 with 语句.

##### this

仅在对象构造器, 方法, 闭包中使用.
this 的语义很特别. 有时它引用一个全局对象(大多数情况下), 调用者的作用域(使用 eval时), DOM 树中的节点(添加事件处理函数时), 新创建的对象(使用一个构造器), 或者其他对象(如果函数被 call() 或 apply()).

使用时很容易出错, 所以只有在下面两个情况时才能使用:

* 在构造器中
* 对象的方法(包括创建的闭包)中

##### for-in 循环

只用于 object/map/hash 的遍历
对 Array 用 for-in 循环有时会出错. 因为它并不是从 0 到 length - 1 进行遍历, 而是所有出现在对象及其原型链的键值. 下面就是一些失败的使用案例:

```javascript
  function printArray(arr) {
    for (var key in arr) {
      print(arr[key]);
    }
  }

  printArray([0,1,2,3]);  // This works.

  var a = new Array(10);
  printArray(a);  // This is wrong.

  a = document.getElementsByTagName('*');
  printArray(a);  // This is wrong.

  a = [0,1,2,3];
  a.buhu = 'wine';
  printArray(a);  // This is wrong again.

  a = new Array;
  a[3] = 3;
  printArray(a);  // This is wrong again.

  // 而遍历数组通常用最普通的 for 循环.
  function printArray(arr) {
    var l = arr.length;
    for (var i = 0; i < l; i++) {
      print(arr[i]);
    }
  }
```

##### 多行字符串

不要使用. 不要这样写长字符串:

```javascript
var myString = 'A rather long string of English text, an error message \
                actually that just keeps going and going -- an error \
                message to make the Energizer bunny blush (right through \
                those Schwarzenegger shades)! Where was I? Oh yes, \
                you\'ve got an error and all the extraneous whitespace is \
                just gravy.  Have a nice day.';
```

在编译时, 不能忽略行起始位置的空白字符; "\" 后的空白字符会产生奇怪的错误; 虽然大多数脚本引擎支持这种写法, 但它不是 ECMAScript 的标准规范.

##### Array 和 Object 直接量

使用 Array 和 Object 语法, 而不使用 Array 和 Object 构造器.

使用 Array 构造器很容易因为传参不恰当导致错误.

```javascript
  // Length is 3.
  var a1 = new Array(x1, x2, x3);

  // Length is 2.
  var a2 = new Array(x1, x2);

  // If x1 is a number and it is a natural number the length will be x1.
  // If x1 is a number but not a natural number this will throw an exception.
  // Otherwise the array will have one element with x1 as its value.
  var a3 = new Array(x1);

  // Length is 0.
  var a4 = new Array();
```
如果传入一个参数而不是2个参数, 数组的长度很有可能就不是你期望的数值了.

为了避免这些歧义, 我们应该使用更易读的直接量来声明.

```javascript
  var a = [x1, x2, x3];
  var a2 = [x1, x2];
  var a3 = [x1];
  var a4 = [];
```
虽然 Object 构造器没有上述类似的问题, 但鉴于可读性和一致性考虑, 最好还是在字面上更清晰地指明. 例如：

```javascript
  var o = new Object();

  var o2 = new Object();
  o2.a = 0;
  o2.b = 1;
  o2.c = 2;
  o2['strange key'] = 3;
```
应该写成:

```javascript
  var o = {};

  var o2 = {
    a: 0,
    b: 1,
    c: 2,
    'strange key': 3
  };
```

##### 不要修改内置对象的原型

千万不要修改内置对象, 如 Object.prototype 和 Array.prototype 的原型. 而修改内置对象, 如 Function.prototype 的原型, 虽然少危险些, 但仍会导致调试时的诡异现象. 所以也要避免修改其原型.



#### JavaScript 小技巧(Tips and Tricks)

##### True 和 False 布尔表达式

下面的布尔表达式都返回 false:

```javascript
null
undefined
''          // 空字符串
0           //数字0
```

但小心下面的, 可都返回 true:

```javascript
'0'   // 字符串0
[]    // 空数组
{}    // 空对象
```
下面段比较糟糕的代码:

```javascript
while (x != null) {
```
你可以直接写成下面的形式(只要你希望 x 不是 0 和空字符串, 和 false):

```javascript
while (x) {
```
如果你想检查字符串是否为 null 或空:

```javascript
if (y != null && y != '') {
```

但这样会更好:

```javascript
if (y) {
```
注意: 还有很多需要注意的地方, 如:

```javascript
    Boolean('0') == true
    '0' != true
    0 != null
    0 == []
    0 == false
    Boolean(null) == false
    null != true
    null != false
    Boolean(undefined) == false
    undefined != true
    undefined != false
    Boolean([]) == true
    [] != true
    [] == false
    Boolean({}) == true
    {} != true
    {} != false
```

##### 条件(三元)操作符 (?:)

三元操作符用于替代下面的代码:

```javascript
    if (val != 0) {
      return foo();
    } else {
      return bar();
    }
```

你可以写成:
```javascript
  return val ? foo() : bar();
```
在生成 HTML 代码时也是很有用的:

```javascript
  var html = '<input type="checkbox"' +
      (isChecked ? ' checked' : '') +
      (isEnabled ? '' : ' disabled') +
      ' name="foo">';
```

##### && 和 ||

二元布尔操作符是可短路的, 只有在必要时才会计算到最后一项.

"||" 被称作为 'default' 操作符, 因为可以这样:

```javascript
    /** @param {*=} opt_win */
    function foo(opt_win) {
      var win;
      if (opt_win) {
        win = opt_win;
      } else {
        win = window;
      }
      // ...
    }
```

你可以使用它来简化上面的代码:

```javascript
    /** @param {*=} opt_win */
    function foo(opt_win) {
      var win = opt_win || window;
      // ...
    }
```

"&&" 也可简短代码.比如:

```javascript
    if (node) {
      if (node.kids) {
        if (node.kids[index]) {
          foo(node.kids[index]);
        }
      }
    }
```
你可以像这样来使用:

```javascript
    if (node && node.kids && node.kids[index]) {
      foo(node.kids[index]);
    }
```
或者:

```javascript
    var kid = node && node.kids && node.kids[index];
    if (kid) {
      foo(kid);
    }
```

不过这样就有点儿过头了:
```javascript
    node && node.kids && node.kids[index] && foo(node.kids[index]);
```

##### 使用 join() 来创建字符串

通常是这样使用的:

```javascript
    function listHtml(items) {
      var html = '<div class="foo">';
      for (var i = 0; i < items.length; ++i) {
        if (i > 0) {
          html += ', ';
        }
        html += itemHtml(items[i]);
      }
      html += '</div>';
      return html;
    }
```
但这样在 IE 下非常慢, 可以用下面的方式:

```javascript
    function listHtml(items) {
      var html = [];
      for (var i = 0; i < items.length; ++i) {
        html[i] = itemHtml(items[i]);
      }
      return '<div class="foo">' + html.join(', ') + '</div>';
    }
```
你也可以是用数组作为字符串构造器, 然后通过 myArray.join('') 转换成字符串. 不过由于赋值操作快于数组的 push(), 所以尽量使用赋值操作.

##### 类型检测 (来源于 jQuery Core Style Guidelines)

* 直接类型（实际类型，Actual Types）

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

* 转换类型（强制类型，Coerced Types）

    考虑下面这个的含义...

    给定的 HTML:

    ```html

    <input type="text" id="foo-input" value="1">

    ```

    ```javascript

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

* 字符串转换为整数

将字符串转换为整数有以下几种方式，可以在[这里](http://jsperf.com/converting-string-to-int/2)进行测试对比：
```javascript
    var number1 = "45";
    // ParseInt() Test on chrome for mac:31% slower
    var i = parseInt(number1);
    // Using unary Test on chrome for mac:67% slower
    var j = +number1;
    // Number constructor Test on chrome for mac:59% slower
    var k = Number(number1);
    // By multplication Test on chrome for mac:69% slower
    var l = number1 * 1;
    // parseInt with Test on chrome for mac:radix ±3.85% fastest
    var m = parseInt(number1, 10);
```
所以推荐使用 parseInt(number1, 10) 这种方式，不过 +number1 更为简单，在操作次数极少的情况下也可以酌情使用。


##### 对比运算

```javascript
    // 当只是判断一个 array 是否有长度，相对于使用这个:
    if (array.length > 0) ...

    // ...判断真伪, 请使用这种:
    if (array.length) ...

    // 当只是判断一个 array 是否为空，相对于使用这个:
    if (array.length === 0) ...

    // ...判断真伪, 请使用这种:
    if (!array.length) ...

    // 当只是判断一个 string 是否为空，相对于使用这个:
    if (string !== "") ...

    // ...判断真伪, 请使用这种:
    if (string) ...

    // 当只是判断一个 string 是为空，相对于使用这个:
    if (string === "") ...

    // ...判断真伪, 请使用这种:
    if (!string) ...

    // 当只是判断一个引用是为真，相对于使用这个:
    if (foo === true) ...

    // ...判断只需像你所想，享受内置功能的好处:
    if (foo) ...

    // 当只是判断一个引用是为假，相对于使用这个:
    if (foo === false) ...

    // ...使用叹号将其转换为真
    if (!foo) ...

    // ...需要注意的是：这个将会匹配 0, "", null, undefined, NaN
    // 如果你 _必须_ 是布尔类型的 false，请这样用：
    if (foo === false) ...

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
    // 类型转换和对比运算说明
    // 首次 `===`，`==` 次之 (除非需要松散类型的对比)
    // `===` 总不做类型转换，这意味着:
    "1" === 1;
    // false

    // `==` 会转换类型，这意味着:
    "1" == 1;
    // true

    // 布尔, 真 & 伪
    // 布尔:
    true, false

    // 真:
    "foo", 1

    // 伪:
    "", 0, null, undefined, NaN, void 0
```

##### Misc

这个部分将要说明的想法和理念都并非教条。相反更鼓励对现存实践保持好奇，以尝试提供完成一般 JavaScript 编程任务的更好方案。

* 提前返回值提升代码的可读性并且没有太多性能上的差别

    ```javascript

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
    ```

* for循环遍历

    ```javascript
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


## 保持一致性.

当你在编辑代码之前, 先花一些时间查看一下现有代码的风格. 如果他们给算术运算符添加了空格, 你也应该添加. 如果他们的注释使用一个个星号盒子, 那么也请你使用这种方式.

代码风格中一个关键点是整理一份常用词汇表, 开发者认同它并且遵循, 这样在代码中就能统一表述. 我们在这提出了一些全局上的风格规则, 但也要考虑自身情况形成自己的代码风格. 但如果你添加的代码和现有的代码有很大的区别, 这就让阅读者感到很不和谐. 所以, 避免这种情况的发生.

