# js-QualityGuide
> 原文英文地址：https://github.com/bevacqua/js

这篇指南旨在为JavaScript代码的使用提供基本规则，从而保证它的良好的可读性，同时在一个团队中的不同开发者之间保持一致。本文的重点立足于js的代码质量和js应用中的各部分一致性。

# 目标
以下的这些建议不是一成不变的，它们旨在为您提供一个基线使得您能够写出更加具有风格一致性的js代码。为了使效果最大化，将这些规范与您的同事一起分享，并且尝试着去执行它们。当然，不要沉迷于代码风格，不然的话，后果只能是无功而返并且适得其反。试着找寻一个能够使全组的人都感到舒适的切合点来一起开发代码，而不是感受到崩溃，因为他们在一个不该加空格的地方加了空格从而使代码总是无法通过“自动检测”。它是一个很薄的一行，但它是一个很好的个人线，我将它留给你，任由你描绘。

#内容列表
1. [模块](#modules)
2. [严格模式](#strict)
3. [空格](#spacing)
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
这个风格指南假设你正在使用一个模块系统，例如：[CommonJS](http://wiki.commonjs.org/wiki/CommonJS),[AMD](http://requirejs.org/docs/whyamd.html),[ES6 Modules](https://eviltrout.com/2014/05/03/getting-started-with-es6.html),或者其它类型的模块系统。模块系统提供私有作用域，避免泄露到全局对象中，通过自动生成的依赖图来提高代码的基本组织，而不是人为地创建许多\<script\>标签。

模块系统也能为我们提供依赖注入模式，这对于独立地测试单元模块至关重要。

<a href = '#strict' id = 'strcit'></a>
#严格模式
记住总是将\'use strict\'放在你的模块的顶端。严格模式能够帮你捕捉到无意义的行为，阻止差劲的实践，而且更加快速，因为它允许编译器对你的代码做出一定程度的假设。

<a href = '#spacing' id = 'spacing'></a>
#空格

