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
9. [条件语句](#conditionals)
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

模块系统也能为我们提供依赖注入模式，这对于单元模块的独立测试至关重要。

<a href = '#strict' id = 'strict'></a>
#严格模式
记住总是将\'use strict\'放在你的模块的顶端。严格模式能够帮你捕捉到无意义的行为，阻止差劲的实践，而且更加快速，因为它允许编译器对你的代码做出一定程度的假设。

<a href = '#spacing' id = 'spacing'></a>
#间距
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
<b>不要！</b>严肃地说，代码风格检查对于每一个相关人员来说都是极度痛苦的，同时执行这样严厉的政策得不到任何可见的收获。


<a href = '#linting' id = 'linting'></a>
#Linting
另一方面，Linting有时是必须的。再一次重申，不要使用一个对代码风格有极度控制要求的linter,比如说[jslint](http://www.jslint.com/)。相反地，要使用一些更加宽容的linter，比如：[jshint](https://github.com/jshint/jshint/)或者[eslint](https://github.com/jshint/jshint/)。

以下是在使用JSHint时的一些提示：
* 声明一个\.jshintignore文件，将类似于node_modules、bower_components的文件包含进去
* 你可以使用如下的一个.jshintrc文件来和你的规则一起使用
       
        #以下配置的意义参考：https://github.com/jshint/jshint/blob/master/examples/.jshintrc
        {
            "curly": true,          //对于新的块或作用域必须加{}
            "eqeqeq": true,         //在变量比较时必须使用'==='
            "newcap": true,         //对于构造函数首字母必须大写
            "noarg": true,          //禁止使用'arguments.caller'和'arguments.callee'
            "noempty": true,        //禁止使用空的块
            "nonew": true,          //禁止使用不起作用(没有赋值)的构造函数
            "sub": true,            //允许使用'[]'符号，即使是可以用点符号代替
            "undef": true,          //要求所有的非全局变量都必须声明（防止全局泄露）
            "unused": true,         //未使用的变量； true-所有的变量和最后一个函数参数；vars-只是所有的变量;strict-所有的变量和所有的函数参数         
            "trailing": true,       // ？
            "boss": true,           //在比较的地方允许赋值
            "equnull": true,        //允许使用'== null'
            "strict": true,         //要求所有的函数在ES5的严格模式下运行
            "immed": true,          //要求立即执行的函数要用()包裹，eg : '(function () {} ())'
            "expr": true,           //允许表达式声明作为程序
            "latedef": "nofunc",    //要求变量非函数在使用前要先被定义
            "quotmark": "single",   // 引号一致性; 'single'-单引号；'double'-双引号；false-不做检查（默认）；true-要求一致；
            "indent": 2,            //缩进？
            "node": true            //是否是node.js 
        }

这些规则绝对不是你所必须遵循的，但是你必须在根本不用linting和不写出超级难看的代码风格之间找到一个 合适的平衡点。（sweet spot）

<a href = '#string' id = 'string'></a>
#字符串

字符串的引用需要使用相同的引用符号，使用\'或者\" ，并且在你的代码中始终一致。确保团队中的人在每一处的Javascript处都是用相同的引用标记。

<b>不好的写法</b>
        var message = 'oh hai ' + name + "!";
        
<b>好的写法</b>
        var message = 'oh hai ' + name + '!';
    
通常情况下，如果你使用例如[util.format in Node](nodejs.org/api/util.html#util_util_format_format)等参数替换方法，你将成为一个更快乐的Javascript开发者。使用这种方式将更加容易格式化你的字符串，并且使得代码看起来更加整洁。

<b>更好的写法</b>

        var message = util.format('oh hai %s!', name);
        
如果不用util接口，你可以使用以下的代码实现类似的功能。

        function format () {
            var args = [].slice.call(arguments);
            var initial = args.shif();
            
            function replacer (text, replacement) {
                return text.replace('%s', replacement);
            }
            return args.reduce(replacer, initial);
        }
        
声明多行的字符串，尤其是对于HTML片段，有时最好是将他们先组成作为一个buffer数组，然后在join在一起。用字符串连接的方式也许更快，但是也更加难以追踪。

        var html = [
            '<div>',
                format('<span class = "monster">%s<span>', name),
            '</div>'
        ].join('');
        
利用这种建立数组的风格，你可以将片段推入到数组中，在最后将所有的东西组合在一起。这实际上就是[一些模板引擎例如Jade](https://github.com/jadejs/jade)喜欢做的事情。

<a href = '#varDeclaration' id = 'varDeclaration'></a>
#变量声明
保持变量声明方式的一致性，并且在作用域的顶部声明。鼓励变量声明执行\"一个变量一行\"原则。逗号在前，单个var声明，多个var声明，这些都是可以的，只要在项目中保持一致，并且确保团队一致就好。

<b>不好的写法</b>
        var foo = 1,
            bar = 2;
            
        var baz;
        var pony;
        
        var a 
            , b;
            
        var foo = 1;
        
        if (foo > 1) {
            var bar = 2;
        }

<b>好的写好</b>
只是因为他们相互之间一致，并不是因为风格一致。

        var foo = 1;
        var bar = 2;
        
        var baz;
        var pony;
        
        var foo = 1;
        var baz;
        
        if (foo > 1) {
            bar = 2;
        }
声明变量时不及时赋值也是可以接受的，并且与其他代码一样占有一行。

<b>可接受的</b>
        var a = 'a';
        var b = 2;
        var i, j;
        
<a href = '#conditionals' id = 'conditionals'></a>
#条件语句
大括号是必须要有的。使用大括号再加上合理的空格策略将帮助你避免例如[Apple's SSL/TLS bug](https://www.imperialviolet.org/2014/02/22/applebug.html)。

<b>不好的写好</b>
        if (err) throw err;

<b>好的写好</b>
        if(err) { throw err; }
        



