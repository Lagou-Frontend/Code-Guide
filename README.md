# Code Guide

*Nothing can be accomplished without norms or standards.*

[HTML](#html)

* [语法](#html_syntax)
* [HTML5 doctype](#html_doctype)
* [lang属性](#html_lang)
* [meta标签](#html_meta)
* [引入css，js](#html_importJSCSS)
* [属性顺序](#html_attrOrder)
* [boolean属性](#html_booleanAttr)
* [减少标签数量](#html_reduceTagsCount)
* [正确嵌套标签](#html_nestTagCorrectly)
* [语义化](#html_semantic)
* [图片](#html_img)
* [表单](#html_formItem)
* [JS生成标签](#html_jsCreatsTag)

[CSS/LESS](#cl)

* [缩进](#cl_indent)
* [分号](#cl_semicolon)
* [空格](#cl_blankSpace)
* [空行](#cl_blankLine)
* [换行](#cl_newline)
* [引号](#cl_quotes)
* [命名](#cl_named)
* [属性声明顺序](#cl_attrOrder)
* [带前缀的属性](#cl_prefixAttr)
* [颜色](#cl_color)
* [属性简写](#cl_shortAttr)
* [媒体查询](#cl_media)
* [LESS相关](#cl_less)
* [其他](#cl_other)

[Javascript](#js)

* [缩进](#js_indent)
* [分号](#js_semicolon)
* [空格](#js_blankSpace)
* [空行](#js_blankLine)
* [换行](#js_newline)
* [引号](#js_quotes)
* [命名](#js_named)
* [单行注释](#js_singleLineComment)
* [多行注释](#js_multiLineComment)
* [文档注释](#js_documentComment)
* [函数](#js_function)
* [数组、对象](#js_arrObj)
* [括号](#js_bracket)
* [null](#js_null)
* [undefined](#js_undefined)
* [其他](#js_other)

[移动端相关](#mobile)

* [meta](#mobile_meta)
* [css](#mobile_css)


## <a name="html">HTML</a>

### <a name="html_syntax">语法</a>

* 缩进使用4个空格；
* 嵌套的标签应该缩进；
* 标签名全⼩写；
* 不要忽略可选的关闭标签，例：&lt;/li&gt; 和 &lt;/body&gt;；
* 无内容标签也需闭合，例：&lt;br /&gt;；
* 在属性上，使用双引号，不要使用单引号；
* 属性名全小写，用中划线做分隔符；
* 属性名不能重复；
* 自定义属性，以"data-"开头；
* id使用驼峰规则，在html文档中不能重复；
* class使用下划线连接。


```html
<!DOCTYPE html>
<html>
	<head>
		<title>Page title</title>
	</head>
	<body>
		<img src="images/company_logo.png" alt="Company" />
		<h1 class="hello_world">Hello, world!</h1>
		<br />
	</body>
</html>
```

### <a name="html_doctype">HTML5 doctype</a>

在页面开头使用这个简单的doctype来启用标准模式，使其在每个浏览器中尽可能有一致的展现；<br />
虽然doctype不区分大小写，但是按照惯例，doctype大写。

```html
<!DOCTYPE html>
<html>
	...
</html>
```

### <a name="html_lang">lang属性</a>

根据HTML5规范：
>应在html标签上加上lang属性。这会给语音工具和翻译工具以帮助，告诉它们应当怎么去发音和翻译。

在[sitepoint](http://www.sitepoint.com/web-foundations/iso-2-letter-language-codes/)上可以查到语言列表；<br />
但[sitepoint](http://www.sitepoint.com/web-foundations/iso-2-letter-language-codes/)只是给出了语言的大类，例如中文只给出了zh，但是没有区分香港，台湾，大陆。而微软给出了一份更加[详细的语言列表](https://msdn.microsoft.com/en-us/library/ms533052(v=vs.85).aspx)，其中细分了zh-cn， zh-hk，zh-tw。

```html
<html lang="zh-CN">
	...
</html>
```

### <a name="html_charset">字符编码</a>

通过明确声明字符编码，能够确保浏览器快速并容易的判断页面内容的渲染方式。这样做的好处是，可以避免在 HTML 中使用字符实体标记（character entity），从而全部与文档编码一致（一般采用 UTF-8 编码）。

```html
<head>
	<meta charset="UTF-8">
</head>
```

### <a name="html_meta">meta标签</a>

* IE兼容模式<br />
	IE 支持通过特定的```<meta>```标签来确定绘制当前页面所应该采用的 IE 版本。除非有强烈的特殊需求，否则最好是设置为 edge mode，从而通知 IE 采用其所支持的最新的模式。如果你想要了解更多，请点击[这里](http://stackoverflow.com/questions/6771258/whats-the-difference-if-meta-http-equiv-x-ua-compatible-content-ie-edge-e)；不同doctype在不同浏览器下会触发不同的渲染模式（[这篇文章](https://hsivonen.fi/doctype/)总结的很到位）。
* Google Chrome Frame<br />
	Google Chrome Frame(谷歌内嵌浏览器框架GCF)插件可以使IE浏览器使用Google Chrome浏览器内核来渲染页面，并且支持IE6、7、8等多个版本的IE浏览器，为了能取得更好的渲染效果，请为content属性添加chrome=1的值，来让安装了此插件的IE浏览器优先选择webkit内核渲染页面。
* 优先使用webkit内核渲染页面<br />
  国内的浏览器基本都是双核浏览器，极速模式通过webkit内核渲染页面，兼容模式通过ie的Trident内核渲染页面，360浏览器实现了通过在页面添加```<meta name="renderer" content="webkit">```的[私有方案](http://se.360.cn/v6/help/meta.html)来让浏览器优先选择webkit内核渲染页面，为了能让页面获得更好的渲染效果，请添加该标签。

```html
<head>
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
    <meta name="renderer" content="webkit">
</head> 
```

### <a name="html_importJSCSS">引入CSS, JS</a>

根据HTML5规范, 通常在引入CSS和JS时不需要指明```type```，因为```text/css```和 ```text/javascript```分别是他们的默认值。
HTML5 规范链接

* [使用link](http://www.w3.org/TR/2011/WD-html5-20110525/semantics.html#the-link-element)
* [使用style](http://www.w3.org/TR/2011/WD-html5-20110525/semantics.html#the-link-element)
* [使用script](http://www.w3.org/TR/2011/WD-html5-20110525/semantics.html#the-style-element)

```html
<!-- External CSS -->
<link rel="stylesheet" href="code_guide.css">

<!-- In-document CSS -->
<style>
	...
</style>

<!-- External JS -->
<script src="code_guide.js"></script>

<!-- In-document JS -->
<script>
	...
</script>
```

### <a name="html_attrOrder">属性顺序</a>

属性应该按照特定的顺序出现以保证易读性；

* id
* class
* name
* data-*
* src, for, type, href, value , max-length, max, min, pattern
* placeholder, title, alt
* aria-*, role
* required, readonly, disabled

class是为高可复用组件设计的，所以应处在第一位；<br />
id更加具体且应该尽量少使用，所以将它放在第二位。

```html
<a class="..." id="..." data-modal="toggle" href="#">Example link</a>

<input class="form-control" type="text">

<img src="..." alt="...">
```

### <a name="html_booleanAttr">boolean属性</a>

boolean属性指不需要声明取值的属性，XHTML需要每个属性声明取值，但是HTML5并不需要；<br />

更多内容可以参考 [WhatWG section on boolean attributes](http://www.whatwg.org/specs/web-apps/current-work/multipage/common-microsyntaxes.html#boolean-attributes)：

>boolean属性的存在表示取值为true，不存在则表示取值为false。

```html
<input type="text" disabled>

<input type="checkbox" value="1" checked>

<select>
	 <option value="1" selected>1</option>
</select>
```

### <a name="html_reduceTagsCount">减少标签数量</a>

* 在编写HTML代码时，需要尽量避免多余的父节点；

	```html
	<!-- bad -->
	<span class="avatar">
		<img src="...">
	</span>
	
	<!-- good -->
	<img class="avatar" src="...">
	```
* 不要引入一些特定的HTML结构来解决一些视觉设计问题。

	```html
	<!-- bad -->
	<style>
	    .text-box > .square {
	        display: inline-block;
	        width: 1rem;
	        height: 1rem;
	        background-color: red;
		}
	</style>
	
	<span class="text-box">
	    <span class="square"></span>
	    See the square next to me?
	</span>
	
	<!-- good -->
	<style>
	    .text-box:before {
	        content: "";
	        display: inline-block;
	        width: 1rem;
	        height: 1rem;
	        background-color: red;
		}
	</style>
	<span class="text-box">
	    See the square next to me?
	</span>
	```

很多时候，需要通过迭代和重构来使HTML变得更少。

### <a name="html_nestTagCorrectly">正确嵌套标签</a>

标签应该被正确的嵌套：

* 块级元素可以嵌套块级元素和行内元素；
* 行内元素可以嵌套行内元素；
* 行内元素不允许嵌套块级元素；
* div不得置于p中

```html
<!-- bad -->
<span class="parent">
	<div class="child"></div>
</span>

<!-- good -->
<div class="parent">
	<p class="child"></p>
</div>

<span class="parent">
	<i class="child"></i>
</span>
```

### <a name="html_semantic">语义化</a>

语义化的使用HTML标签，根据HTML元素的本⾝⽤途来使⽤，如列表、段落，导航栏等；<br />
另外也要注意相关的使用规则，比如一个页面应该只有1个h1标签;<br />
标签的合理使用，能够保证良好的⽂档结构，便于开发者阅读和写出更加优雅的代码，也能够让浏览器的爬虫更好地解析。<br />
为兼容不支持HTML5语义化标签的IE8及其以下版本，需添加html5shiv.js或类似的兼容代码。

```html
<!-- bad -->
<div class="title">Title</div>
<div class="content">Content</div>

<!-- good -->
<h1>Title</h1>
<p>Content</p>

<!DOCTYPE html>
<html>
	<head>
		<title>Page title</title>
		<!--[if lt IE 9]>
		<script src="scripts/html5shiv.js"></script>
		<![endif]-->
	</head>
	<body>
		<header></header>
		<nav></nav>
		<section></section>
		<section></section>
		<footer></footer>
	</body>
</html>
```

### <a name="html_img">图片</a>

* 图片元素img，需增加alt属性，这样当图片文件没有加载出来或用户有阅读障碍时，都不会影响⽤户使⽤；
* 也需增加width，height属性，设置这些属性可以在页面加载时为图片留出空间。如果没有设置这些属性，当图片加载时，页面的布局就会发生变化。但是，仍然需要额外设置图片元素css的height和width属性，如果不设置，当图片链接失效时，图片并不会占据你在标签中声明的大小区域，从而出现布局的混乱。

```html
<!-- bad -->
<img class="logo" />

<!-- good -->
<img class="logo" src="..." alt="logo" width="40px" height="40px" />
```

### <a name="html_formItem">表单</a>

* 如果表单元素有对应的文本说明，请将表单元素与label标签结合使用，用label标签的```for```属性关联表单元素的```id```，这样当点击label标签时，对应的表单元素也同样获得焦点，以提升用户体验。

	```html
	<!-- bad -->
	<form method="post">
		<span>Username</span>
		<input name="username" type="text" />
		<input type="submit" />
	</form>
	
	<!-- good -->
	<form method="post">
		<label for="username">Username</label>
		<input id="username" name="username" type="text" />
		<input type="submit" />
	</form>
	```
* 为button指定type属性值，button的type属性默认值为```submit```，为了保证使用时不出问题，请在任何情况下，为button指定type属性的值。

	```html
	<!-- bad -->
	<button>Click</button>
	
	<!-- good -->
	<button type="button">Click</button>
	```
	* <s>为form指定method属性值为```post```，这是因为form的默认提交方式为get，另外如果表单是通过ajax异步提交的，请设置action属性值为```javascript:;```，以避免在js发成错误时，提交到当前页面。</s>

	```html
	<!-- bad -->
	<form>
	    ...
	</form>
	
	<!-- good -->
	<form method="post" action="javascript:;">
	    ...
	</form>
	```

### <a name="html_jsCreatsTag">JS生成标签</a>

在JS文件中生成标签让内容变得更难查找，更难编辑，性能更差。应该尽量避免这种情况的出现。


## <a name="cl">CSS/LESS</a>

### <a name="cl_indent">缩进</a>

缩进使用4个空格。

### <a name="cl_semicolon">分号</a>

每个属性声明末尾都要加分号。

```css
.selector {
	width: 100px;
}
```

### <a name="cl_blankSpace">空格</a>

以下几种情况不需要空格：

* 多个规则的分隔符','前
* 属性值中'('后和')'前
* 行末不要有多余的空格

以下几种情况需要空格：

* 属性值前
* 选择器'>', '+', '~'前后
* '{'前
* !important '!'前
* 属性值中的','后
* 注释```/*```后```*/```前

```css
/* bad */
.selector {
	color :red! important;
	background-color: rgba(0,0,0,.5);
}

/* good */
.selector {
	color: red !important;
	background-color: rgba(0, 0, 0, .5);
}

/* bad */
.selector ,
.dialog {
	...
}

/* good */
.selector,
.dialog {
	...
}

/* bad */
.selector>.dialog{
	...
}

/* good */
.selector > .dialog{
	...
}

/* bad */
.selector{
	...
}

/* good */
.selector {
	...
}
```

### <a name="cl_blankLine">空行</a>

以下几种情况需要空行：

* 文件最后保留一个空行([原因](http://segmentfault.com/q/1010000000614237/a-1020000000614285))
* <s>'}'后最好跟一个空行，包括less中嵌套的规则</s>
* 属性之间需要适当的空行，具体见属性声明顺序

```css
/* bad */
.selector {
    ...
}
.dialog {
    color: red;
    &:after {
        ...
    }
}

/* good */
.selector {
    ...
}

.dialog {
    color: red;

    &:after {
        ...
    }
}
```

### <a name="cl_newline">换行</a>

以下几种情况不需要换行：

* '{'前
* 多个规则的分隔符','后
 
```css
/* bad */
.selector, .dialog {
    ...
}

/* good */
.selector,
.dialog {
    ...
}
```

以下几种情况需要换行：

* '{'后和'}'前
* 每个属性独占一行

```css
/* bad */
.selector {color: red; background-color: black;}

/* good */
.selector {
    color: red;
    background-color: black;
}
```

### <a name="cl_quotes">引号</a>

* 最外层统一使用双引号
* url的内容不需要用引号
* 属性选择器中的属性值需要引号

```css
.selector:after {
    content: "";
    background-image: url(logo.png);
}

li[data-type="single"] {
    ...
}
```

### <a name="cl_named">命名</a>

* 类名采用小写字母，以下划线分隔
* less中的混合样式采用小写字母，以中划线分隔
* id和less中的变量采用驼峰式命名
* id和class不要以'ad'开头，否则在安装AdBlock等插件的浏览器中会被当作广告而隐藏屏蔽

```less
/* class */
.selector_content {
    ...
}

/* id */
#myDialog {
    ...
}

/* variables */
@colorBlack: #000;


/* mixin */
.text-shadow (@string: 0 1px 3px rgba(0, 0, 0, .25)) {
    text-shadow: @string;
}
```

### <a name="cl_attrOrder">属性声明顺序</a>

相关的属性声明应当归为一组，并按照下面的顺序排列：

1. Positioning
2. Box model
3. Typographic
4. Visual

由于定位（positioning）可以从正常的文档流中移除元素，并且还能覆盖盒模型（box model）相关的样式，因此排在首位。盒模型排在第二位，因为它决定了组件的尺寸和位置。<br />
其他属性只是影响组件的内部（inside）或者是不影响前两组属性，因此排在后面。

```css
.declaration-order {
	/* Positioning */
	position: absolute;
	top: 0;
	right: 0;
	bottom: 0;
	left: 0;
	z-index: 100;
	
	/* Box-model */
	display: block;
	float: right;
	width: 100px;
	height: 100px;

	/* Typography */
	font: normal 13px "Helvetica Neue", sans-serif;
	line-height: 1.5;
	color: #333;
	text-align: center;

	/* Visual */
	background-color: #f5f5f5;
	border: 1px solid #e5e5e5;
	border-radius: 3px;

	/* Misc */
	opacity: 1;
}
```

### <a name="cl_prefixAttr">带前缀的属性</a>

<s>当使用特定厂商的带有前缀的属性时，通过缩进的方式，让每个属性的值在垂直方向对齐，这样便于多行编辑;<br />
	另外无前缀的标准属性应该写在有前缀的属性后面。</s>

```css
/* Prefixed properties */
.selector {
	-webkit-box-shadow: 0 1px 2px rgba(0, 0, 0, .15);
	        box-shadow: 0 1px 2px rgba(0, 0, 0, .15);
}
```

### <a name="cl_color">颜色</a>

<s>颜色16进制用小写字母；</s><br />
颜色16进制尽量用简写。

```css
/* bad */
.selector {
    color: #ABCDEF;
    background-color: #001122;
}

/* good */
.selector {
    color: #abcdef;
    background-color: #012;
}
```

### <a name="cl_shortAttr">属性简写</a>

属性简写需要你非常清楚属性值的正确顺序，而且在大多数情况下并不需要设置属性简写中包含的所有值，另外分开写有助于样式的组合，所以建议尽量分开声明会更加清晰；<br />
margin，padding，border在大多数的情况下推荐使用简写，但是也不要滥用。

常见的属性简写包括：

* margin
* padding
* border
* font
* background
* transition
* animation

```css
/* bad */
.selector {
	margin: 0 0 0 10px;
	background: red;	
}

/* good */
.selector {
	margin-left: 10px;
	background-color: red;	
}

```

### <a name="cl_media">媒体查询</a>

尽量将媒体查询的规则统一放在在文档的最底部，如果规则较少可以将媒体查询的规则靠近与他们相关的规则，不要将他们一起放到一个独立的样式文件中，这样做只会让大家以后更容易忘记他们。

```css
.selector {
    ...
}

.selector-avatar{
    ...
}

@media (min-width: 480px) {
    .selector {
        ...
    }

    .selector-avatar {
        ...
    }
}
```

### <a name="cl_less">LESS相关</a>

<s>声明顺序：</s>
	1. 引入文件
	2. 声明变量
	3. 混合样式
	4. 嵌套规则

@import引入的文件不需要结尾的'.less'；<br />
尽量减少less中的嵌套，<s>最多不超过4层；</s><br />
去掉不必要的父级引用符号'&'。

```less
/* bad */
.selector {
    & .dialog {
        ...
    }
}

/* good */
.selector {
    .dialog {
        ...
    }
}
```

### <a name="cl_other">其他</a>

* 不允许有空的规则；
* <s>去掉小数点前面的0</s>；
* 属性值'0'后面不要加单位；
* 不要在同个规则里出现重复的属性；
* 不要在一个文件里出现两个相同的规则；
* 尽量不要通过CSS的`@import`来引入css文件，而使用less的`@import (css)`引入；
* 尽量不使用`*`选择器；
* 尽量不使用`!important`;
* 尽量不要同时使用reset.css和normalize.css。

## <a name="js">JavaScript</a>

### <a name="js_indent">缩进</a>

缩进使用4个空格。

### <a name="js_semicolon">分号</a>

语句必须以分号结尾，这样可以避免语法错误和压缩错误，而且解析器也不必再分析语句为其添加分号从而提高了性能。

```javascript
if (x < y) {
    x += 10;
} 
```

### <a name="js_blankSpace">空格</a>

以下几种情况不需要空格：

* 对象的属性名后

	```javascript
	var a = {
		b: 1
	};
	```
* 前缀一元运算符后

	```javascript
	+new Date();
	```
* 后缀一元运算符前

	```javascript
	a++;
	```
* 函数调用括号前

	```javascript
	a();
	```
* 无论是函数声明还是函数表达式，'('前不要空格

	```javascript
	function a() {
	
	}
	
	var a = function() {
	
	}
	```
* 运算符'('后和')'前

	```javascript
	var a = (b + c) * 100;
	```

以下几种情况需要空格：

* 二元运算符前后

	```javascript
	var a = b + c;
	```
* 三元运算符'?:'前后

	```javascript
	var a = x ? 1 : 0;
	```
* 代码块'{'前

	```javascript
	if (a) {
			
	}
	```
* 数组的'['后和']'前

	```javascript
	var a = [ 1, 2, 3 ];
	```
* 对象的'{'后和'}'前

	```javascript
	var a = { b: 1 };
	```
* 下列关键字前：else, while, catch, finally
	
	```javascript
	do {
		x++;
	} while (x < 10);
	```
* 下列关键字后：if, else, for, while, do, switch, case, try, catch, finally, return, typeof
 
	```javascript
	try {
	
	} catch(e) {	
	
	}
	```
* 单行注释'//'后（若单行注释和代码同行，则'//'前也需要），多行注释`*`后
 
	```javascript
	// comment
	var a = b; // comment
	```
* 对象的属性值前

	```javascript
	var a = { b: 1, c: 2 };
	```	
* for循环，分号后留有一个空格，前置条件如果有多个，逗号后留一个空格

	```javascript
	for (i = 0; i < 10; i++) {
	    x++;
	}
	```	
* 无论是函数声明还是函数表达式，'{'前一定要有空格

	```javascript
	function a() {
	
	}
	
	var a = function() {
	
	}
	```
* 函数的参数之间

	```javascript
	function method(args1, args2, args3) {
	
	}
	```

### <a name="js_blankLine">空行</a>

以下几种情况需要空行：

* 注释前（当注释在代码块的第一行时，则无需空行）
* 代码块后（在函数调用、数组、对象中则无需空行）
* 文件最后保留一个空行([原因](http://segmentfault.com/q/1010000000614237/a-1020000000614285))

### <a name="js_newline">换行</a>

* 行末有';'时需要换行
* 行末有','或者运算符时可以换行

```javascript
var a = 1,
    b = 2;
```

### <a name="js_quotes">引号</a>

最外层统一使用单引号。

```javascript
var y = 'foo',
    z = '<div id="test"></div>';
```

### <a name="js_named">命名</a>

* 标准变量采用驼峰式命名
* 常量全大写，用下划线连接
* 构造函数，大写第一个字母
* jquery对象必须以'$'开头命名

```javascript
var mayName;

var MAX_COUNT = 10;

function Person(name) {
	this.name = name;
}

var $body = $("body");
```

### <a name="js_singleLineComment">单行注释</a>

* 双斜线后，必须跟一个空格；
* 缩进与下一行代码保持一致；
* 可位于一个代码行的末尾，与代码间隔一个空格。

```javascript
if (condition) {
    // if you made it here, then all security checks passed
    allowed();
}

var zhangsan = 'zhangsan'; // one space after code
```

### <a name="js_multiLineComment">多行注释</a>

最少三行，`*`后跟一个空格，建议在以下情况下使用：

* 难于理解的代码段
* 可能存在错误的代码段
* 浏览器特殊的HACK代码
* 业务逻辑强相关的代码

```javascript
/*
 * one space after '*'
 */
var x = 1;
```

### <a name="js_documentComment">文档注释</a>

各类标签@param, @method等请参考[usejsdoc](http://usejsdoc.org/)和[JSDoc Guide](http://yuri4ever.github.io/jsdoc/)，建议在以下情况下使用：

* 所有常量
* 所有函数
* 所有类

```javascript
/**
 * @func
 * @desc 一个带参数的函数
 * @param {string} a - 参数a
 * @param {number} b=1 - 参数b默认值为1
 * @param {string} c=1 - 参数c有两种支持的取值</br>1—表示x</br>2—表示xx
 * @param {object} d - 参数d为一个对象
 * @param {string} d.e - 参数d的e属性
 * @param {string} d.f - 参数d的f属性
 * @param {object[]} g - 参数g为一个对象数组
 * @param {string} g.h - 参数g数组中一项的h属性
 * @param {string} g.i - 参数g数组中一项的i属性
 * @param {string} [j] - 参数j是一个可选参数
 */
function foo(a, b, c, d, g, j) {
    ...
}
```

### <a name="js_function">函数</a>

* 无论是函数声明还是函数表达式，'('前不要空格，但'{'前一定要有空格；
* 函数调用括号前不需要空格；
* 立即执行函数外必须包一层括号；
* 不要给inline function命名；
* 参数之间用', '分隔，注意逗号后有一个空格。

```javascript
// no space before '(', but one space before'{'
var doSomething = function(item) {
    // do something
};

function doSomething(item) {
    // do something
}

// not good
doSomething (item);

// good
doSomething(item);

// requires parentheses around immediately invoked function expressions
(function() {
    return 1;
})();

// not good
[ 1, 2 ].forEach(function x() {
    ...
});

// good
[ 1, 2 ].forEach(function() {
    ...
});

// not good
var a = [ 1, 2, function a() {
    ...
} ];

// good
var a = [ 1, 2, function() {
    ...
} ];

// use ', ' between function parameters
var doSomething = function(a, b, c) {
    // do something
};
```

### <a name="js_arrObj">数组、对象</a>

* 对象属性名不需要加引号；
* 数组、对象最后不要有逗号。

```javascript
// not good
var a = {
    'b': 1
};

var a = {
    b: 1
};

var a = {
    b: 1,
    c: 2,
};

// good
var a = {
    b: 1,
    c: 2
};
```

### <a name="js_bracket">括号</a>

下列关键字后必须有大括号（即使代码块的内容只有一行）：if, else, for, while, do, switch, try, catch, finally, with。

```javascript
// not good
if (condition)
    doSomething();

// good
if (condition) {
    doSomething();
}
```

### <a name="js_null">null</a>

适用场景：

* 初始化一个将来可能被赋值为对象的变量
* 与已经初始化的变量做比较
* 作为一个参数为对象的函数的调用传参
* 作为一个返回对象的函数的返回值

不适用场景：

* 不要用null来判断函数调用时有无传参
* 不要与未初始化的变量做比较

```javascript
// not good
function test(a, b) {
    if (b === null) {
        // not mean b is not supply
        ...
    }
}

var a;

if (a === null) {
    ...
}

// good
var a = null;

if (a === null) {
    ...
}
```

### <a name="js_undefined">undefined</a>

* 永远不要直接使用undefined进行变量判断
* 使用typeof和字符串'undefined'对变量进行判断

```javascript
// not good
if (person === undefined) {
    ...
}

// good
if (typeof person === 'undefined') {
    ...
}
```

### <a name="js_other">其他</a>

* 用'===', '!=='代替'==', '!='；

	```javascript
	// not good
	if (a == 1) {
	    a++;
	}
	
	// good
	if (a === 1) {
	    a++;
	}
	```
* for-in里一定要有hasOwnProperty的判断；

 	```javascript
 	// good
	for (key in obj) {
	    if (obj.hasOwnProperty(key)) {
	        // be sure that obj[key] belongs to the object and was not inherited
	        console.log(obj[key]);
	    }
	}
	```
* 不要在内置对象的原型上添加方法，如Array, Date；

	```javascript
	// not good
	Array.prototype.count = function(value) {
	    return 4;
	};
	```
* 不要在一些不需要的地方加括号；

	```javascript
	// not good
	delete(obj.attr);

	// good
	delete obj.attr;
	```
* 不要使用未声明的变量
* 不要声明了变量却不使用；
* 不要在应该做比较的地方做赋值；

 	```javascript
 	// not good
	if (a = 10) {
	    a++;
	}
	```
* 数组中不要存在空元素；

 	```javascript
 	// not good
	var a = [1, , , 2, 3];
	```
* 不要在循环内部声明函数；

	```javascript
	// not good
	var nums = [];
	
	for (var i = 0; i < 10; i++) {
	    (function(i) {
	        nums[i] = function(j) {
	            return i + j;
	        };
	    }(i));
	}
	```
	
* switch的falling through和no default的情况一定要有注释特别说明；

	```javascript
	// good
	switch (condition) {
	    case 1:
	    case 2:
	        ...
	        break;
	    case 3:
	        ...
	    // why fall through
	    case 4
	        ...
	        break;
	    // why no default
	}
	```

* 不允许有空的代码块。

	```javascript
	// not good with empty block
	if (condition) {
	
	}
	```
* 不要使用浮点数进行计算

	```javascript
	
	// not good
	var a = 0.1,
	    b = 0.2;
	var c = a + b;
	```


## <a name="mobile">移动端相关</a>

### <a name="mobile_meta">meta</a>

建议移动端head使用如下meta设置

* viewport 设置视窗宽为设备宽度，默认不缩放，不允许用户缩放。

```
<meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no" />
```

* 忽略电话号码和邮箱识别

```
<meta name="format-detection" content="telephone=no, email=no" />
```

* iOS隐藏工具栏和菜单栏

```
<meta name="apple-mobile-web-app-capable" content="yes" />
```

* iOS顶部状态栏(手机信号、时间、电池)的背景颜色。默认值为default（白色），可以定为black（黑色）和black-translucent（灰色半透明）

```
<meta name="apple-mobile-web-app-status-bar-style" content="black" />
```

### <a name="mobile_css">CSS</a>

* 字体设置

```
body { 
    font-family: "Helvetica Neue", Helvetica, STHeiTi, sans-serif; 
}
```

* 盒模型

```
*, *:before, *:after {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
```

* 上下拉动滚动条时卡顿、慢

```
E {
    -webkit-overflow-scrolling: touch;
    overflow-scrolling: touch;
}
```
P.S. 本条及以下的E均代表选择器

* 禁止复制、选中文本

```
E {
    -webkit-user-select: none;
    -moz-user-select: none;
    -khtml-user-select: none;
     user-select: none;
}
```

* 长时间按住页面出现闪退

```
E {
    -webkit-touch-callout: none;
}
```
当你触摸并按住触摸目标时候，禁止或显示系统默认菜单

* 动画定义3D启用硬件加速

```
E {
    -webkit-transform:translate3d(0, 0, 0)
    transform: translate3d(0, 0, 0);
}
```
注意：3D变形会消耗更多的内存与功耗
