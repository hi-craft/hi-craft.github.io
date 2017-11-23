<button type="button">open</button>---
layout: post
title: 'JavaScript高级程序设计随记'
subtitle: ''
date: 2017-10-30
categories: 笔记
cover: 'http://oy6bua0oj.bkt.clouddn.com/46453-106.jpg'
tags: JavaScript
---
# js 高级 #

----------

当script标签通过src引入外部js文件，其标签内部的js代码将被忽略

----------
### 异步脚本 ###
HTML5为script元素定义了async属性，其目的是不让页面等待两个脚本下载和执行，从而异步加载页面其他内容，多个指定async属性的脚本文件并不保证按照先后顺序执行，确保两个脚本互不依赖

`<script type ="text/javascript" async src= "xxx.js"></script>`

----------
### XHTML用法 ###

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
### 方法一 ###
用`&lt;`（<）和`&gt;`(>)替代
### 方法二 ###
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
### 数值转换 ###
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
### 按位非（NOT） ###
~

由一个波浪线~表示，返回数值的反码减1即

    var nu = 25；
    var num = ~nu；
    alert(num);   //-26
### 按位与（AND） ###
&

会将两个比较数字的二进制码对齐对比如果对应为都是1返回1，任何一位是0都将返回0

    25 = 0000 0000 0000 0000 0000 0000 0001 1001
    3  = 0000 0000 0000 0000 0000 0000 0000 0011
    AND =0000 0000 0000 0000 0000 0000 0000 0001
var res = 25 & 3;
alert(res); //1
### 按位或（OR） ###
|

只要有一个位是1的情况就返回1

    25 = 0000 0000 0000 0000 0000 0000 0001 1001
    3  = 0000 0000 0000 0000 0000 0000 0000 0011
    AND =0000 0000 0000 0000 0000 0000 0001 1011
二进制码11011等于十进制27
### 按位异或（XOR） ###
^

对应为只有一个1返回1，对应为相同则返回0

    25 = 0000 0000 0000 0000 0000 0000 0001 1001
    3  = 0000 0000 0000 0000 0000 0000 0000 0011
    AND =0000 0000 0000 0000 0000 0000 0001 1010
### 左移操作符（<<） ###
会将数值二进制的所有位向左移指定位数，左移产生的空位用0补充

    var oldvalue = 2;   //10
    var newvalue = oldvalue <<5 ;//1000000
左移操作不影响数值的符号位
### 右移操作符（>>）同理 ###

逻辑操作符

- 或 ||
- 与 &&
- 非 ！

全等和不全等（=== && ！==）

    var res1 = ("55" == 55) // true 转换后相等
    var res2 = （“55” == 55） // false 不同数据类型相等

不全等操作符则返回相反结果

### 条件操作符（？） ###
varse = boolean ? true-value : false-value 
分别在值为true与false时返回前后的值
### 赋值操作符（=） ###
do-while语句会在循环体的代码全部执行完毕后，才会测试出口条件，代码最少执行一次

while语句属于前测试循环语句 在循环体的代码执行之前，就会对出口条件求值，有可能代码永不执行

for循环只是把与循环有关的代码集中到了一个位置

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
###break语句和continue语句###
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


RegExp构造函数的属性

长属性名 短属性名
  
    input   	 $_ 最近一次要匹配的字符串，opera未实现
    
    lastMatch    $& 最近一次的匹配项。opera未实现
    
    lastParen    $+ 最近一次匹配的捕获组。opera未实现
    
    leftContext  $` input字符串中lastMatch之前的文本
    
    multiline    $* 布尔值，表示是否所有表达式都使用多行模式
    
    rightContext $' input字符串中lastMatch之后的文本

----------

    var text = "this has been a short summer";
    var pattern = /(.)hort/g;
    if(pattern.test(text)){
        console.log(RegExp.input);  //this has been a short summer
        console.log(RegExp.leftContext);  //this has been a
        console.log(RegExp.rightContext);  //summer
        console.log(RegExp.lastMatch);     //short
        console.log(RegExp.lastParen);    //s
        console.log(RegExp.multiline);    //false
    }

匹配任何一个字符后跟hort，且把第一个字符放在了一个捕获组中

对应的短属性名

    alert(RegExp["$`"]);

9个用于存储捕获组的构造函数属性，分别用于存储第一，第二。。第九个匹配的捕获组

    var text = "this has been a short sumer";
    var pattern = /(..)or(.)/g;
    if(pattern.test(text)){
    alert(RegExp.$1);   //sh
    alert(RegExp.$2);   //t
    }


----------
### Function ###

声明函数的两种方法

//函数声明

    function sum(num1,num2){
    	return num1+num2;
    }

//函数表达式

    var sum = function(num1,num2){
    return num1+num2;
    } ;
函数名是指针

声明两个同名函数，后者会覆盖前者

解析器在执行环境加载数据时，会率先读取函数声明，并使其在执行任何代码之前可用

arguments.callee属性是一个指针，指向拥有这个arguments对象的函数

    function factory(num){
    if(num <= 1){
    return 1;
    }else{
    return num*factory(num-1);
    }
    }

当var truefactory = factory;时原函数将无法调用

可以通过callee属性来取消函数名的耦合状态

    function factory(num){
    if(num <= 1){
    return 1;
    }else{
    return num*arguments.callee(num-1);
    }
    }

当在网页的全局作用域中调用函数时，this对象引用的就是window

length属性表示函数希望接收的命名参数的个数

    function sayname(){
    	alsert("s");
    }
    
    alert(sayname.length);   //0


----------
### 基本包装类型概述 ###
 实际上,每当读取一个基本类型值的时候,后台就会创建一个对应的基本包装类型的对象,从而能够调用一些方法来操作这些数据

    var box = 'Mr.Lee';  // 定义一个String字符串;  
    var box2 = box.substring(2);　// 截掉字符串前两位;
    console.log(box2);  //.Lee;
    // 变量box是一个字符串String类型,而box.substring(2)又说明它是一个对象(只有对象才会调用方法);
    console.log('Mr.Lee'.substring(3));  // 直接通过字符串值来调用方法=>Lee;

引用类型和基本包装类型的主要区别就是对象的生存期;
自动创建的基本包装类型的对象,则只存在于一行代码的执行瞬间,然后立即被销毁;

字面量写法

    var box = 'Mr.Lee'; // 字面量;
    box.name = 'Lee';  // 无效属性;
    box.age = function(){// 无效方法;
      return 100;
    };
    console.log(box.substring(3));// =>Lee;
    console.log(typeof box);   // =>string;
    console.log(box.name);// =>undefined;
    console.lgo(box.age());   // =>错误;这意味着我们不能在运行时为基本类型值添加属性和方法;

new运算符写法

    var box = new String('Mr.Lee');
    box.name = 'Lee';
    box.age = function(){
      return 100;
    };
    console.log(box.substring(3));// =>Lee;
    console.log(typeof box);  　// =>object;
    console.log(box.name);// =>Lee;
    console.lgo(box.age());// =>100;

### Number类型 ###
Number对象的方法

 toString()           将数值转化为字符串,并且可以转换进制;

 toLocaleString()     根据本地数字格式转换字符串;

 toFixed()            将数字保留小数点后指定位数并转化为字
符串;

 toExponential()      将数字以指数形式表示;

 toPrecision()        指数形式或点形式表示数字;指定以几位数表示
    
    var numberobject = new Number(10);
    var numbervalue = 10;
    alert(typeOf numberpbject);   //object
    alert(typeOf numbervalue);//number

number对象是number的实例，而基本类型的数值不是

### string类型 ###
字符方法

charAt()以单字符字符串的形式返回给定位置的那个字符

charCodeAt()返回字符编码

    var stringvalue = "hello world";
    alert(stringvalue.charAt(1));  //e
    
    alert(stringvalue.charCodeAt(1));  //101 

字符串操作方法

concat() 用于将一个或多个字符串拼接起来；返回新的字符串
实际操作中更多用+操作符，比较简单易行

    var stringvalue = "hello";
    var result = stringvalue.concat("world");
    
    alert(result);   //"hello world"
    alert(stringvalue);  //world

基于字符串创建新字符串的方法
slice（）；

substr（）；  第二个参数指定返回的字符个数

substring（）；

他们都接收两个参数，即开始位置和结束位置（不包括结束位置），如果未指定第二个参数，则默认到字符串结尾（substr除外）

    var stringvalue = "hello world";
    alert(stringvalue.slice(3));   //lo world
    alert(stringvalue.substring(3)); //lo world
    alert(stringvalue.substr(3));  //lo world
    alert(stringvalue.slice(3,7));  //lo w
    alert(stringvalue.substring(3,7)); //lo w
    alert(stringvalue.substr(3,7));  //lo worl

当指定的参数为负值，slice会将传入的负值与字符串的长度相加。substr方法会将负的第一个参数加上字符串的长度，将第二个参数设为0，substring会将所有负值参数转换为0

    var stringvalue = "hello world";
    alert(stringvalue.slice(-3));  //rld
    alert(stringvalue.substring(-3));  //hello world
    alert(stringvalue.substr(-3));  //rld
    alert(stringvalue.slice(3,-4));  //lo w
    alert(stringvalue.substring(3,-4));  //hel
    alert(stringvalue.substr(3,-4));  //空

字符串位置方法

indexOf  从头查找指定字符串，并返回第一次发现的位置
lastIndexOf 相反

他们都可以接收第二个可选参数，即从哪里开始查找
lastIndexOf 会从指定位置向前搜索

    var stringvalue = "sad  sadasd sdaserqqwe qw";
    var positions = new Array();
    var pos = stringvalue.indexOf("e");
    
    while(pos>-1){
    positions.push(pos);
    pos = stringvalue.indexOf("e",pos+1);
    }
    alert(positions);

trim()方法会创建一个字符串的副本，并删除前置及后缀的所有空格，返回结果

toLowerCase()方法会返回字符串的小写

toUpperCase()方法会返回字符串的大写

字符串的模式匹配方法

match()方法本质上与调用RegExp的exec方法相同，match()方法只接收一个参数，要么是一个正则表达式，要么是一个RegExp对象

    var text = "cat,bat,sat";
    var pattern = /.at/;

    var matches = text.match(pattern);
    alert(matches.index);   //0
    alert(matches[0]);  //cat
    alert(pattern.lastIndex); //0

search()方法会返回第一个匹配项的索引         //一千行合影

    var text = "cat,bat,sat";
    var pos= text.search(/.at/);
    alert(pos);  //1

replace()替换方法，它接收两个参数，第一个是一个RegExp对象或一个字符串。第二个参数可以是一个字符串或者一个函数，要想替换所有字符串，唯一的方法就是提供一个正则表达式，而且要指定全局标志（g），

    var text = "cat,sat,bat";
    var result = text.replace("at","ond");
    alert(result);  //"cond,sat,bat"
    
    result = text.replace(/at/g,"ond");
    alert(result);  //"cond sond band"
    
split()方法可以基于指定的分隔符将一个字符串分割成多个字符串，并将结果放在一个数组中，他也可以接收第二个参数，指定数组的大小，确保返回的数组不会超过既定大小

eval()方法会将传入的参数当作实际的javascript语句来解析，然后将执行结果插入到原位置

math对象

min()确定一组数值中的最小值

max()确定一组数值中的最大值

ceil()执行向上舍入

floor()执行向下舍入

round()执行标准舍入

random()随机返回大于等于0小于1的一个随机数

值 = Math.floor(Math.random()*可能值的总数+第一个可能的值)

    var num = Math.floor(Math.random()*10+1);

返回1到10的随机整数

JavaScript中定义了两种不同的属性

数据属性和访问器属性

数据属性一般用于存储数据数值，而访问器属性一般进行get/set操作，不能直接存储数据数值

在ES5中，我们为了描述属性(property)的各种特征，定义了特性(attribute)。在JavaScript中不能直接访问特性，我们把它放在两对方括号中，例如[[Enumerable]]

•数据属性

数据属性主要有四个特性描述其行为

1.[[Configurable]]：默认为true。表示能否通过delete删除属性从而重新定义属性，能否修改属性特性，或者能否把属性修改为访问器属性

2.[[Enumerable]]：默认为true。表示能否通过for-in循环返回属性

3.[[Writable]]：默认为true。表示能否修改属性的值

4.[[Value]]：默认值为undefined。表示包含属性的数据值。读写属性值都从这个位置进行

如果想要修改属性默认的特性，可以使用ES5提供的Object.defineProperty()方法，这个方法接收三个参数：属性所在对象、属性的名字和一个描述符对象。描述符对象只能包含上述四个特性的一个或多个

    var person = {};
    Object.defineProperty(person,"name",{
    	writable:false,
    	value:"Nicholas"
    });
    alert(person.name); //"Nicholas"
    person.name = "Greg"; 
    alert(person.name);  //"Nicholas"

当调用Object.defineProperty()把除writable之外的特性修改回true，就会报错

    var person = { 
      name: "Scott"
    } 
    Object.defineProperty(person,"name",{ 
      configurable:false; 
    }) 
     
    Object.defineProperty(person,"name",{ 
      configurable:true;  //此处会抛出错误 
    }) 

•访问器属性

访问器属性不包含数据值。它包含一对getter和setter函数。当读取访问器属性时，会调用getter函数并返回有效值；当写入访问器属性时，会调用setter函数并传入新值，setter函数负责处理数据

该属性有四个特性：

1.[[Configurable]]：默认为true。表示能否通过delete删除属性从而重新定义属性，能否修改属性特性，或者能否把属性修改为访问器属性

2.[[Enumerable]]：默认为true。表示能否通过for-in循环返回属性

3.[[Get]]：读取属性时调用的函数，默认为undefined

4.[[Set]]：写入属性时调用的函数，默认为undefined

访问器属性不能直接定义，必须通过Object.defineProperty()函数定义

    var book = {
    _year:2004,
    edition:1
    };
    Object.defineProperty(book,"year",{
    get:function(){
    return this._year;
    },
    set: function(newValue){
    if(newValue>2004){
    this._year = newValue;
    this.edition += newValue -2004;
    }
    }
    });
    
    book.year = 2005;
    alert(book.edition);  //2

以上代码创建了一个book对象，并给它定义了两个默认的属性。getter函数返回-year的值，setter函数通过计算来确定正确的版本，因此把year属性修改为2005会导致_year变成2005，edition变为2

Object.defineProperties(),利用这个方法可以通过描述符一次性定义多个属性，该函数接收两个参数，属性所在的对象以及需要修改的属性及其描述符对象组成的对象

    var book = {};
    Object.defineProperties(book,{
    	_year:{
    		writable:true,
    		value:2004},
   		edition:{
    		writion:true,
    		value:1},
    	year:{
    		get:function(){
    		return this._year;
    	},
    	set: function(newValue){
    		if(newValue>2004){
    			this._year = newValue;
    			this.edition += newValue -2004;
    	}
    }
    }
    
    });

读取属性的方法

Object.getOwnPropertyDescriptior() 

接受两个参数,属性所在的对象和要读取其描述符的属性名称,返回值是一个对象

如果是访问其属性 这个对象的属性有configurable,enumerable,get,set

如果是数据属性 这个对象的属性有configurable,enumerable,writable,value

    var book ={};
    
    Object.defineProperties(book,{
    	_year:{
    		value:2004	
    	},
    	edition:{
    		value:1
    	},
    	year:{
    		get:function(){
    			return this._year;
    		},
    		set:function(newValue){
    			if(newVlaue>2004){
    				this._year = newValue;
    				this.edition += newValue - 2004;
    			}
    		}
    	}
    })
    
    var descriptor = Object.getOwnPropertyDescriptor(book,"_year");
    
    alert(descriptor.value);   //2004
    alert(description.configurable); //false
    alert(typeOf descriptor.get);  //undefined
    var descriptor = Object.getOwnPropertyDescriptor(book,"year");
    alert(descriptor.value);  //undefined
    alert(descriptor.enumerable); //false
    alert(typeOf descriptor.get);  //function


----------
### 工厂模式 ###
这种模式抽象了创建具体对象的过程,用函数来封装以特定接口创建对象的细节

    function creatPerson(name,age,job){
    	var o = new Object();
    	o.name = name;
    	o.age = age;
    	o.job = job;
    	o.sayName =  function(){
    	alert(this.name)
    	};
    	return o;
    }
    
    var person1 = creatPerson("n",29,"software");

但是工厂模式无法识别对象(即怎么知道一个对象的类型)

### 构造函数 ###

    function Person(name,age,job){
    	this.name =name;
    	this.age = age;
    	this.job = job;
    	this.sayName = function(){
    		alert(this.name);
    	};
    }
    var person1 = new Person("sd",29,"softethe");

通过构造函数可以创建自定义对象类型的属性和方法

构造函数过程:

1.创建一个新对象;
2.将构造函数的作用域赋给新对象(因此this就指向了这个新对象);
3.执行构造函数中的代码
4.返回新对象

person1,person2保存着person的不同实例,这两个函数都有一个constructor(构造函数)属性,该属性指向person
	
	alert(person1.constructor ==person);//true

	alert(person1 instanceof Object);//true

	alert(person1 instanceof Person); //true

创建自定义的构造函数意味着将来可以把它的实例标识为一种特定的类型

构造函数不加new,this对象会被指向global对象(在浏览器中就是window对象)

每个person实例都会包含一个不同的function实例,以这种方式创建函数,会导致不同的作用域链和标识符解析,所以有了原型模式的产生

### 原型模式 ###

创建的每个函数都有一个prototype属性,这个属性是一个指针,指向一个对象,而这个对象的用途是包含可以有特定的所有实例共享的属性和方法

例:

    function Person(){
    }
    
    Person.prototype.name = "sd";
    Person.prototype.age = 29;
    Person.prototype.job = "sofether";
    Person.prototype.sayName = function(){
    	alert(this.name);
    };
    
    var person1 = new Person();
    var person2 = new Person();
    
    alert(person1.sayName == person2.sayName);//true

理解原型对象 p148

当创建一个新函数时,就会为该函数创建一个prototype属性,这个是姓指向函数的原型对象,而原型对象则会获得一个constructor(构造函数)属性,这个属性是一个指向函数的指针

当函数创建了一个实例后,会包含一个内部属性,该属性指向了构造函数的原型对象,也就是说,实例与构造函数并没有直接的关系

当向实例请求一个属性值的时候,会执行一次搜索,如果实例中具有给定名字的属性,则会返回该属性的值,否则会在该实例的原型中查找具有给定名字的属性

hasOwnProperty()方法可以检测一个属性是存在于实例中,还是原型中,只有当存在于实例中,会返回true,in操作符只要可以访问就会返回true,所以当in操作符返回true,hasOwnProperty()返回false,就可以确定属性是原型中的属性

在ECMAscript5中Object.keys();方法,可以返回包含所有可枚举属性的字符串数组(原型中的属性不算);

    function Person(){}
    Person.prototype.name = "nic";
    Person.prototype.age = 29;
    Person.prototype.sayname = function(){
    alert(this.name);
    };
    var p1 = new Person();
    p1.name = "rob";
    p1.age = 31;
    var p1keys = Object.keys(p1);
    console.log(p1keys);//name,age

### 原型语法的简化写法 ###

    function Person(){
    }
    Person.prototype = {
    name:"sd",
    age:21,
    sayName:function(){
    alert(this.name);
    }
    };

这样写之后constructor属性不再指向Person,而指向Object,因为每创建一个函数,同时会创建他的prototype对象,这个对象也会自动获得constructor属性

如果有特别的需要,可以在原型函数中通过指定constructor属性

### 原型模式和构造模式混合使用 ###

    function Person(name,age){
    	this.name = name;
    	this.age = age;
    	this.friends = ["sd","cs"];
    }
    Person.prototype = {
    	constructor:Person,
    	sayName : function(){
    	alert(this.name);
    	}
    }
    var person1 = new Person('qq',21);
    var person2 = new Person('ww',20);
    person1.friends.push('van');
    alert(person1.friends);  //sd,cs,van
    alert(person2.friends);  //sd,cs

p160

### 稳妥构造函数模式 ###

    function Person(name,age){
    	//创建要返回的对象
    	var o = new Object();
    	//定义私有变量和函数
    	//添加方法
    	o.sayName = function(){
    		alert(name);	
    	}
    	return o;
    }
    
    var person1 = Person("sd",21);
    person1.sayName();//"sd"

在一些安全环境中会禁用this和new,或者防止数据被其他应用程序改动时使用(Mashup)

这种模式创建的对象,除了使用sayName()方法外,没有其他方法可以访问其数据成员

### 原型链 ###

每个构造函数都有一个原型对象,原型对象包含一个指向构造函数的指针,而实例包含一个指向原型对象的内部指针

如果原型对象等于另一个对象的实例,则这个原型对象会包含一个指向另一个原型的内部指针,相应的,另一个原型中也包含着一个指向另一个构造函数的指针.层层递进,就是原型链的基本概念

    //定义方法
    	function Supertype(){
    	this.property = true;
    }
    //定义原型方法
    	Supertype.prototype.getSuperValue = function(){
    	return this.property;
    };
    //定义方法
    	function Subtype(){
    	this.subproperty = false;
    }
    //将新函数的原型指向原函数的实例,同时继承supertype
    	Subtype.prototype = new Supertype();
    //定义新函数原型方法
    	Subtype.prototype.getSubValue = function(){
    	return this.subproperty;
    };
    //新函数创建实例
    	var instance = new Subtype();
    	alert(instance.getSuperValue()); //true

以上函数将subtype默认提供的原型,重写为supertype的实例,新原型不仅作为一个supertype的实例所拥有的全部属性和方法,而且其内部还有一个指针,指向supertype的原型,最终结果就是:instance指向subtype的原型,subtype的原型又指向supertype的原型,此时instance的constructor指向supertype,所以在查询属性名的时候,会先在实例中查找,然后在subtype的原型中查找,然后在supertype的原型中查找,在查找不到属性和方法时,搜索过程会前行到原型链末端

所有函数的默认原型都是Object的实例,因此默认原型会包含一个内部指针,指向Object.prototype

在通过原型链实现继承时,不能使用对象字面量创建原型方法, 因为重写后的原型对象,不再指向被继承的对象,而是指向Object的原型对象

### 借用构造函数 ###

    function supertype (){
    	this.colors = ["red",'blue,','green'];
    }
    function subtype(){
    	supertyep.call(this);
    }
    var instance1 = new subtype();
    instance1.colors.push('black');
    alert(instance1.colors);//red,blue,green,black
    var instance2 = new subtype();
    alert(instance2.colors);//red,blue,green

call方法借调了超类型的构造函数,通过调用call方法,可以在新创建的subtype实例的环境下调用了supertype构造函数

借用构造函数也可以传递参数

    function supertype(name){
    	this.name = name;
    }
    function subtype(){
    	supertype.call(this,"sd");
    	this.age = 29;
    }
    var instance = new subtype();
    alert(instance.name);//sd
    alert(instance.age); //29

### 组合继承 ###

    function supertype(name){
    	this.name = name ;
    	this.colors = ["red","blue","green"];
    }
    supertype.prototype.sayname = function(){
    alert(this.name);
    };
    function subtype(name,age){
    	supertype.call(this,name);
    	this.age = age;
    }
    subtype.prototype = new supertype();
    subtype.constructor = subtype;
    subtype.prototype.sayage = function(){
    	alert(this.age);
    };
    var instance1 = new subtype("sd",29);
    instance1.colors.push("as");
    alert(instance1.colors); //red,blue,green,as
    instance1.sayname(); //sd
    instance1.sayage(); //29
    var instance2 = new subtype("qq",21);
    alert(instance2.colors); //red,blue,green
    instance2.sayname(); //qq
    instance2.sayage(); //21

supertype函数定义了两个属性:name,colors它的原型定义了sayname方法,subtype构造函数在调用supertype构造函数时传入了name参数,又定义了自己的age属性,然后将supertype的实例赋值给subtype的原型,又在该原型上定义了方法sayage,这样就可以让两个不同的subtype实例即分别拥有自己的属性,又可以使用相同的方法

原型式继承:

寄生式继承:

寄生组合式继承:

都神马玩意~~~~

## 第七章:函数表达式 ##

函数声明提升:在执行代码之前会先读取函数声明,这意味着可以把函数声明放在调用它的语句后面,但是函数声明和函数表达式有区别,此规则在函数表达式下不适用

函数声明

    function s(){
    //yoooooo
    }

函数表达式

    var s = function(){
    //yoooooo
    }

### 递归 ###

递归函数是在一个函数通过名字调用自身的情况下构成的

    function factory(num){
    	if(num<=1){
    		return 1;
    	}else{
    		return num* factory(num-1);
    	}
    }

但是加入以下的代码会导致出错
    
    var sd = factory;
    factory =null;
    console.log(sd(5));

在不确定函数名字或匿名函数的时候可以使用arguments.callee
,他是一个指向正在执行的函数的指针,在严格模式下无法使用

    function factory(num){
    	if(num<=1){
    		return 1;
    	}else{
    		return num* arguments.callee(num-1);
    	}
    }

以上的效果也可以通过使用命名函数表达式来实现同样的效果,在严格模式下同样可用

var factory = (function f(num){
	if(num<=1){
		return 1;
	}else{
		return num*f(num-1);
	}
});

### 闭包 ###

创建闭包的常见方式,就是在一个函数内部创建另一个函数

在函数被调用时,会创建一个执行环境及相应的作用域链,在作用域链中外部函数的活动对象始终处于第二位,直到最后的全局执行环境,作用域链是一个指向变量对象的指针列表

内部函数会将外部函数的活动对象添加到它的作用域链中,普通函数中定义的局部变量,会在调用后销毁,但是闭包不会,因为在外部函数执行完毕后,其内部函数的作用域链仍在引用这个活动对象,在外部函数返回后,它的作用域链被初始化为其函数内的活动对象和全局变量对象,其执行环境的作用域链会被销毁,但是他的活动对象仍会留在内存中,直到匿名函数被销毁后,其活动对象才会被销毁
    
    //创建对象
    var com = creat("name");
    //调用函数
    var result = com({name:"nic"},{name:"greg"});
    //解除对匿名函数的引用(以便释放内存)
    com =null;

闭包与变量,关于this对象 p182

匿名函数的执行环境具有全局性

