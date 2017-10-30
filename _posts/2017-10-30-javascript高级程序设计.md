---
layout: post
title: 'JavaScript高级程序设计随记'
subtitle: ''
date: 2017-10-30
categories: 知识
cover: 'http://oy6bua0oj.bkt.clouddn.com/46453-106.jpg'
tags: JavaScript
---
#js 高级

----------

当script标签通过src引入外部js文件，其标签内部的js代码将被忽略

----------
###异步脚本
HTML5为script元素定义了async属性，其目的是不让页面等待两个脚本下载和执行，从而异步加载页面其他内容，多个指定async属性的脚本文件并不保证按照先后顺序执行，确保两个脚本互不依赖

`<script type ="text/javascript" async src= "xxx.js"></script>`

----------
###XHTML用法

    <script type ="text/javascript">
    	function compare(a,b){
    		if(a < b) {
    			alert("A is less than B");
    		}else if (a > b){
    			alert("A is greater than B");
    		}else {
    			alert("A is equal to B");
    	}
    }
    </script>
xhtml是将html作为xml的应用而重新定义的一个标准，在xhtml中小于号（<）将被当作开始一个新标签解析，但是作为标签，小于号后面不允许跟空格，因此会导致语法错误
###方法一
用`&lt;`（<）和`&gt;`(>)替代
###方法二
用一个CData片段来包含js代码，在xhtml中，CData是文档中的一个特殊区域，这个区域包含不需要解析任意格式的文本内容，

    <script type ="text/javascript"><![CDATA[
    function compare(a,b){
    if(a < b) {
    alert("A is less than B");
    }else if (a b){
    alert("A is greater than B");
    }else {
    alert("A is equal to B");
    }
    }
    ]]></script>
在不兼容xhtml的浏览器中用javascript()注释将CDATA注释掉就可以
![](https://i.imgur.com/KNj7Eel.png)

----------
在不支持或关闭了javascript的浏览器中可以用noscript元素
在符合上述条件时浏览器会显示noscript中的内容，除此之外浏览器不会呈现noscript中的内容
>        <noscript>
>        <p>本页面需要浏览器支持（启用）javascript。</p>
>        </noscript>

----------
用var操作符定义的变量将成为定义该变量的作用域中的局部变量。也就是说如果在函数中使用var定义一个变量，那么这个变量将在函数退出后被销毁，如果省略var 将定义一个全局变量，这个变量在函数外部的任何地方都可以被访问，但是不建议在局部作用域中定义全局变量，那样将变得难以维护

----------
ECMAscript中由5种简单数据类型（也称为基本数据类型）
一种复杂数据类型object，typeOf可用于检测数据类型


Undefined --如果这个值未定义


Boolean -- 如果这个值时布尔值

Number -- 如果这个值是数值

string -- 如果这个值是字符串

object -- 如果这个值是对象或null

function -- 如果这个值是函数

----------
NaN（Not a Number）是一个特殊的数值，在ECMA中任何数值除以非数值会返回NaN，任何涉及NaN的操作都会返回NaN。其次，NaN与任何值都不相等，包括NaN本身
ECMAscript定义了isNaN函数这个函数可以检测括号内是否“不是数值”
alert(isNaN(NaN))  //true

alert(isNaN(10))  //false

alert(isNaN("10")) //false

alert(isNaN("blue")) //true
###数值转换
parseInt（）会忽略字符串前面的空格，直到找到第一个非空格字符

如果第一个字符不是数字或负号会返回NaN，如果是数字字符，会继续解析直到解析了所有字符或者遇到非数字字符，浮点数将被忽略小数点后面的数字 0x开头将被解析为16进制 0开头将被解析为8进制（但大多数解析引擎中前导0将被视为无效）
可以自行制定数字进制，以保证正确解析

var num = parseInt("AF",16); //将被当作16进制解析


var num = parseInt（"10",8）; //将按照8进制解析

如果是布尔值true和false将被分别转换为1和0

如果是null，将返回0

如果是undefined，将返回NaN

如果字符串为空，将返回0

parseFloat 可以识别所有浮点数，并原值输出

toString方法将把一个值转换为字符串

alert（num.toString(//括号内可设置转化进制数)） 

不设置默认转换10进制

String方法效果同样
var value1 = 10;

var value2 = true;

var value3 = null;

var value4;

alert(String(value1));  //10

alert(String(value2));  //true

alert(String(value3));  //null

alert(String(value4));  //undefined

----------
###按位非（NOT）
~

由一个波浪线~表示，返回数值的反码减1即

    var nu = 25；
    var num = ~nu；
    alert(num);   //-26
###按位与（AND）
&

会将两个比较数字的二进制码对齐对比如果对应为都是1返回1，任何一位是0都将返回0

    25 = 0000 0000 0000 0000 0000 0000 0001 1001
    3  = 0000 0000 0000 0000 0000 0000 0000 0011
    AND =0000 0000 0000 0000 0000 0000 0000 0001
var res = 25 & 3;
alert(res); //1
###按位或（OR）
|

只要有一个位是1的情况就返回1

    25 = 0000 0000 0000 0000 0000 0000 0001 1001
    3  = 0000 0000 0000 0000 0000 0000 0000 0011
    AND =0000 0000 0000 0000 0000 0000 0001 1011
二进制码11011等于十进制27
###按位异或（XOR）
^

对应为只有一个1返回1，对应为相同则返回0

    25 = 0000 0000 0000 0000 0000 0000 0001 1001
    3  = 0000 0000 0000 0000 0000 0000 0000 0011
    AND =0000 0000 0000 0000 0000 0000 0001 1010
###左移操作符（<<）
会将数值二进制的所有位向左移指定位数，左移产生的空位用0补充

    var oldvalue = 2;   //10
    var newvalue = oldvalue <<5 ;//1000000
左移操作不影响数值的符号位
###右移操作符（>>）同理

逻辑操作符

- 或 ||
- 与 &&
- 非 ！

全等和不全等（=== && ！==）

    var res1 = ("55" == 55) // true 转换后相等
    var res2 = （“55” == 55） // false 不同数据类型相等

不全等操作符则返回相反结果

###条件操作符（？）
varse = boolean ? true-value : false-value 
分别在值为true与false时返回前后的值
###赋值操作符（=）
####do-while语句会在循环体的代码全部执行完毕后，才会测试出口条件，代码最少执行一次
####while语句属于前测试循环语句 在循环体的代码执行之前，就会对出口条件求值，有可能代码永不执行
####for循环只是把与循环有关的代码集中到了一个位置
    var num = 10;
    for(var i = 0 ;i<num; i++){
    alert(i);
    }


    var i = 0;
    var num = 10;
    while(i<num){
    alert(i);
    i++;
    }

----------

**alert()** 弹出个提示框 （确定） 

**confirm()** 弹出个确认框 （确定，取消） 

**prompt()** 弹出个输入框

----------
###break语句和continue语句
### break，立即跳出循环，执行循环后的语句 ###
### continue ，立即跳出本次循环，并继续下一次循环 ###

----------

### with语句 ###

with语句的作用是将代码的作用于设置到一个特定的对象中。

例：

    var qs = location.search.substring(1);
    var hostName = location.hostname;
    var url = location.href;
    

----------

    with(location){
    	var qs = serarch.substring(1);
    	var hostName = hostname;
    	var url = href;
    }

----------
### switch语句 ###

    switch (expression) {
     case value: statement break;
     case value: statement break;
     case value: statement break;
     case value: statement break;
     default: statement
    }
当表达式的值等于value 则执行value后的语句 并跳出循环
可以不跳出循环，用以合并多种情况，但要特别添加注释

switch语句也可以用于字符串比较

     switch ("hello world"){
    	case "hello" + "world": alert("Greeting was found");
    	break;
    	case "goodbye" : alert("closing was found");
    	break;
    	default : alert("Unexepected message was found");
    }
switch布尔值操作

    var num = 25;
    switch (true){
    	case num < 0;
    	alert("less than 0");
    	break;
    	case num >= 0 && num <= 10;
    	alert("between 0 and 10");
    	break;
    	default : alert("more than 10");
    }

----------
arguments
可以通过length属性查看传递进来多少参数
 
    fuction howmangargs(){
    	alert(arguments.length);
    }
    howmangargs("string",45); //2
    howmangargs(); 		  //0
    howmangargs(12);		  //1

----------
### 管理内存 ###
javascript语言并不需要担心操作内存的问题，但是为了防止javascript运行所占用的系统内存耗尽而导致的系统崩溃，可以手动解除引用变量（null）

    function creatperson(name){
    	var localperson = new object();
    	localperson.name = name;
    	return localperson;
    }
    var globalperson = creatperson ("nicholas");
    globalperson = null；
javascript有自己的垃圾清理系统，上面的操作并不能直接释放内存
，而是让值脱离执行环境，以便垃圾收集器在下次运行时将其回收

     javascript高程 第四章

----------
## object类型 ##
创建object实例的方式

一：

new操作符加object构造函数

    var person = new object();
    person.name = "Nicholas";
    person.age = 29;

二：

对象字面量表示法

    var person = {
    	name: "Nicholas",
    	age: 29
    
    };

访问对象属性可以通过两种方式实现

    alert(person["name"]);
    alert(person.name);
点表示法		方括号表示法

方括号表示法可以通过变量来访问属性，当属性名包含关键字或保留字
或会导致语法错误的字符（空格也会导致语法错误），可以通过方括号表示法访问属性

    var pre = "name";
    alert(person[pre]);

----------

    
    person["first name"] = "Nicholas" ;
    

----------
## Array类型 ##
创建数组的基本方式：

    var colors = new Array(); //new操作符可以省略
    
    var colors = new Array(20); // 创建一个包含20项的数组
    
    var colors = new Array("Greg"); //创建一个包含一项，且字符串为“Greg”的数组

----------
    var colors = ["red","blue","green"];  //创建一个包含三个字符串的数组
    var names = []; //创建一个空数组
    var names = [1,2,]   //错误写法，创建一个在ie8之前包含三个字符串的数组，最后一个为undefined ，在其他浏览器中会创建一个包含2歌字符串的数组 
    
读取操作可以通过数组的下标读取，也可以用数组下标写入字符串

    var colors = ["red","blue","green"];
    alert(colors[0]);   //显示第一项
    colors[2] = "black";   //修改第三项
    colors[3] = "brown";   //新增第四项
数组的length属性可写可读

    var colors = ["red","blue","green"];
    colors.length = 2;  //删除第三项
    alert(colors[2]);  //undefined
    
----------

    var colors = ["red","blue"];
    colors.length = 99;  
    alert(colors.length); //100 从第三项起后面为undefined

----------
ECMAscript提供了一种让数组的行为类似于其他数据结构的方法

栈（后进先出）
    
    var colors = new Array();   //创建一个新数组
    var count = colors.push("red","green"); // 向数组中推入两个参数
    alert(count);//2
    
    count = colors.push("black");  //推入另一项 
    alert(count);   //3
    
    var item = cikirs.pop();  //获取栈顶元素
    alert(item); //"black"
    alert(colors.length)  //2

队列（先进先出）

    var colors = new Array();  //创建一个数组
    var count = colors.push("red","green"); //推入两项
    alert(count); //2
    
    count = colors.push("black"); // 推入另一项
    alert(count);  //3
    
    var item = colors.shift(); //推出队列第一项
    alert(item);  //"red"
    alert(colors.length);   //2

----------
### 数组操作方法 ###

### concat() ###
这个方法会创建当前数组的一个副本，然后将接收到的参数添加到这个副本的末尾，最后返回新构建的数组
    
    var colors = ["red","green"];
    var colors2 = colors.concat("yellow",["black","brown"]);
    
    alert(colors); // red, green 
    alert(colors2); // red,green,yellow,black,brown
### slice() ###
接收一个或两个参数，即要返回项的起始和结束位置
他会返回起始位置到结束位置的参数的数组，但不包括结束位置
在只有一个参数的情况下，他会返回从设定起始位置至结尾位置的数组


    var colors= ["red","blue","green","yellow"];
    var colors2 = colors.slice(1);
    var colors3 = colors.slice(1,3);
    
    alert(colors2); // blue,green,yellow
    alert(colors3); //blue,green
### splice() ###
删除:  可以删除任意数量的项，需要指定两个参数，要删除的第一项的位置和要删除的项数

    var colors = ["red","green","blue"]; 
    var removed = colors.splice(0,1); //删除第一项
    alert(colors); //green blue
    alert(removed); //red 

插入：可以向指定位置插入任意数量的项，需要提供三个参数：起始位置，0（要删除的项数），和要插入的项

    var colors= ["red","green","blue"];
    var removed = colors.splice(1,0,"yellow","orange"); //从位置一开始插入两项
    alert(colors); //red,green,yellow,orange,blue
    alert(removed); //空

替换： 可以向指定位置插入任意数量的项，且同时删除任意数量的项
起始位置，要删除的项数和要插入的任意数量的项，插入的项数不必与删除的项数相等

    var colors= ["red","green","blue"];
    var removed = colors.splice(1,1,"red","purple");
    alert(colors); //red red purple
    alert(removed); //green

----------
### 位置方法 ###
indexOf()和lastindexOf()

需要提供两个参数 要查找的项的值和表示要查找起点位置的索引（可选）
其中，indexOf从数组的开头向后查找，lastindexOf从数组的末尾向前查找

    var numbers = [1,2,3,4,5,6,7,8,9];
    alert(numbers.indexOf(4));   //3

----------
### 迭代方法 ###

 五个迭代方法 都接受两个参数：要在每一项上运行的函数 和 运行该函数的作用域（可选）

every():对数组中的每一项运行给定函数。如果函数对每一项都返回true，则返回true。

filter():对数组中的每一项运行给定函数。返回该函数会返回true的项组成的数组。

forEach():对数组中每一项运行给定函数。该函数没有返回值。

map():对数组中每一项运行给定函数。返回每次函数调用的结果组成的函数。

some():对数组中每一项运行给定函数。如果函数对 任一项返回true，则返回true。
 
 
        var numbers = [1, 2, 3, 4, 5, 4, 3, 2, 1];
        //every()和some()最相似
        //every()  item:当前遍历项，index:当前项索引，array:数组对象本身
        var everyResult = numbers.every(function (item, index, array) {
            return item > 2;
        });
        alert(everyResult);//false
 
 
        //some()
        var someResult = numbers.some(function (item, index, array) {
            return item > 2;
        });
        alert(someResult);//true
 
 
        //filter
        var filterResult = numbers.filter(function (item, index, array) {
            return item > 2;
        });
        alert(filterResult);//[3,4,5,4,3]
 
        //map()
        var mapResult = numbers.map(function (item, index, array) {
            return (item * 2);
        });
        alert(mapResult);//[2,4,6,8,10,8,6,4,2]
 
        //forEach 本质上和for循环没有区别
        var forEachResult=numbers.forEach(function(item,index,array){
            alert(item)
        });

----------
### 归并方法 ###
reduce(),reduceRight().这两个方法都会迭代数组的所有项，然后构建一个最终返回的值，其中reduce是从数组的第一项开始遍历，reduceRight相反

他们接收四个参数：前一个值，当前值，项的索引，数组对象

    var values = [1,2,3,4,5];
    var sum = values.reduce(function(prev,cur,index,array){
    return prev + cur;
    });//1+2---3+3---6+4---10+5   
    alert(sum); //15


----------
### Date类型 ###
var now = new Date(); //创建一个日期对象，自动获取当前时间

Date.parse()会接收传入的字符串，如果字符串不表示日期，则返回NaN

    var someDate  = new Date(Date.parse("May 25,2004"));//月，日，年
    
    var someDate  = new Date("May 25,2004"); //Date函数会在后台自动调用parse函数，所以与上面的例子等价

Date.UTC()也会返回日期的毫秒数，但他与Date.parse不同的是，他的参数分别为，年，月，日，时，分，秒 ，只有前两个参数是必需的，如果只提供了前两个参数，则后面的参数全部为零（月，日以0为第一天，也就是返回1月1日）

    var y2k = new Date(Date.UTC(2000,0));//2000年1月1日0点
    var all = new Date(Date.UTC(2000,4,5,17,55,55));//2000年4月5日17点55分55秒

同样的Date.UTC也可以省略

Date.now()可以获取当前时间

    //取得开始时间
    var start = Date.now();
    
    //执行函数
    
    //取得停止时间
    
    var stop = Date.now(),
    result = stop- start;//返回差值的毫秒数

----------
###日期/时间组件方法###
getDate()	从 Date 对象返回一个月中的某一天 (1 ~ 31)

getDay()	从 Date 对象返回一周中的某一天 (0 ~ 6)

getFullYear()	从 Date 对象以四位数字返回年份

getHours()	返回 Date 对象的小时 (0 ~ 23)

getMilliseconds()	返回 Date 对象的毫秒(0 ~ 999)

getMinutes()	返回 Date 对象的分钟 (0 ~ 59)

getMonth()	从 Date 对象返回月份 (0 ~ 11)

getSeconds()	返回 Date 对象的秒数 (0 ~ 59)

getTime()	返回 1970 年 1 月 1 日至今的毫秒数

getTimezoneOffset()	返回本地时间与格林威治标准时间 (GMT) 的分钟差

getUTCDate()	根据世界时从 Date 对象返回月中的一天 (1 ~ 31)

getUTCDay()	根据世界时从 Date 对象返回周中的一天 (0 ~ 6)

getUTCFullYear()	根据世界时从 Date 对象返回四位数的年份

getUTCHours()	根据世界时返回 Date 对象的小时 (0 ~ 23)

getUTCMilliseconds()	根据世界时返回 Date 对象的毫秒(0 ~ 999)

getUTCMinutes()	根据世界时返回 Date 对象的分钟 (0 ~ 59)

getUTCMonth()	根据世界时从 Date 对象返回月份 (0 ~ 11)

getUTCSeconds()	根据世界时返回 Date 对象的秒钟 (0 ~ 59)

setDate()	设置 Date 对象中月的某一天 (1 ~ 31)

setFullYear()	设置 Date 对象中的年份（四位数字）

setHours()	设置 Date 对象中的小时 (0 ~ 23)

setMilliseconds()	设置 Date 对象中的毫秒 (0 ~ 999)

setMinutes()	设置 Date 对象中的分钟 (0 ~ 59)

setMonth()	设置 Date 对象中月份 (0 ~ 11)

setSeconds()	设置 Date 对象中的秒钟 (0 ~ 59)

setTime()	setTime() 方法以毫秒设置 Date 对象

setUTCDate()	根据世界时设置 Date 对象中月份的一天 (1 ~ 31)

setUTCFullYear()	根据世界时设置 Date 对象中的年份（四位数字）

setUTCHours()	根据世界时设置 Date 对象中的小时 (0 ~ 23)

setUTCMilliseconds()	根据世界时设置 Date 对象中的毫秒 (0 ~ 999)

setUTCMinutes()	根据世界时设置 Date 对象中的分钟 (0 ~ 59)

setUTCMonth()	根据世界时设置 Date 对象中的月份 (0 ~ 11)

setUTCSeconds()	setUTCSeconds() 方法用于根据世界时 (UTC) 设置指定时间的秒字段

toDateString()	把 Date 对象的日期部分转换为字符串

toLocaleDateString()	根据本地时间格式，把 Date 对象的日期部分转换为字符串

toLocaleTimeString()	根据本地时间格式，把 Date 对象的时间部分转换为字符串

toLocaleString()	据本地时间格式，把 Date 对象转换为字符串

toString()	把 Date 对象转换为字符串

toTimeString()	把 Date 对象的时间部分转换为字符串

toUTCString()	根据世界时，把 Date 对象转换为字符串

UTC()	根据世界时返回 1970 年 1 月 1 日 到指定日期的毫秒数

valueOf()	返回 Date 对象的原始值

----------
### RegExp类型 ###
正则表达式中的元字符

#### ( ) { } [ ] | \ ^ $ ? * + . ####

g 表示全局模式，即模式将被应用于所有字符串，而非在发现第一个匹配项时立即停止

i 表示不区分大小写模式，即在确定匹配项时忽略模式与字符串的大小写

m 表示多行模式，即在到达一行文本末尾时还会继续查找下一行是否存在与模式匹配的项

`var pattern = /[bc]at/i;`    //匹配第一个bat或cat，不区分大小写

`var pattern2 = /\[bc\]at/i;` //匹配第一个[bc]at，不区分大小写

`var pattern3 = /.at/gi;`    //匹配所有以at结尾的三个字符的组合，不区分大小写

`var pattern4 = /\.at/gi;`   //匹配所有“.at”，不区分大小写

用RegExp 构造函数

它接收两个参数，一个是要匹配的字符串模式，另一个是可选的标志字符串

    var pattern = new RegExp{"[bc]at","i"};

----------

    var re = null,
    			i;
    for (i=0; i<10;i++){
    	re = /cat/g;
    	re.test("Catastrophe");
    }
    for (i=0; i<10;i++){
    	re = new RegExp("cat","g");
    	re.test("Catastrophe");
    }
在第一个循环中，实际上只为/cat/创建了一个RegExp实例，实例属性不会重置，所以第一次调用test()找到了“cat”，第二次调用是从索引为3的字符开始的，所以第二次就无法寻找；

在第二个循环中实用RegExp构造函数在每次循环中创建正则表达式。因此每次迭代都会创建一个新的RegExp实例，所以每次调用test()都会返回true；

----------
RegExp的每个实例都具有以下属性，使用这些属性可以取得有关模式的各种信息

global： 布尔值，表示是否设置了g标志

ignoreCase：布尔值，表示是否设置了i标志

lastIndex：整数，表示开始搜索下一个匹配项的字符位置，从0算起

multiline：布尔值，表示是否设置了m标志

source：正则表达式的字符串表示，按照字面量形式而非传入构造函数中的字符串模式返回

var pattern = /\[bc\]at/i;

alert(pattern.global);  //false
alert(pattern.ignoreCase); //true
alert(pattern.multiline); //false
alert(pattern.lastIndex);  //0
alert(pattern.source);  //"\[bc\]at"

----------
### RegExp实例方法 ###
exec()方法是专门为捕获组设计的，exec()接受一个参数，既要应用模式的字符串，然后返回包含第一个匹配项信息的数组；或者在没有匹配项的情况下返回null；
返回的数组虽然是Array的实例，但包含两个额外的属性，index（匹配项在字符串中的位置）和input（应用正则表达式的字符串）

对于exec()方法而言，即使在模式中设置了全局标志（g），他每次也只会返回一个匹配项，在不设置全局标志的情况下，在同一个字符串上多次调用exec()将始终返回第一个匹配项的信息，而在设置了全局标志的情况下，每次调用exec()则都会在字符串中继续查找新匹配项

    var text = "cat,bat,sat,fat";
    var pattern = /.at/;
    
    var matches = pattern.exec(text);
    alert(matches.index);   //0
    alert(matches[0]);//cat
    alert(pattern.lastIndex);   //0
    
    matches = pattern.exec(text);   
    alert(matches.index);   //0
    alert(matches[0]);//cat
    alert(pattern.lastIndex);   //0

----------
    var pattern2 = /.at/g;
    
    var matches = pattern2.exec(text);
    alert(matches.index);   //0
    alert(matches[0]);//cat
    alert(pattern2.lastIndex);   //3
    
    matches = pattern2.exec(text);
    alert(matches.index);   //5
    alert(matches[0]);//bat
    alert(pattern2.lastIndex);   //8

----------
test()方法接受一个字符串参数，在模式与该参数匹配的情况下返回true，否则，返回false
    
    var text = "000-00-0000";
    var pattern = /\d{3}-\d{2}-\{4}/;
    
    if(pattern.test(text)){
    	alert("The pattern was matched");
    }
# p107 #