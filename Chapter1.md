

# 第一章 什么是JavaScript

## 1.1 简单的历史回顾

诞生于1995年。

当时表单的验证都是在服务器端实现，Netscape公司想通过在其Navigator加入JavaScript来改变这一现状，JavaScript应运而生。所以JavaScript从开始的一个简单的输入验证器发展成为了一门强大的语言。

扒开JavaScript的历史，开始开发时，JavaScript叫做liveScript，其在发布前夕，为了蹭一把当时大火的Java的热度，改名为JavaScript。不难看出JavaScript其实是编程网红的雏形。

JavaScript的1.0版本获得了巨大的成功，紧接着Netscape又在Netscape Navigator3中发布了JavaScript1.1版本，由于JavaScript受用户的关注度屡创新高，1996年微软瞅准了机会决定进军来分一杯羹。就在Netscape Navigator3发布不久，微软就在自家的Internet Explorer3中加入了对JavaScript的支持，命名为JScript，之所以起这个名字是为了防止和Netscape打官司。

所以，在当时的背景下，有两种JavaScript的实现：一种是Netscape的，另一种是微软的。因为当时没有相关组织去制定JavaScript的语法和特性的标准，所以慢慢的，JavaScript的标准问题也被提上了日程。另外，有竞争就存在着进步，导致JavaScript呈现一种爆炸式的发展速度。

在1997年，JavaScript1.1版本被提交给了ECMA（European Computer Manufactures Association），也就是欧洲计算机制造商协会。该协会指定了TC39（Technical Committee #39），也就是39号技术委员会来负责去指定标准。经过数月努力完成了ECMA-262——定义了一种名为ECMAScript的新脚本语言标准。原来这个读作 “ek-ma-script”。

第二年，ISO/IEC(International Organization for Standardization and International Electrotechnical Commission，国标标准化组织和国际电工委员会)也采用了 ECMAScript 作为标准(即 ISO/IEC-16262)。 自此以后，浏览器开发商就开始致力于将 ECMAScript 作为各自 JavaScript 实现的基础，也在不同程度上取得了成功。

## 1.2 JavaScript的实现

JavaScript由三部分组成：

- ECMAScript（核心）
- DOM（文档对象模型）
- BOM（浏览器对象模型）

### 1.2.1 ECMAScript

我们的Web浏览器其实是ECMAScript的宿主环境之一，宿主环境不仅提供基本的ECMAScript的实现，还提供了该语言的扩展。其他宿主环境还有运行在服务端的Node.js以及将要被淘汰的Adobe Flash。

如果不涉及浏览器的话，ECMA-262到底定义了什么？在最基本的层面，它描述了这门语言的如下部分：

- 语法
- 类型
- 语句
- 关键字
- 保留字
- 操作符
- 全局对象

ECMAScript是标准，JavaScript是对这一标准的实现。

**ECMAScript的版本历程：**

- **ECMA-262第1版**，本质是跟NetScape的JavaScript1.1相同，只是删除了所有浏览器特定的代码，外加少量细微修改。ECMA-262要求支持Unicode标准（以支持多语言），而且对象要与平台无关。这也是JavaScript1.1和JavaScript1.2不符合ECMA-262第一版要求的原因。
- **ECMA-262第2版**，只是做了一些编校工作，以符合ISO/IEC-16262的标准，并没有增减和修改特性。
- **ECMA-262第3版**，里程碑式变革，更新了字符串处理、错误定义和数值输出。此外还增加了正则表达式、新的控制语句、try/catch异常处理的支持，以及为了更好地让标准国际化做的少量修改。
- **ECMA-262第4版**，是对这门语言的的一次彻底修订，作为对JavaScript在Web浏览器上的巨大成功的回应，开发者开始修订ECMAScript以满足全球Web开发日益增长的需求。为此 Ecma T39再次被召集起来，以决定这门语言的未来。结果，他们制定的规范几乎在第三版的基础上完全制定了一门新的语言，第四版包括强类型变量、新语句和数据结构、真正的类和经典的继承、以及操作数据的新手段。与此同时，TC39委员会的子委员会认为第四版的修订对这门语言的改动太大了，提出了改动较小的提案，只在现有的JavaScript引擎基础上做一些增改就可以实现。最终该提案赢得了TC39委员会的支持，ECMA-262第4版在正式发布前被放弃。
- **ECMA-262第5版**，于是ECMAScript3.1变成了ECMA-262的第5版，于2009年12月3日正式发布，第5版致力于理清第3版中存在的歧义，也增加了新功能，包括原生的解析和序列化JSON数据的JSON对象，方便继承和高级属性定义的方法，以及新的增强ECMAScript引擎解释和执行代码能力的严格模式。该版本在2011年6月发布了一个维护性修订版本，只是更正了规范中的错误。
- **ECMA-262第6版**，就是我们耳熟能详的ES6、ES2015或ES Harmony，于2015年6月发布。这个版本涵盖了有史以来最重要的一批特性。ES6支持了类、模块、迭代器、生成器、箭头函数、Promise、Reflect、Proxy、和众多的新的数据特性。
- **ECMA-262第7版**，也称为ES7或ES2016，于2016年6月发布。这次发布只包含少量语法层面的增强，如Array.prototype.includes和指数操作符。
- **ECMA-262第8版**，也称为ES8或ES2017，于2017年6月发布。这一版主要增加了异步函数（async/await）、sharedArrayBuffer及Atomics API，以及Object.values()/Object.entries()/Object.getOwnPropertyDescriptors()和字符串填充方法，另外明确支持对象字面量最后的逗号。
- **ECMA-262第9版**，也称为ES9或ES2018，于2018年6月发布。这次修订内容主要包括异步迭代、剩余和扩展属性、一组新的正则表达式特性、Promise.finally()、以及模版字面量修订。
- **ECMA-262第10版**，也称为ES10或ES2019，发布于2019年6月。这次修订增加了Array.prototype.flat()/flatMap()、String.prototype.trimStart()/trimEnd()、Object.fromEntries方法，以及Symbol.prototype.description属性，明确定义了Function.prototype.toString()的返回值并固定了Array.prototype.sort()的顺序，另外，这次修订解决了与JSON字符串兼容的问题，并定义了catch子句的可选绑定。

**ECMAScript符合性是什么意思**

- 支持ECMA-262中描述的所有“类型、值、对象、属性、函数、以及程序语法与语义“
- 支持Unicode字符标准

此外符合性实现还可以满足下列要求：

- 增加ECMA-262中未提及的“额外的类型、值、对象、属性、函数“
- 支持ECMA-262中没有定义的“程序和正则表达式语法“，意思是可以修改和扩展内置的正则表达式特性。

以上条件为实现开发基于ECMAScript开发语言提供了极大的权限和灵活度，也是其广受欢迎的原因之一。

**浏览器对ECMAScript的支持**

略……

### 1.2.2 DOM

文档对象模型DOM（Documnet Object Model）是一个应用编程接口（API），用于在HTML中使用扩展的XML。DOM将整个页面抽象为一组分层节点。HTML或XML页面中的每个组成部分都是一种节点，包含着不同的数据。

DOM通过创建表示文档的树，让开发者随心所欲控制网页的结构和内容。使用DOM API可以轻松的删除、增加、替换、修改节点。

**为什么DOM是必需的**

在IE4和Navigator  4支持不同形式的动态HTML的情况下，开发者首页可以做到不刷新页面去修改页面的外观和内容。这代表着Web技术的巨大进步，也暴露的了很大的问题，由于网景和微软采用不同的思路开发DHTML，开发者写一个HTML页面就可以在任何浏览器上顺利运行成为了问题。

为了保证Web跨平台的本性，W3C开始了制定DOM标准的进程。

**DOM级别**

- DOM1级：DOM Core 和 DOM HTML。
- DOM2级：DOM视图、DOM事件、DOM样式、DOM范围和遍历
- DOM3级：进一步扩展DOM，引入了以统一方式加载和保存文档的方法、新增了验证文档的方法、对DOM Core进行了扩展

**其他DOM**

- 可伸缩矢量图（SVG）
- 数学标记语言（MathML）
- 同步多媒体集成语言（SMIL）

**Web浏览器对DOM的支持情况**

随着历史的发展各大浏览器厂商都已经支持了DOM。

### 1.2.3 BOM

IE3和Netscape Navigator  3提供了**浏览器对象模型（BOM）API**，用于支持访问和操作浏览器的窗口。

使用BOM，开发者可以操控浏览器显示页面之外的部分。

BOM是唯一一个没有相关标准的JavaScript实现，HTML5的出现改变了这个局面，这个版本的HTML以正式规范的形式涵盖了尽可能多的BOM特性。由于HTML5的出现，之前很多与BOM有关的问题都迎刃而解了。

总体来说，BOM主要针对浏览器窗口和子窗口（frame）BOM所具备的一些能力如下：

- 弹出新浏览器窗口的能力
- 移动、缩放和关闭浏览器窗口的能力
- navigator对象，提供关于浏览器的详尽信息
- location对象，提供浏览器加载界面的详尽信息
- screen对象，提供关于用户屏幕分辨率的详尽信息
- performance对象，提供浏览器内存占用、导航行为和时间统计的详尽信息
- 对cookie的支持
- 其他自定义对象，如XMLHttpRequest和IE的AcitiveXObject

## 1.3 JavaScript版本

作为网景的继承者，Mozilla是唯一仍在延续最初JavaScript版本编号的浏览器厂商。

当初网景在开源其源代码时，JavaScript在浏览器中的最后版本时1.3。

后续Mozilla Foundation在持续开发JavaScript，为其增加新特性、关键字以及语法，所以JavaScript版本号也一直在不断递增。

随着JavaScript的发展，JavaScript2.0作为一个目标已经不存在了，而相应的版本号编排方式也在Firefox4.0发布后终止了。

## 1.4 小结

JavaScript是一门用来和网页交互的脚本语言，包含一下三个组成部分：

- ECMAScript：由ECMA-262定义并提供核心功能
- 文档对象模型（DOM）：提供与网页内容交互的方法和接口
- 浏览器对象模型（BOM）：提供与浏览器交互的方法和接口
