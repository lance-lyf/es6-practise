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
    







    





    
    

    

