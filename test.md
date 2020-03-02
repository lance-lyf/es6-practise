## ECMAScript 6 简介
>ECMAScript 6.0(以下简称ES6)是JavaScript语言的下一代标准，已经在2015年6月正式发布了，它的目标，是使得JavaScript语言可以用来编写复杂的大型应用程序，成为企业及开发语言。
### 1.ECMAScript和javaScript的关系
>一个常见的问题是，ECMAScirpt和javaScript到底是什么关系？

>要讲清楚这个问题，需要回顾历史，1996年11月，javaScript的创造者Netscape公司，决定将javaScript提交个标准化组织ECMA，希望这种语言能够成为国际标准，次年ECMA发布262号标准文件（ECMA-262)的第一版，规定了浏览器脚本语言的标准，并将这种语言称为ECMAScript，这个版本就是1.0版，该标准从一开始就是针对JavaScript语言制定的，但是之所以不叫JavaScript，有两个原因。一个是商标，Java和Sun公司的商标，根据授权协议，只有Netscape公司可以合法使用JavaScript这个名字，且JavaScript本身也已经被Netscape公司注册为商标。二是想要体现这门语言的制定者是ECMA，不是Netscape，这样有利于保证这门语言的开放性和中立性。

>因此，ECMAScript和JavaScript的关系是，前者是后者的规格，后者是前者的一种实现(另外的ECMAScript方言还有JScript和ActionScript)。日常场合，这两个词是可以互换得到。

### 2.ES6和ECMAScript 2015的关系

> ECMAScript 2015 （简称ES2015)这个词，也是经常可以看到的，它与ES6是什么关系呢？

> 2011年,ECMAScript5.1版本发布后，就开始制定6.0版了，因此，ES6这个词的愿意，就是值JavaScript语言的下一个版本。

> 但是，因为这个版本引入的语法功能太多，而且制定过程当中，还有很多组织和个人不断提交新功能。事情很快就变得清楚了，不可能在一个版本里面包括所有将要引入的功能。
常规的做法是先发布6.0版，过一段时间再发6.1版，然后6.2版，6.3版等等。

>但是标准的制定者不想这样做。他们想让标准的升级成为常规流程： 任何热在任何时候，都可以向标准委员会提交新语法的天，然后标准委员会每个月开一次会，
评估这些提案是否可以接受，需要哪些改进。如果经过多次会议以后，一个提案足够成熟了，就可以正式进入标准了。这就是说，标准的版本升级成为了一个不断滚动的流程，每个月都会有变动。

>标准委员会最终决定，标准在每年的6月份正式发布一次，作为当年的正式版本。接下来的时间，就在这个版本的基础上做改动，直到下一年的6月份，草案就自然变成了新一年的版本。
这样一来，就不需要以前的版本号了，只要用年份标记就可以了。

>ES6的第一个版本，就这样在2015年6月发布了，正式名称就是（ECMAScript 2015标准）（简称ES2015)。2016年6月，小幅修订的(ECMAScirpt 2016标准)。根据计划，2017年6月发布ES2017标准。

>因此，ES6即使一个历史名词，也是一个泛指，含义是5.1版本以后的JavaScrit的下一代标准，涵盖了ES2015、ES2016、ES2017等等，而ES2015则是正式的名称。
特指该年发布的正式版本的语言标准，本书中提到ES6的地方，一般是指ES2015标准，但有时也是泛指**下一代JavaScript语言**

### 3.语法提案的批准流程

>任何人都可以向标准委员会（又成TC39委员会）提案，要求修改语言标准。

>一种新的语法从提案到变成正确标准，需要经过五个阶段，每个阶段的变动都需要由TC39委员会批准。
* Stage 0 - strawman(展示阶段)
* Stage 1 - Proposal(征求意见阶段)
* Stage 2 - Draft(草案阶段)
* Stage 3 - Candidate(候选人阶段)
* Stage 4 - Finished(定案阶段)
>一个提案只要能进入Stage 2，就差不多肯定会包括在以后的正式标准里面。
>ECMAScript当前的所有提案，可以在TC39的官方网站GitHub.com/tc39/ecma262查看。
>本练习介绍5.1版本以后所有的新语法。对于那些明确或很有希望，将列入标准的新语法，都将予以介绍。

>目前各大浏览器ES6的支持可以查看[es6兼容](kangax.github.io/compat-table/es6/).

>Node.js是JavaScript的服务器运行环境（runtime)。它对ES6的支持最高，除了那些默认打开的功能。

## 一、let 和 const命令

### 1.let命令

#### 基本用法

>ES6新增了let命令，用来声明变量，它的用法类似于var，但是所声明的变量，只在let命令所
>在的代码块内有效。

    {
        let a = 10;
        var b = 1;
    }
    console.log(a);
    console.log(b);
>上面代码在代码块中，分别用let和var声明了两个变量。然后在代码块之外调用这两个变量。
>结果let声明的变量报错，var声明的变量返回了正确的值。这表明，let声明的变量只在它
>所在的代码块有效

    for循环计数器，就很合适使用let命令
    for (let i = 0; i < 10; i++) {
           
    }
    console.log(i);
>上面代码中，计数器i只在for循环体内有效，在循环体外引用就会报错。
>下面的代码如果使用var,最后输出的时10

      var a =[];
       for (var i = 0; i < 10; i++) {
           a[i] = function (){
               console.log(i);
           }
       }
       a[6]();
>上面代码中，变量i是var命令声明的，在全局范围内都有效，所以全局只有一个变量i。
>每一次循环，变量i的值都会发生改变，而循环内被赋给数组a的函数内部的console.log(i),
>里面的i指向的就是全局的i。也就是说，所有数组a的成员里面的i，指向的都是同一个i，
>导致运行时输出的最后一轮的i的值，也就是10。

>如果使用let，声明的变量仅在块级作用域内有效，最后输出的时6

      var a =[];
       for (let i = 0; i < 10; i++) {
           a[i] = function (){
               console.log(i);
           }
       }
       a[6]();
>上面代码中，变量i是let声明的，当时的i只在本轮循环有效，所以每一次循环的i其实都是一个新的变量，
>所以最后输出的时6，你可能会稳，如果每一轮循环的变量i都是重新声明的，那它怎么知道上一轮循环的值，从而计算出
>本轮循环的值？这是因为JavaScript引擎内部会记住上一轮循环的值，初始化本轮得到变量i时，就在上一轮
>循环的基础上进行计算。

>另外，for循环还有一个特别之处，就是设置循环变量的那部份是一个父作用域，而循环体内是一个单独的子作用域。

#### 不存在变量提升

>var 命令会发生"变量提升"现象，即变量可以在声明之前使用，值为undefined。这种现象多多少少
>是有些奇怪的，按照一般的逻辑，变量应该在声明语句之后才可以使用。

>为了纠正这种现象，let命令改变了语法行为，它所声明的变量一定要在声明后使用，否则报错。

    console.log(foo);
    var foo = 2;
    console.log(bar);
    let bar = 2;
>上面代码中，变量foo用var命令声明，会发生变量提升，即脚本开始运行时，变量foo已经存在了，但是
>没有值，所以会输出undefined。变量bar用let命令声明，不会发生变量提升，这个表示在声明它之前，变量
>bar是不存在的，这时如果用到它，就会抛出一个错误。

#### 暂时性死区

>只有块状作用域内存在let命令，它所声明的变量就"绑定"这个区域，不再受外部的影响。

    var tmp = 123;

    if(true){
        tmp = "abc";
        let tmp;
    }

>上面代码中，存在全局变量tmp,但是块级作用域内let又声明了一个局部变量tmp，导致后者绑定这个
>块级作用域，所以在let声明变量前，对tmp赋值会报错。

>es6明确规定，如果区块中存在let和const命令，这个区块对这个鞋命令声明的变量，从一开始就形成了
>封闭作用域，凡是在声明之前就使用这些变量，就会报错。

>总之，在代码块内，使用let命令声明变量之前，改变量都是不可用的，这在语法上，称为“暂时性死区”
>(temporal dead zone 简称 TDZ)

>上面代码中，在let命令声明变量tmp之前，都属于tmp的"死区"。
>“暂时性死去”也意味着typeof不再是一个百分之百安全的操作。

    typeof x;
    let x;
>上面代码中，变量x使用let命令声明，所以在声明之前，都属于x的死区，只要用到该变量就会报错。
>因此,typeof运行时就会抛出一个ReferenceError。

>作为比较，如果一个变量根本没有被声明，使用typeof反而不会报错

    console.log(typeof x);
>上面代码中，x是一个不存在的变量名，结果返回“undefined"。所以，在没有let之前，
>typeof运算符是百分之百安全的，永远不会报错，现在这一点不成立了。这样的设计是为了让大家养成
>良好的编程习惯，变量一定要在声明之后使用，否则就报错。

>有些死区比较隐蔽，不太容易发现。

    function bar(x=y,y=2){
        return [x,y]
    }
    bar();
>上面代码中，调用bar函数之所以报错（某些实现可能不报错），是因为参数x默认值等于另一个参数y
>而此时y还没有声明，属于"死区"。如果y的默认值是x，就不会报错,因为此时x已经声明了。
    
    function bar(x=2,y=x){
        return [x,y];
    }
    bar();
>另外，下面的代码也会报错，与let的行为不同。

    let x = x;
>上面代码报错，也是因为暂时性死去，使用let声明变量时，只要变量在还没有声明完成前使用，
>就会报错。上面这行属于这个情况，在变量x的声明语句还没有执行完成前，就去取x的值，导致报错。

#### 不允许重复声明

>let 不允许在相同作用域内，重复声明同一个变量。
    
    function func(){
           let a = 10;
           var a = 1;
       }
>因此，不能再函数内部重复声明参数

    function func(arg){
          let arg;
    }//报错
     function func(arg) {
            {
                let arg;
            }
    }//不报错
### 2.块级作用域
#### 为什么需要块级作用域？
>ES5只有全局作用域和函数作用域，没有块级作用域，这带来很多不合理的场景。
>第一个场景内层变量可能会覆盖外层变量。

     var tmp = new Date();
        function f(){
            console.log(tmp);
            if(false){
                var tmp = "hello world"
            }
        }
        f();
>上面代码的愿意是，if代码块的外部使用外层的tmp变量，内部使用内层的tmp变量，但是
>函数f执行后，输出结果为undefined，愿意在于变量提升，导致内层的tmp变量覆盖了外层的tmp变量。

>第二个场景，用来计数的循环变量泄露为全局变量。

    var s = "hello";
    for(var i = 0; i < s.length; i++){
        console.log(s[i]);
    }
    console.log(i);
>上面代码中，变量i只用来控制循环，但是循环结束后，它并没有消失，泄露成了全局变量。
#### ES6的块级作用域
>let实际上为JavaScript新增了块级作用域。

        function f1(){
            let n = 5;
            if(true){
                let n = 10;
            }
            console.log(n);
        }
        f1();
>上面的函数有两个代码块，都声明了变量n，运行后输出5。这表示外层代码块不受内层代码块的影响。
>如果两次都使用var定义变量n，最后输的值为10。

>ES6允许块级作用域的任意嵌套

    {{{{
        {let insame = 'hello world'}
        console.log(insame);
    }}}}
>上面代码使用了一个五层的块级作用域，每一层都是一个单独的作用域，第四层作用域无法读取第五层作用域的内部变量。
    {{{{
        let insame = 'hello'
           {let insame = 'hello world'}
           console.log(insame);
       }}}}
>块级作用域的出现，实际上使得获得广泛应用的匿名立即执行函数表达式（匿名IIFE）不再必要了。
    //IIFE的写法
      (function (){
            var tmp = 1;
      })()
    //块级作用域的写法
      {
            let tmp = 1;         
      }
#### 块级作用域与函数声明

>函数能不能在块级作用域中声明？这是一个相当令人混淆的问题。

>ES5规定，函数只能在顶层作用域和函数作用域之中声明，不能在块级作用域声明。

    if(true){
            function f(){}
        }
        try{
            function f(){}
        }catch(e){
            //...
        }
>上面两种函数声明，根据ES5的规定都是非法的。

>但是，浏览器没有遵守这个规定，为了兼容以前的旧代码，还是支持在块状作用域之中声明函数，因此上面两种情况实际都能运行，不会报错。

>es6引入块状作用域，明确允许在块级作用域之中声明函数。ES6规定，块级作用域之中，函数声明语句的行为类似于let，在块级作用域之外不可引用。

     function f() {
            console.log('i am outside');
        }
        (function () {
            if (false) {
                function f() {
                    console.log('i am inside');
                }
            }

            f();
        })()
>上面代码在ES5中运行，会得到"I am inside",因为在if内声明的函数f会被提升到函数头部，实际运行的代码如下。

    //ES5环境
     function f() {
            console.log('i am outside');
        }
        (function () {
            function f() {
                console.log('i am inside');
            }
            if (false) {
               
            }
            f();
        })() // i am inside
>ES6就完全不一样了，理论上会得到“I am outside".因为快状作用域内声明的函数类似于let,
>对作用域之外没有影响，但是，如果你真的在ES6浏览器中运行一下上面的代码，是会报错的,
>这是为什么呢？

    //浏览器的ES6环境
    function f() {
            console.log('i am outside');
        }
        (function () {
            if (false) {
                function f() {
                    console.log('i am inside');
                }
            }
            f();
        })()//Uncaught TypeError f is not a function
>上面的代码在ES6浏览器中，都会报错。

>原来，如果改变了块级作用域内声明的函数的处理规则，显然会对老代码产生很大影响，为了减轻
>因此产生的不兼容问题，ES6在附录B里面规定，浏览器的实现可以不遵守上面的规定，有自己的行
>为方式。
* 允许在块状作用域内声明函数。
* 函数声明类似于Var,即会提升到全局作用域或函数作用域的头部。
* 同时，函数声明还会提升到所在的块级作用域的头部。

>**注意，上面三条规则只对ES6的浏览器实现有效，其它环境的实现不用遵守，还是将块级作用域的函数声明当做let处理。**

>根据这三条规则，浏览器的ES6环境中，块级作用域内声明的函数，行为类似于var声明的变量。上述实际运行代码如下：
    
    //浏览器的Es6环境
     function f() {
            console.log('i am outside');
        }
        (function () {
            var f = undefined;
            if (false) {
                function f() {
                    console.log('i am inside');
                }
            }
            f();
        })()
>考虑到环境导致的行为差异太大，应该避免在块级作用域内声明函数。如果确实需要，也可以写成
>函数表达式，而不是函数声明语句。

    //块级作用域内部的函数声明语句，建议不要使用
    {
        let a = 'secret';
        function f(){
            return a;
        }
    }
    //块级作用域内部，优先使用函数表达式
    {
            let a = 'secret';

            let f = function(){
                return a;
            }
        }
>另外，还有一个需要注意的地方。ES6的块级作用域必须有大括号，如果没有大括号，JavaScript
>引擎就认为不存在块级作用。
    
    if(true) let x = 1;//报错
    if(true) {let x = 1};//第二种写法，不报错
>上面代码中，第一种写法没有大括号，所以不存在块级作用域，而let只能出现在当前作用域的顶层，
>所以报错。第二种写法有大括号，所以块状作用域成立。

>函数声明也是如此，严格模式下，函数只能声明在当前作用域的顶层。

     'use strict'
       if(true) function f(){};//报错

### 3.const 命令

#### 基本用法

> const声明一个只读的常量，一旦声明，常量的值就不能改变。

      const PI = 3.1415;
      PI = 3;
>上面代码表面改变常量的值会报错

>const声明的变量不得改变值，这意味着,const一旦声明变量，就必须立即初始化。
>不能留到以后赋值。

     const foo;//报错
>上面代码表示，对于const来说，只声明不赋值，就会报错

>const的作用域与let命令相同；只在声明所在的块状作用域内有效。

    if(true){
        const Max = 3;
    }
    Max
>const命令声明的常量也是不提升，同样存在暂时性死区，只能在声明的位置后面使用。

     if(true){
        console.log(Max);
        const Max = 3;
    }//报错，初始化前无法访问Max

>const声明的常量，也与let一样不可重复声明。

     const Max = 3;
    let Max = 4;
#### 本质

>const 实际上保证的，并不是变量的值不得改动，而是变量指向的那个内存地址保存
>的数据不得改动，对于简单类型的数据（数值、字符串、布尔值），值就保存在变量
>指向的那个内存地址，因此等于常量。但对于复合类型的数据（主要是对象和数组），
>变量指向的内存地址，保存的只是一个指向实际数据的指针，const只能保证这个指针是固定的
>(即总是指向另一个固定的地址），至于他指向的数据结构是不是可变的，就完全不能控制了，
>因此，将一个对象声明常量必须非常小心
    
    const foo = {};
    foo.prop = 123;
    foo.prop;//123
    foo = {};
>上面代码中，常量foo存储的是一个地址，这个地址指向一个对象，不可变的只是这个地址，
>即不能把foo指向另一个地址，但对象本身是可变的，所以依然可以为其添加新属性。
>下面是另外一个例子

    const a = [];
    a.push('Hello');
    a.length = 0;
    a = ['Dave']
>上面代码中，常量a是一个数组，这个数组本身是可写的，但是如果将另一个数组赋给a，就会报错。

>如果真的想将对象冻结，应该使用Obeject.freeze方法。
    
     const foo = Object.freeze({});
        //常规模式时，下面一行不起作用
        //严格模式，改行就报错
        foo.prop = 123;
>上面代码中，常量foo指向一个冻结的独享，所以添加新的属性不起作用，严格模式时，还会报错。
>除了将对象本身冻结，对象的属性也应该冻结。下面是一个将对象彻底冻结的函数。

        var constantize = (obj)=>{
           Object.freeze(obj);
           Object.keys(obj).forEach((key,i)=>{
               if(typeof obj[key]==='object'){
                   constantize(obj[key]);
               }
           })
       }

#### ES6声明变量的六种方法

>ES5只有两种声明变量的方法，var命令和function命令。ES6除了添加let和const命令，
>后面章节还会提到，另外两种声明变量的方法：import命令和class命令。
>所以，ES6一共有6中声明变量的方法。

### 4.顶层对象的属性

>顶层对象，在浏览器环境指的是window对象，在Node指的是global对象，ES5之中，顶层对象的属性与全局变量是等
>价的   
    window.a = 1;
    a //1;
    a = 2;
    window.a = 2;
>上面代码中，顶层对象的属性赋值与全局变量的赋值，是同一件事。

>顶层对象的属性与全局变量挂钩，被认为是JavaScript语言最大的设计败笔之一。
>这样的设计带了几个很大的问题，首先是没法在编译时就报错变量未声明的错误。
>只有运行时才能知道（因为全局变量可能是顶层对象的属性创造的，而属性的创造是动态的）；
>其次，程序员很容易不知不觉地就创建了全局变量（比如打字出错）；
>最后，顶层对象的属性是到处可读可写的，这非常不利于模块化编程。
>另一方法，window对象有实体含义，指的是浏览器的窗口对象，顶层对象是一个有实体含义的对象，也是不合格的。

>ES6为了改变着一点，一方面规定，为了保持兼容性，var命令和function命令声明的全局变量，依旧是顶层对象的属性；
>另外一方面规定，let命令、const命令、class命令声明的全局变量,不属于顶层对象的属性，也就是从ES6开始，全局变量逐步与顶层对象的属性脱钩。

    var a = 1;
    window.a //1;
    let b = 1;
    window.b// undefined
>上面代码中，全局变量a由var命令声明，所以它是顶层对象的属性，全局变量b由let命令声明，所以它不是顶层对象的属性，返回undefined.

### 5.globalThis对象

>JavaScript语言存在一个顶层对象，它提供全局环境（即全局作用域）,所有代码都是在这个环境中运行。
>但是，顶层对象在各种实现里面是不统一的。

* 浏览器里面，顶层对象是window，但Node和Web Worker没有window。
* 浏览器和Web Worker里面，self也指向顶层对象，但是Node没有self。
* Node里面，顶层对象是global，但是其他环境都不支持。

>同一段代码为了能够在各种环境，都能取得顶层对象，现在一般是使用this变量，但是有局限线。

* 全局环境中，this会返回顶层对象，但是，Node模块和ES6模块中，this返回的时当前模块。
* 函数里的this，如果函数不是作为对象的方法运行，而是单纯作为函数运行，this指向顶层对象，
但是严格模式下，这时this会返回undefined。
* 不管是严格模式，还是普通模式，new Function('return this')(),总是会返回全局对象，
但是如果浏览器用到了CSP（Content Security Policy，内容安全策略），那么eval,new Function这些方法都
可能无法使用。

>综上所述，很难找到一种方法，可以在所以情况下，都取得顶层对象。下面是两种勉强可以使用的方法。

    //方法一
     (typeof window !== 'undefined' ? window : 
     (typeof process == "object" && 
     typeof require == "function" &&
     typeof global === "object") ? global : this);
    //方法二
     var getGlobal = function (){
           if (typeof self !=="undefined") {
               return self;
           }
           if (typeof window !=="undefined") {
               return window;
           }
           if(typeof global !=="undefined"){
               return global;
           }
           throw new Error('unable to locate global object');
       }
> ES2020在语言的标准的层面，引入globalThis作为顶层对象，也就是说，任何环境下,
>globalThis都是存在的，都可以从它拿到顶层对象，指向全局环境下的this。

>垫片库global-this模拟了这个提案，可以在所有环境拿到globalThis。

## 二、变量的结构赋值
### 1.数组的解构赋值
#### 基本用法

>ES6允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被
>称为解构（Destructing)
以前，为变量赋值，只能直接指定值。

    let a = 1;
    let b = 2;
    let c = 3;
>ES6允许写成下面这样。

    let[a,b,c]=[1,2,3];
>上面代码表示，可以从数组中提取值，按照对应位置，对变量赋值。
>本质上，这种写法属于“模式匹配”，只要等号两边的模式相同，左边的变量
就会被赋予对应的值。下面是一些使用嵌套数组进行解构的例子。

    let[foo,[[bar],baz]]=[1,[[2],3]];
    let[x,,y]=[1,2,3];
    let[head,...tail]=[1,2,3,4];
>如果解构不成功，变量的值就等于undefined。
    
    let[foo] = [];
    let[bar,foo] = [1];
>以上两种情况都属于解构不成功，foo的值都会等于undefined。

>另外一种情况是不完全解构，即等号左边的模式，只匹配一部分的等号右边的数组。这种情况下，解构依然可以成功。

    let[x,y] = [1,2,3];
        //x = 1;
        //y = 2;
        let[a,[b],d] = [1,[2,3],4];
        //a = 1;
        //b = 2;
        //d = 4;
>上面两个例子都属于不完全解构。但是可以成功。

>如果等号的右边不是数组（或者严格地说，不是可遍历的结构）那么将会报错。

    // let [foo] = 1;
    // let [foo] = false;
    // let [foo] = NaN;
    // let[foo] = undefined;
    // let[foo] = null;
    // let [foo] = {};
>上面的语句都会报错，因为等号右边的值，要么转化为对象以后不具备Iterator接口，要么本身不具备Iterator接口（最后一个表达式）。
对于Set结构，也可以使用数组的结构赋值。

    let[x,y,z] = new Set(['a','b','c'])
>事实上，只要某种数据结构具有Iterator接口，都可以采用数组形式的结构赋值。

    function* fibs(){
        let a = 0;
        let b = 1;
        while (true) {
            yield a;
            [a,b] = [b,a+b];
        }
    }
    let [first, second, third, fourth, fifth, sixth] = fibs();
>上面代码中，fibs是一个Generator函数，原生具有Iterator接口，解构赋值会依次从这个接口获取值。

#### 默认值

>解构赋值允许指定默认值。

    let[foo = true] = [];
    let[x,y='b'] = ['a'];
    let[a,b='b'] = ['a',undefined];
>**注意，ES6内部使用严格相等运算符（===），判断一个位置是否有值，所以，只有当一个数组成员严格等于undefined,默认值才会生效。

     let[foo = 1] = [null];
>上面代码中，如果一个数组成员是null，默认值就不会生效，因为null不严格等于undefined。

>如果默认值是一个表达式，那么这个表达式是惰性求值的，即只有用到的时候，才会求值。

     function f(){
        console.log('aaa');
    }
    let[x=f()]=[1]
上面代码中，因为x能取到值，所以函数f根本不会执行，上面代码的代码等价于下面的代码

    let x;
    if([1][0] ===undefined){
        x = f();
    }else{
        x = [1][0]
    }
默认值可以引用解构赋值的其它变量，但改变量必须已经声明。
    // let[x=1,y=x]=[];x=1,y=1。
    // let[x=1,y=x]=[2];x=2,y=2。
    // let[x=1,y=x]=[1,2];x=1,y=2
    // let[x=y,y=1]=[];报错
上面最后一个表达式之所以会报错，是因为x用y做默认值时，y还没有声明。

### 2.对象的结构赋值

#### 简介
>解构不仅可以用于数组，还可以用于对象。

    let{foo,bar} = {foo:'aaa',bar:'bbb'};
>对象的解构与数组有一个重要的不同，数组的元素是按次序排列的，变量的取值由它的位置决定，而对象的属性没有次序，变量必须与属性同名，才能取到正确的值。

    let{foo,bar} = {foo:'aaa',bar:'bbb'};
    let{baz} = {foo: "aaa",bar:"bbb"};
>上面代码的第一个例子，等号左边的两个变量的次序，与等号右边两个同名属性的次序不一致，但是对取值完全没有影响。第二个例子的变量没有对应的同名属性，导致取不到值，最后等于undefined。

>如果解构失败，变量的值等于undefined。

>对象的解构赋值，可以很方便地将现有对象的方法，赋值到某个变量。

    const{log} = console;
    log('hello')
>上面代码将console.log赋值到log变量中

>如果变量名和属性不一致，必须写成下面这样。

    //let{foo:baz} = {foo: 'aaa',bar:'bbb'}
    //baz 'aaa'
    // let obj = {first: 'hello',last: "word"};
    // let {first:f,last: l} =obj;
    //f 'hello'
    //l 'world'
>这实际上说明，对象的结构赋值是下面形式的简写

    //let{foo:foo,bar:bar} = {foo: 'aaa',bar:'bbb'}
>也就是说，对象的解构赋值的内部机制，是先找到同名属性，然后再赋给对应的变量，真正被赋值的是后者，而不是前者。

    // let{foo:baz} = {foo: 'aaa',bar:'bbb'}
    // baz 'aaa'
    // foo error: foo is not defined
>上面代码中，foo是匹配的模式，baz才是变量，真正被赋值的变量baz，而不是模式foo

>与数组一样，解构也可以用于嵌套结构的对象

    // let obj = {
    //     p: [
    //         "hello",
    //         {y:"World"}
    //     ]
    // }
    // let{p:[x,{y}]}=obj;
    // x 'Hello'
    // y 'World'
> **注意：这时p是模式，不是变量，因此不会被赋值。如果p也要作为变量赋值，可以写成下面这样。**
     
     let obj = {
        p: [
            "hello",
            {y:"World"}
        ]
    }
    let{p,p:[x,{y}]}=obj;
> 下面是另一个例子。

     const node = {
        loc:{
            start:{
                line: 1,
                column: 5
            }
        }
    }
    let{loc,loc:{start},loc:{start:{line}}} = node;
    //line 1
    //loc Object {start:Object}
    //start Object {line:1,column:5}
>上面代码有三次解构赋值，分别是对loc,start,line三个属性的结构赋值。**注意，最后一次对line属性的解构赋值之中，只有line是变量，loc和start都是模式，不是变量。

>下面是嵌套赋值的例子

    // let obj = {};
    // let arr = [];
    // ({foo:obj.prop,bar:arr[0]}= {foo:123,bar:true});
    //打大括号原因，{}会被浏览器解析为{}
    //obj  {prop:123}
    //arr {true}
>如果解构模式是嵌套的对象，而且子对象所在的父属性不存在，那么将会报错。

    let{foo:{bar}} = {baz:'baz'};
    上面代码中，等号左边对象的foo属性，对应一个子对象，该子对象的bar属性，解构时会报错，原因很简单，因为foo这时等于undefined，再取子属性就会报错。
#### 默认值
>对象的解构也可以指定默认值。

    // let {x = 3} = {};
    //x 3
    // let {x,y = 5} = {x: 1};
    // x 1
    // y 5
    // let {x:y=3} = {};
    // y 3
    // let {x:y=3} ={x:5}
    // y = 5
    // let{message:msg = 'Somethiing went wrong'} = {};
    // msg  'Something went wrong'
>默认生效的条件是，对象的属性值严格等于undefined

#### 注意点
>(1)如果要将一个已经声明的变量用于解构赋值，必须非常小心。

    let x;
    {x} = {x:1};
>上面代码的写法会报错，因为javaScript引擎会将{x}理解成一个代码块，从而发生语法错误。只有不将大括号写在行首，避免javaScript将其解析为代码块，才能解决这个问题。

    let x;
    ({x} = {x:1});
>上面代码将整个解构赋值语句，放在一个圆括号里面，就可以正确执行。关于圆括号与解构赋值的关系。

>(2)解构赋值允许等号左边的模式之中，不放置任何变量名，因此，可以写出非常古怪的赋值表达式。

     ({}=[true,false]);
    ({}='abc');
    ({}=[]);
>上面的表达式虽然毫无意义，但是语法是合法的，可以执行。

（3）由于数组本质是特殊的对象，因此可以对数组进行对象属性的解构。

     let arr = [1,2,3];
    let {0:first,[arr.length-1]:last} = arr;

>上面代码对数组进行对象解构。数组arr的0键对应的值是1，[arr.length-1]就是2键，对应值是3，方括号这种写法属于“属性名表达式”

### 3.字符串的解构赋值

>字符串也可以解构赋值。这是因为此时，字符串被转换成了一个类似数组的对象。
    
    //const[a,b,c,d,e] = 'hello';
    //a "h"
    //b "e"
    //c "1"
    //d "1"
    //e "o"
>类似数组的对象都有一个length属性，因此还可以对这个属性进行解构赋值。

    // let {length:len} = "hello";
    // len 5
### 4.数值和布尔值的解构赋值

>解构赋值时，如果等号右边是数值和布尔值，则会先转为对象。

    let {toString: s} = 123;
    s === Number.prototype.toString;//true
    let {toString: s} = true;
    s === Boolean.prototype.toString;//true
>上面代码中，数值和布尔值的包装对象都有toString属性，因此变量s都能取到值。

>解构赋值的规则是，只要等号右边的值不是对象和数组，就先将其转换为对象。由于undefined和null无法转换为对象，所以对他们进行解构赋值，都会报错。

    // let {prop: x} = undefined;
    // let {prop: y} = null;
### 5.函数参数的解构赋值
>函数的参数也可以使用解构赋值。

      function add([x,y]){
            return x+y
        }
      add([1,2]);
>上述代码中，函数add的参数表面上是一个数组，但是传入参数的那一刻，数组参数就被解构变量x和y，对函数内部代码来说，他们能感受到的参数就是x和y。

>下面是另外一个例子。

    [[1,2],[3,4]].map(([a,b])=>a+b);

>函数参数的解构也可以使用默认值。

    function move({x=0,y=0}={}){
          return [x,y];
      }
      let b = move({x:3,y:8});
      console.log(b);
      let a = move({x:3});
      console.log(a);
      let c = move({});
      console.log(c);
      let d = move();
      console.log(d);

>上面代码中，函数move的参数是一个对象，通过对这个对象进行解构，得到变量x和y的值，如果解构失败，x和y等于默认值。

>注意，下面的写法会得到不一样的结果

     function move({x,y}={x:0,y:0}){
          return [x,y];
      }
      move({x:3,y:8})//[3,8]
      move({x:3})//[3,undefined]
      move({})//[undefined,undefined]
      move();
>上面代码是为函数move的参数指定默认值，而不是变量x和y指定默认值，所以会得到与前一种写法不同的结果。

>undefined就会触发函数参数的默认值。

[1,undefined,3].map((x='yes')=>x);

### 6.圆括号问题
>解构赋值虽然很方便，但是解析起来并不容易，对于编译器来说，一个式子到底是模式还是表达式，没有办法从一开始就知道，必须解析到（或解析不到）等号才知道。

>由此带来的问题是，如果模式中出现圆括号怎么处理。ES6的规则是，只要有可能导致解构的歧义，就不得使用圆括号。

>但是，这条规则实际上不容易辨别，处理起来相当麻烦。因此，建议只要有可能，就不要再模式中放置圆括号。

#### 不能使用圆括号的情况

>以下三种情解构赋值不得使用圆括号

1. 变量声明语句

    //全部报错
    // let[(a)]=[1];
    // let{x:(c)} = {};
    // let({x:c}) = {};
    // let{(x:c)}={};
    // let{(x):c} = {};
    // let{o:({p:P})}={o:{p:2}};
>上面6个语句都会报错，因为他们都是变量声明语句，模式不能使用圆括号。
2. 函数参数

>函数参数也属于变量声明，因此不能带圆括号。

    //全部报错
    //function f([(z)]){return z}
    //function f([z,(x)]){return x}
3. 赋值语句的模式

    //全部报错
    // （{p:a}）={p:42};
    // ([a])=[5]
>上面代码将整个模式放在圆括号之中，导致报错。

    [({p:a}),{x:c}]=[{},{}]
>上面代码将一部分模式放在圆括号之中，导致报错。

#### 可使用圆括号的情况

>可以使用圆括号的情况只有一种，赋值语句的非模式部分，可以使用圆括号

    // [(p)]=[{}]
    //({p:(d)})={})
    // [(parseInt.prop)]=[3];
>上面三行语句都可以正确执行，因为首先他们都是赋值语句，而不是声明语句；其次他们的圆括号都不属于模式的一部分。第一行语句中，模式是提取数组的第一个成员，跟圆括号无关；第二行语句中，模式是p，而不是d；第三行语句与第一句的性质一致。

### 7.用途

>变量的解构赋值用途很多

1. 交换变量的值

    let x = 1;
    let y = 2;
    [x,y] = [y,x];
>上面代码交换变量x和y的值，这样的写法不仅简洁，而且易读，语义非常清晰。
2. 从函数返回多个值

>函数只能返回一个值，如果要返回多个值，只能将他们放在数组或对象里返回。有了解构赋值，取出这些值非常方便。

    //返回一个数组
    // function example(){
    //     return [1,2,3]
    // }
    // let [a,b,c] = example();
    //返回一个对象
    // function example(){
    //     return {
    //         foo: 1,
    //         bar: 2
    //     }
    // }
    // let {foo,bar} = example();

3. 函数参数的定义

>解构赋值可以方便地将一组参数与变量名对应起来

    function f([x,y,z]){}   
    f([1,2,3]);
    function f({x,y,z}){}
    f({z:3,y:2,x:1});

4. 提取JSON数据

>解构赋值对提取Json对象中的数据，尤其有用

    let jsonData = {
        id: 42,
        status: "ok",
        data:[867,5309]
    }
    let{id,status,data:number} = jsonData;
    console.log(id,status,number);
>上面代码可以快速提取Json数据的值

5. 函数参数的默认值

    jQuery.ajax= function (url,{
        async = true,
        beforeSend = function(){},
        cake = true,
        complete = function(){},
        crossDomain = false,
        global = true,
    }={}){//...do stuff}
>指定参数的默认值，就避免了在函数体内部再 `var foo = config.foo || "default foo"`这样的语句。

6. 遍历Map结构

>任何部署了Iterator接口的对象，都可以for...of循环变量。Map结构原生支持Iterator接口，配合变量的解构赋值，获取键名和键值就非常方便。

    const map = new Map();
    map.set('first','hello');
    map.set('second','world');
    for(let[key,value] of map){
        console.log(key + "is" + value);
    }
>如果只想获取键名，或者只想获取键值，可以写成下面这样

    for(let [key] of map){
    }
    for(let [,value] of map){
    }

7. 输入模板的指定方法

>加载模块时，往往需要指定输入哪些方法，解构赋值使得输入语句非常清晰

    const {sourceMapConsumer, SourceNOde} = require('soure-map')


    


    














    





    
    

    

