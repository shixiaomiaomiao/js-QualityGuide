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
11. [三元操作符](#ternaryoperators)
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
            var initial = args.shift();
            
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
保持变量声明方式的一致性，并且在作用域的顶部声明。鼓励变量声明执行"一个变量一行"原则。逗号在前，单个var声明，多个var声明，这些都是可以的，只要在项目中保持一致，并且确保团队一致就好。

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

<b>好的写法</b>
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

<b>不好的写法</b>

        if (err) throw err;

<b>好的写法</b>

        if(err) { throw err; }
        
从文本理解角度来考虑，避免条件语句出现在单独一行将更加好。

<b>更好的写法</b>

        if (err) {
            throw err;
        }

<a href = '#equality' id = 'equality'></a>
#相等
避免使用 == 和!= 操作符，而使用 === 和 ！== 。 === 和 ！== 操作符被称为"严格相等操作符"，而 == 和 ！= 操作符则[尝试将比较的变量转化成相同类型](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comparison_Operators)。

<b>不好的写法</b>

        function isEmptyString (text) {
            return text == '';
        }
        
        isEmptyString(0);
        // <- true
        
<b>好的写法</b>

        function isEmptyString (text) {
            return text === '';
        }
        
        isEmptyString(0);
        //<- false
    
<a href = '#ternaryoperators' id = 'ternaryoperators'></a>
#三元操作符

对于确定情况操作，三元操作符还好理解；但是对于复杂的选择，三元操作符就不好令人接受了。记住这样一个准则，如果一眼扫过去，你的大脑能够立即解析出结果就用三元操作符声明，有些时候如果太过复杂，则难以理解。

jQuery就是[一个充满着令人恼火的三元操作符的代码库的典型例子](https://github.com/jquery/jquery/blob/c869a1ef8a031342e817a2c063179a787ff57239/src/ajax.js#L117)

<b>不好的写法</b>

        function calculate (a, b) {
            return a && b ? 11 : a ? 10 : b ? 1 : 0;
        }
        
<b>好的写法</b>

        function getName (mobile) {
            return mobile ? mobile.name : 'Generic Player';
        }

如果使用三元操作符会增加令人理解的复杂度的话，请使用 if/else 代替。

<a href = '#functions' id = 'functions'></a>
#函数
当声明一个函数时，记住使用[函数声明形式](http://stackoverflow.com/q/336859/389745)而不是[函数表达式](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/function)。因为[声明提前](https://github.com/buildfirst/buildfirst/tree/master/ch05/04_hoisting)。

<b>不好的写法</b>

        var sum = function (x, y) {
            return x + y;
        }
        
<b>好的写法</b>

        function sum (x, y) {
            return x + y;
        }

但是，使用函数表达式没有任何错误，只是会[套用另一种函数](http://ejohn.org/blog/partial-functions-in-javascript/).

<b>好的写法</b>

        var plusThree = sum.bind(null,3);
请记住：[函数声明会提前](https://github.com/buildfirst/buildfirst/tree/master/ch05/04_hoisting)至作用域的最顶端。所以，他们定义和使用的顺序不是最重要的。尽管如此，但你仍然应该将函数卸载作用域的顶部，避免将它们之于条件语句中。

<b>不好的写法</b>

        if (Math.random() > 0.5) {
            sum(1, 3);
            
            function sum (x, y) {
                return x + y;
            }
        }
        
<b>好的写法</b>

        if(Math.random() > 0.5) {
            sum(1, 3);
        }
        
        function sum (x, y) {
            return x + y;
        }



        function sum (x, y) {
            return x + y;
        }
        
        if (Math.random() > 0.5) {
            sum(1, 3);
        }
        
如果你需要一个"no-op"(无操作)方法，你可以使用Function.prototype或者是function noop () {}.理想情况下，对于noop函数的一个引用在应用中贯穿始终。

不管何时如果你需要操作一个类数组对象，将其丢入数组中。

<b>不好的写法</b>

        var divs = document.querySelectorAll('div');
        
        for (i = 0; i < divs.length; i++) {
            console.log(divs[i].innerHTML);
        }
        
<b>好的写法</b>

        var divs = document.querySelectorAll('div');
        
        [].slice.call(divs).forEach(function (div) {
            console.log(div.innerHTML);
        })
        
不管怎样，请记住在V8环境中， 对arguments 使用这种方法将会存在[很大的性能影响](https://github.com/petkaantonov/bluebird/wiki/Optimization-killers#3-managing-arguments) 。
当性能是首要考虑的因素时，避免对arguments使用 slice方法，相反地使用 for 循环。

<b>不好的写法</b>

        var args = [].slice.call(arguments);
        
<b>好的写法</b>

        var i;
        var args = new Array(arguments.length);
        for (i = 0; i < args.length; i++) {
            args[i] = arguments[i];
        }
        
        
不要在循环里声明函数。(why ? )
<b>不好的写法</b>

        var values = [1, 2, 3];
        var i;
        
        for(i = 0; i < values.length; i++) {
            setTimeout(function() {
                console.log(values[i]);
            }, 1000 * i);
        }
        
        var values = [1, 2, 3];
        var i;
        
        for (i = 0; i < values.length; i++) {
            setTimeout(function (i) {
                return function () {
                    console.log(values[i]);
                }
            }(i), 1000 * i);
        }
<b>好的写法</b>

        var values = [1, 2, 3];
        var i;
        
        for(i = 0; i < values.length; i++) {
            setTimeout(function (i) {
                console.log(values[i]);
            },1000 * i, i);
        }
        
        var values = [1, 2, 3];
        var i;
        
        for (i = 0; i < values.length; i++) {
            wait(i);
        }
        
        function wait (i) {
            setTimeout(function () {
                console.log(values[i]);
            }, 1000 * i);
        }
[setTimeout的第三个参数](http://www.cnblogs.com/shixiaomiao/p/5393201.html)
或者更好的，只用.forEach方法，它不会像在for循环中定义函数产生一样的警告。
<b>更好的写法</b>

        [1, 2, 3].forEach(function (value, i) {
            setTimeout(function () {
                console.log(value);
            },1000 * i);
        });
不管一个函数是否是极其复杂的，尽量使用一个显示命名的函数声明而不是一个匿名函数。在显示命名的函数中，分析堆栈跟踪时，指明意外情况发生的根本原因将变得更加容易。
<b>不好的写法</b>

        function once (fn) {
            var ran = false;
            return function () {
                if (ran) { return };
                ran = true;
                fn.apply(this, arguments);
            };
        }
<b>好的写法</b>

        function once (fn) {
            var ran = false;
            return function run() {
                if (ran) { return };
                ran = true;
                fn.apply(this, arguments);
            }
        }
        
通过使用卫语句(guard clauses)来避免出现太多的条件缩进，而不是用流动的if块。
卫语句： 如果某个条件极其罕见，就应该单独检查该条件，并在该条件为真时立刻从函数中返回。

<b>不好的写法</b>

        if (car) {
            if (black) {
                if (turbine) {
                    return 'batman!';
                }
            }
        }
        if (condition) {
            // 10+ lines of code
        }
<b>好的写法</b>

        if (!car) {
            return;
        }
        if (!black) {
            return;
        }
        if (!turbine) {
            return;
        }
        return 'batman!'
        if (!condition) {
            return;
        }
        // 10+ lines of code
        
<a href = 'prototype' id = 'prototype'></a>
#原型
解析原生原型应该不惜一切代价的避免这么做，使用方法代替。如果你必须以原生的方式扩展函数，试着使用其他的方式，例如[poser](https://github.com/bevacqua/poser)(此处原作者有打广告嫌疑，poser是原作者开发的模块)
<b>不好的写法</b>

        String.prototype.half = function () {
            return this.substr(0, this.length /2);
        }

<b>好的写法</b>

        function half (text) {
            return text.substr(0, text.length /2);
        }
        
<b>避免使用原型继承模型</b>，除非你具有非常好的性能原因来证明你自己。
-原型继承对this具有很高的依赖，需要依赖this与外界联系
-比使用普通的objects对象更加冗长
-当new一个对象时，将产生令人头痛的麻烦
-需要终止隐藏实例有价值的私有状态(private state)
-只使用普通的objects对象

<a href = '#objectliterals' id = 'objectliterals'></a>
#字面对象量
使用 埃及符号{}来实例化对象。使用工厂函数而不是构造函数，以下是我建议的方案来在通常情况下实现objects对象。

        function util (options) {
            //私有方法写在这里
            var foo;
            
            function add () {
                return foo++;
            }
            
            function reset () {   //注意这个方法不是显示暴露的
                foo = options.start || 0;
            }
            
            reset();
            
            return {
                //共有接口方法写在这里
                uuid : add
            };
        }

<a href = '#arrayliterals' id = 'arrayliterals'></a>
#数组字面量
使用方括号符号来实例化一个数组。如果你处于性能原因必须声明一个确定好维数的数组，那么使用new Array(length)的方式来定义比较好。

        //注意区别
        var a = [];
        a instanceof Array;  //true
        var b = 'ss';
        typeof b; //string
        b instanceof String ; // false
        
是时候你该掌握数组操作啦！[学习更多的基础](https://ponyfoo.com/articles/fun-with-native-arrays)这比你想的要更加地容易。
-[.forEach](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)
-[.slice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)
-[.splice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)
-[.join](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/join)
-[.concat](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat)
-[.unshift](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/unshift)
-[.shift](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/shift)
-[.push](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/push)
-[.pop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/pop)

学习和使用函数集合操作的方法。这些是非常值得麻烦。
