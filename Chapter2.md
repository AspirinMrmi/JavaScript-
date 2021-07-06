# 第二章 HTML中的JavaScript

## 2.1 `<script>`元素

将JavaScript插入HTML中的主要方法是通过`<script>`元素。

这个元素是网景创造出来并且在Netscape Navigator 2中实现了的，后来这个元素被纳入到HTML的规范中。

`<script>`元素具有下面8个属性：

- **async** ：可选。表示立即开始下载脚本，但不能影响页面其他动作，比如下载资源或者等待页面其他资源加载。只对外部文件有效。
- **charset**：可选。使用src属性指定的代码字符集。很少使用，大多数浏览器不在乎它的值。
- **crossorigin**：可选。配置相关请求的CORS（跨源资源共享）设置。默认不使用CORS。`crossorigin="anonymous"`配置文件请求不必设置凭据标志。`crossorigin="use-credentials"`设置凭据标志，意味出站请求会包含凭据。
- **defer**：可选。表示脚本可以延迟到文档完全被解析和显示之后执行。只对外部文件有效。
- **intergrity**： 可选。允许比对接收到的资源和指定的加密签名以验证子资源的完整性。如果接收到的资源的签名和这个属性指定的签名不匹配，则页面会报错，脚本不会执行。这个属性可以用于保证内容分发网络（CDN）不会提供恶意内容。
- **language**：废弃。
- **src**：可选。表示要执行的外部代码文件。
- **type**：可选。代替language，表述代码块中脚本语言的内容类型（MIME类型）。这个值通常是`text/javascript`，尽管`text/javascript`和`text/ecmascript`都已经废弃了。Javascript文件的MIME类型通常是`application/x-javascript`，不过给type属性这个值有可能导致脚本被忽略。在非IE浏览器中有效的其他值还有`application/javascript`和`application/ecmascript`。如果这个值是`module`，则代码会被当成是ES6模块，而且只有这种时候代码中才能出现import和export关键字。

使用`<script>`的方式有两种：

- 通过它直接在网页中嵌入JavaScript代码
- 通过src属性引入外部文件

### 2.1.1 标签位置

现代Web应用程序通常会将所有的JavaScript引用放在`<body>`元素中的页面内容后面

```html
<!DOCTYPE html> 
<html> 
 <head> 
 	<title>Example HTML Page</title> 
 </head> 
 <body> 
 	<!-- 这里是页面内容 --> 
  <script src="example1.js"></script> 
  <script src="example2.js"></script> 
 </body> 
</html>
```

这样，页面会在处理JavaScript代码之前完全渲染页面。

### 2.1.2 推迟执行脚本

HTML4.01为`<script>`元素定义了一个叫defer的属性。

脚本会在整个页面都解析完毕后再执行，因此设置了defer属性，相当于告诉浏览器立即下载，但是延迟执行。

```html
<!DOCTYPE html> 
<html> 
 <head> 
 	<title>Example HTML Page</title> 
  <script defer src="example1.js"></script> 
  <script defer src="example2.js"></script> 
 </head> 
 <body> 
 	<!-- 这里是页面内容 --> 
 </body> 
</html>
```

虽然上面的例子中，`<script>`元素包含在`<head>`标签中，但是它们会在浏览器把页面解析结束才会执行。

HTML5规范要求脚本按他们出现的顺序执行，因此第一个推迟的脚本会在第二个推迟的脚本之前执行，而且两者都会在DOMContentLoaded事件之前执行。

不过，在实际当中，推迟执行的脚本不一定总会按顺序或者在DOMContentLoaded事件之前执行，因此最好只包含一个这样的脚本。

如前边所述，defer属性只对外部脚本文件才有效。

对defer属性的支持是从IE4、Firefox3.5、Safari5和Chrome7开始的。其他浏览器则会忽略这个属性，按照通常的做法来处理脚本。所以还是把推迟执行的脚本放在页面底部比较好。

**注意**：对于XHTML文档，指定defer属性的时候要写成`defer="defer"`

### 2.1.3 异步执行脚本

使用async属性类似于使用defer，与defer不同的是，标记为async的脚本并不能保证能按照它们出现的次序执行。

```html
<!DOCTYPE html> 
<html> 
 <head> 
 	<title>Example HTML Page</title> 
  <script async src="example1.js"></script> 
  <script async src="example2.js"></script> 
 </head> 
 <body> 
 	<!-- 这里是页面内容 --> 
 </body> 
</html>
```

上面的例子中，第二个脚本可能先于第一个脚本执行。标记了async的脚本目的是告诉浏览器，不必等脚本下载和执行完之后再加载页面，同样也不用等到该异步脚本下载和执行后再执行其他脚本。正因为这样，异步脚本不应该在加载期间修改DOM。

好的Web项目中，不推荐使用该方法。

注意：对于XHTML文档，指定async属性的时候要写成`async="async"`

### 2.1.4 动态加载脚本

因为JavaScript可以使用DOM API，所以通过向DOM中动态添加`<script>`元素同样可以加载指定的脚本。只要创建一个`<script>`元素并将其添加到DOM即可。

```javascript
let script = document.createElement('script');
script.src = 'gibberish.js';
script.async = false; // 默认情况下，以这种方式创建的script元素是以异步方式加载的，相当于添加了async属性。但是不是所有的浏览器都支持这一属性，所以为了统一动态脚本的加载行为，可以明确将其设置为同步加载
document.head.appendChild(script);
```

以这种方式获取资源对浏览器预加载器是不可见的。这会严重影响它们在资源获取队列中的优先级。要想让预加载器知道这些动态请求文件的存在，可以在头部文档显式地声明它们。

```
<link rel="preload" href="gribberish.js">
```

### 2.1.5 XHTML中的变化

XHTML已经退出历史舞台，略。

## 2.2 行内代码和外部文件

虽然可以在HTML中直接嵌入JavaScript代码，但是最佳实践是把JavaScript代码放在外部文件中。理由如下：

- 可维护性
- 缓存
- 适应未来

## 2.3 文档模式

IE5.5发明了文档模式的概念，即可以使用doctype切换文档模式。

最初的文档模式有两种：

- 混杂文档模式：让IE像IE5一样支持一些非标准的特性
- 标准模式：让IE具有兼容标准的行为

这两种模式的主要区别体现在CSS渲染的内容方面，但对JavaScript也有一些关联影响（副作用）。

IE初次支持了文档模式切换后，其他浏览器也跟着实现了，随着浏览器的普遍实现，又出现了一种新的模式：**准标准模式**。

这种模式下的浏览器支持很多标准的特性，但是没有标准规定的那么严格。主要区别在于如何处理图片元素周围的空白（在表格中使用图片最明显）。

标准模式通过以下几种文档类型声明开启：

```html
<!-- HTML 4.01 Strict --> 
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" 
"http://www.w3.org/TR/html4/strict.dtd"> 
<!-- XHTML 1.0 Strict --> 
<!DOCTYPE html PUBLIC 
"-//W3C//DTD XHTML 1.0 Strict//EN" 
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd"> 
<!-- HTML5 --> 
<!DOCTYPE html>
```

准标准模式通过过渡性文档类型（Transitional）和框架集文档类型（Frameset）来触发：

```html
<!-- HTML 4.01 Transitional --> 
<!DOCTYPE HTML PUBLIC 
"-//W3C//DTD HTML 4.01 Transitional//EN" 
"http://www.w3.org/TR/html4/loose.dtd"> 
<!-- HTML 4.01 Frameset --> 
<!DOCTYPE HTML PUBLIC 
"-//W3C//DTD HTML 4.01 Frameset//EN" 
"http://www.w3.org/TR/html4/frameset.dtd"> 
<!-- XHTML 1.0 Transitional --> 
<!DOCTYPE html PUBLIC 
"-//W3C//DTD XHTML 1.0 Transitional//EN" 
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd"> 
<!-- XHTML 1.0 Frameset --> 
<!DOCTYPE html PUBLIC 
"-//W3C//DTD XHTML 1.0 Frameset//EN" 
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-frameset.dtd">
```

标准模式和准标准模式一般不做区分。

## 2.4 `<noscript>`元素

`<noscript>`元素可以包含任何HTML元素，除了`<script>`。在下面的情况下，包含在`<noscript>`元素中的内容将会显示：

- 浏览器不支持JavaScript
- 浏览器关闭了JavaScript的支持
