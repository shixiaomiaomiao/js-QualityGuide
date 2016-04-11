# js-QualityGuide
> 原文英文地址：https://github.com/bevacqua/js
这篇指南旨在为JavaScript代码的使用提供基本规则，从而保证它的良好的可读性，同时在一个团队中的不同开发者之间保持一致。本文的重点立足于js的代码质量和js应用中的各部分一致性。

# 目标

以下的这些建议不是一成不变的，它们旨在为您提供一个基线使得您能够写出更加具有风格一致性的js代码。为了使效果最大化，将这些规范与您的同事一起分享，并且尝试着去执行它们。当然，不要沉迷于代码风格，不然的话，后果只能是无功而返并且适得其反。试着找寻一个能够使全组的人都感到舒适的切合点来一起开发代码，而不是感受到崩溃，因为他们在一个不该加空格的地方加了空格从而使代码总是无法通过“自动检测”。它是一个很薄的一行，但它是一个很好的个人线，我将它留给你，任由你描绘。

#内容列表
1. [模块](#modules)
2. [严格模式](#strict)
3. [间距](#spacing)
4. [分号](#semicolons)
5. [风格检查](#stylecheck)
6. [Linting](#linting)
7. [字符串](#string)
8. [变量声明](#varDeclaration)
9. [条件](#conditions)
10. [相等](#equality)
11. [三元操作符](#ternaryoperatos)
12. [函数](#functions)
13. [原型](#prototype)
14. [对象字面量](#objectliterals)
15. [数组字面量](#arrayliterals)
16. [正则表达式](#regularexpressions)
17. [console声明](#console)
18. [注释](#comments)
19. [变量命名](#varibalenaming)
20. [Polyfills](#polyfills)
21. [日常小技巧](#everydaytricks)
22. [许可证](#license)

<a href = '#modules' id = 'modules'></a>
#模块
***
这个风格指南假设你正在使用一个模块系统，例如：[CommonJS](http://wiki.commonjs.org/wiki/CommonJS),[AMD](http://requirejs.org/docs/whyamd.html),[ES6 Modules](https://eviltrout.com/2014/05/03/getting-started-with-es6.html),或者其它类型的模块系统。模块系统提供私有作用域，避免泄露到全局对象中，通过自动生成的依赖图来提高代码的基本组织，而不是人为地创建许多\<script\>标签。

模块系统也能为我们提供依赖注入模式，这对于单元模块的独立测试至关重要。

<a href = '#strict' id = 'strict'></a>
#严格模式
记住总是将\'use strict\'放在你的模块的顶端。严格模式能够帮你捕捉到无意义的行为，阻止差劲的实践，而且更加快速，因为它允许编译器对你的代码做出一定程度的假设。

<a href = '#spacing' id = 'spacing'></a>
#间距
***
间距在一个应用的每个文件中必须保持一致。为此，使用\.editorconfig等配置文件是极为被鼓励的。下面是我所建议的默认以javascript缩进开始。

    #editorconfig.org
    root = true
    
    [*]
    indent_style = space
    indent_size = 2
    end_of_line = lf
    charset = utf-8
    trim_trailing_whitespace = true
    insert_final_newline = true
    
    [*.md]
    trim_trailing_whitespace = false
    
设置tabs或k空格取决于项目的特性，但是我建议使用2个空格符来实现缩进。这一点\.editorconfig文件能够为我们注意到。并且每一个人都可以通过按tab键来创造一个正确的间距。

间距不只是需要按tab键，还需要在函数声明参数的前、后和之间设置空格。这种间距通常来说与代码执行正确与否完全无关，所以对于大多数的团队来说，达成一个能够让每个人都满意的机制非常困难。

    function () {}
    
    function( a, b ){}
    
    function(a, b) {}
    
    function(a,b) {}
    
试着将上述的写法的不同降到最小，但是也不用对其细想过多。

如果可能地话，将每行的字符数控制在80以下，提高可阅读性。

<a href = '#semicolons' id = 'semicolons'></a>
#分号 ；

大多数的JavaScript程序员都喜欢使用分号\;。这样做可以避免ASI（自动分号注入）可能带来的问题。如果你决定不使用分号，[请确保你理解ASI规则](http://blog.izs.me/post/2353458699/an-open-letter-to-javascript-leaders-regarding)。

不管你的选择如何，应该用一个linter来捕获不必要的或无意义的分号。

<a href = '#stylecheck' id = 'stylecheck'></a>
#风格检查
<b>不要！</b>严肃地说，代码风格检查对于涉及的每一个人来说都是极度痛苦的，同时执行这样严厉的政策得不到任何可见的收获。


<a href = '#linting' id = 'linting'></a>
#Linting
