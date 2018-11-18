---
layout: post
title: 'ECMAScript6'
date: 2018-9-14
subtitle: 'ES6基础'
categories: 笔记
cover: 'https://farm5.staticflickr.com/4805/44117243400_c3beab9d50_o.png'
tags: ECMAScript6
---
# ES6 基础

**ES6作用于严格模式下,严格模式主要有以下限制**

- 变量必须声明后再使用
- 函数的参数不能有同名属性
- 不能使用with语句
- 不能对只读属性赋值
- 不能使用前缀0表示八进制数
- 不能删除不可删除的属性
- 不能删除变量delete prop，只能删除属性delete global[prop]
- eval不会在它的外层作用域引入变量
- eval和arguments不能被重新赋值
- arguments不会自动反映函数参数的变化
- 不能使用arguments.callee
- 不能使用arguments.caller
- 禁止this指向全局对象
- 不能使用fn.caller和fn.arguments获取函数调用的堆栈
- 增加了保留字(比如protected、static、interface)

[TOC]



**let **

类似于var

声明变量，不能重复声明。存在块级作用域。存在暂时性死区

**const**

声明时应该初始化，否则报错。

声明常量不可重新赋值

## 箭头函数

ES6允许使用箭头（=>）定义函数

```()=>{}```等于一个匿名函数，如果不需要传参，或需要传递多个参数，可以用这种形式

```javascript
(a,b)=>{return a+b}
```

如果函数只需要传递一个参数，那么可以将括号替换为所需要传递的参数

```
a=>{console.log(a)}
```

因为箭头函数默认为一个匿名函数，所以如果需要调用可以将其赋值给一个变量

```javascript
const a  = b=>{console.log(b)};a('1')
```

箭头函数可以简化返回值的操作，例如

```const a = b=>b*b;```等同于```function a(b){return b*b};```

且箭头函数不可以用于构造函数，即不可以使用new关键字，否则报错

另如果需要返回对象，需要以这种形式```const a = ()=>({a:1,b:2})```,因为花括号被认为函数体的开始，不加括号不会返回想要的结果

this会被绑定为函数所在的上下文环境，细节看书

## 模板字符串

模板字符串是字符串的增强版，字符串plus，用反引号（`）标识。可以当做普通字符串用，同时换行空格被支持。

模板字符串中可以使用变量，**${}**。例如：

```javascript
let a = like;
const string = `i ${a} you` //i like you
```

同时，模板字符串花括号中不只可以使用变量，同时可以使用任意的javascript表达式，包括调用函数，只要表达式可以返回一个正确的值，且表达式本身无错误，模板字符串都会正常执行



```javascript
const a = ()=>{//do something};
let string = `${a()}` //do something
let strings = `${3>2?yes:false}` //yes
```

## **变量的解构赋值**

ES6中按照一定模式从数组和对象中提取值，然后对变量进行赋值的操作叫做解构赋值

解构赋值可以用于数组，对象，字符串，数值和布尔值，函数参数

### 数组

数组的解构赋值属于“模式匹配”，只要等号两边的模式相同，左边的变量就会被赋予相应的值

```javascript
let [a,b,c] = [1,2,3];
let [foo,[[boo],coo]] = [1,[[2],3]];
let [x,,y] = [1,2,3] //x = 1 y =3
```

如果解构失败，变量的值就等于**undefined**

```javascript
let [foo] = [];   //undefined
let [bar ,foo ] = [1]; //  undefined
```

为了避免上面这种情况可以为变量指定默认值

```javascript
let [foo = true] = []; //foo = true
let [x,y = 'b'] = ['a'] //x = 'a' ,y = 'b'
```

另外，ES6内部使用严格相等运算符(===)判断一个位置是否有值。所以，如果一个数组成员不严格等于undefined，默认值不生效

```javascript
let [x = 1] = [null]; //x = null
```

如果默认值是一个表达式，那么这个表达式是惰性求值的，即只有在用到的时候才会求值

```javascript
let f = ()=>{console.log('a')};
let [x = f()] = [1] ; //x = 1
```

上面的方法不会被执行

另外，默认值可以被指定为解构赋值的其他变量，前提是该变量必须已经声明

```javascript
let [x = 1,y = x] = [];//x = 1; y = 1
let [x = 1,y = x] = [2]; // x = 2, y = 2
let [x = 1,y = x] = [1,2]; //x = 1,y = 2
let [x = y, y = 1] = [];//错误
```

最后一个表达式会抛出错误，因为在x用到y的时候，y还没有被声明

当等号右边的子元素多于左边时，可以解构成功。但属于不完全解构，可以用rest接收剩余的元素

```javascript
let [x,y] = [1,2,3] // x= 1 y = 2 
```

如果等号右边是不可遍历解构，或转为对象后不具有**Iterator**接口，会导致解构失败，且抛出错误

### 对象

对象的解构赋值与数组不同的是，数组的元素是按次序排列的，变量的取值由他们的位置决定。而对象的属性没有次序，变量必须与属性同名才能取到正确的值

```javascript
let {bar,foo} = {foo:"aaa",bar:"bbb"} //foo = "aaa",bar = "bbb"
let {vaz} = {foo:"aaa"} //vaz = undefined
```

如果想要把值赋给一个新的变量，而不是沿用原来的属性名，可以直接指定

```javascript
let obj = {first:'hello',last:'world'};
let {first:f,last:l} = obj;
f //'hello'
l //'world'
```

对象的解构赋值是先找到同名属性，然后再赋值给对应的变量，前者只用于匹配，不会生成变量，后者用于被赋值，会生成新的变量；

```javascript
let {p:[x,{y}]} = {p:['hello',{y:'world'}]}; 
x //'hello'
y // 'world'
```

同数组的解构赋值一样对象的解构也可以指定默认值，生效条件是对象的属性值严格等于undefined

```javascript
var {x=3} = {};
x//3
var {x:y=3} = {};
y//3
```

### 字符串

字符串也可以解构赋值。因为字符串被转换成了一个类数组对象

```javascript
const [a,b,c,d,e] = 'hello';
a//'h'
b//'e'
c//'l'
d//'l'
e//'o'
```

类数组对象都有一个length属性，因此可以对这个属性进行解构赋值

```javascript
let {length:len} = 'hello';
len // 5
```

### 数组和布尔值

解构赋值的规则是，只要等号右边的值不是对象或数组，就先将其转为对象。undefined和null无法转为对象，所以会抛出错误

```javascript
let {toString:s} = 123;
s === Number.prototype.toString //true
let {toString:s} = true;
s === Boolean.prototype.toString //true
let {prop:x} = undefined //TypeError
let {prop:y} = null //TypeError
```

### 函数

函数的参数也可以使用解构赋值

```javascript
let add = ([x,y])=>x+y;
add([1,2]); //3
add(1,2); //TypeError
```

上面的例子中传入的参数会被解构为两个变量

同样的，函数参数的解构也可以指定默认值

```javascript
let move = ({x=0,y=0}={})=>[x,y]
move({x:3,y:8}); //[3,8]
move({x:3}); //[3,0]
move({}); //[0,0]
move(); //[0,0]
```

### 解构赋值的用途

#### 交换变量的值

```javascript
let x = 1;
let y = 2;
[x,y] = [y,x];
```

#### 从函数返回多个值

```javascript
//返回一个数组
let example = ()=>[1,2,3];
let [a,b,c] = example();
//返回一个对象
let example = ()=>{foo:1,bar:2};
let {foo,bar} = example();
```

#### 函数参数的定义

可以很方便的将一组参数与变量名对应起来

```javascript
//参数是一组有次序的值
let f = ([x,y,z])=>{ //do something};
f([1,2,3]);
//参数是一组无次序的值
let f = ({x,y,z})=>{ //do something};
f({z:3,y:2,x:1});
```

#### 提取JSON数据

```javascript
let jsondata = {id:42,status:'ok',data:[867,1]};
let {id,status,data:number} = jsondata;
id // 42
status //'ok'
number //[867,1]
```

#### 函数参数的默认值

```javascript
let jQuery.ajax = (url,{
async=true,
beforeSend = function(){},
cache=true,
complete=function(){},
crossDomain=false,
global=true,})=>{ // do something}
```

#### 遍历Map结构

```javascript
let map = new Map();
map.set('first','hello');
map.set('second','world');
for(let [key, value] of map){console.log(key+"is"+value)};
//first is world
//second is world
```

如果只要获取键名，或者只想获取键值，可以向下面这样写

```javascript
//获取键名
for(let [key] of map){ // ... }
//获取键值
for(let [,value] of map){ // ... }
```

输入模块的指定方法

加载模块时，往往需要指定输入的方法。解构赋值是的输入语句非常的清晰

```javascript
const {SourceMapConsumer, SourceNode} = require('source-map')
```





## spread

**...**扩展运算符用于展开操作,该运算符主要用于函数调用

```javascript
console.log(...[1,2,3]) //1 2 3
console.log(1,...[2,3,4],5) //1 2 3 4 5

let push = (array,...items)=>{array.push(...items)};

let add = (x,y)=>x+y;
add(...[4,38]) //42

Math.max(...[14,3,77]);

let arr1=[0,1,2];
let arr2=[3,4,5];
arr1.push(...arr2);
```

扩展运算符也可以放置表达式，如果放置空数组，则不产生任何效果

```javascript
const arr = [...(x>0?['a']:[]),'b'];
[...[],1] //[1]
```

### spread运算符的应用

#### 合并数组

```javascript
[1,2,...more]
let arr1= ['a','b'];
let arr2= ['c'];
let arr3= ['d','e'];
[...arr1,...arr2,...arr3]
```

#### 与解构赋值结合

```javascript
const [fi,...rest] = [1,2,3,4,5]
fi //1
rest // [2,3,4,5]

const [...btn,last] = [1,2,3,4,5] //报错
const [first,...middle,last] = [1,2,3,4,5] //报错
```

如果将扩展运算符应用于数组赋值，那么只能将其放在参数的最后一位，否则报错

#### 函数的返回值

函数如果需要返回多个值，只能返回数组或对象。扩展运算符可以简化这一操作

```javascript
var datef = readDAte(database);
var d = new Date(...datef);
```

#### 字符串

扩展运算符还可以将字符串转为数组。

```javascript
[...'hello'];
// ["h","e","l","l","o"]
```

而且这种写法有一个好处，可以正确识别32位的Unicode字符。

```javascript
'x\uD83D\uDE80y'.length //4
[...'x\uD83D\uDE80y'].length //3
console.log('x\uD83D\uDE80y') //x🚀y
```

js会将32位Unicode字符识别为2个字符。因此，如果遇到这种情况，最好都用扩展运算符改写

## rest

ES6中引入了rest参数（形式为“...变量名”），用于获取函数的多余参数，多出来的参数会被放入一个数组里

```javascript
let add = (...values)=>{
	let sum = 0;
	for(let val of values){
    sum +=val;
	}
	return sum;
}
add(2,5,3) //10
```

上面是一个简单的求和函数，通过rest参数接收剩余参数，就可以实现传入任意数目的参数

同样的，rest参数之后不能再有其他参数，否则报错

```javascript
let push = (array,...items)=>{
    items.forEach((item)=>{
        array.push(item);
    });
}
var a = [];
push(a,1,2,3);
a //[1,2,3]
```

## class

类方法等同于构造函数，使用时需要通过new关键字，直接调用会报错，而且不需要加上function保留字，定义的原型方法之间不需要逗号分隔

```javascript
class Point{
    constructor(){
        this.x = 1;
        this.y = 2;
    }        //构造函数部分
    toString(){
        //do something
    }  //定义在原型上的方法
}
let b = new Point();
```

构造函数的prototype属性在ES6的类上继续存在，所有的方法都被定义在prototype属性上，在类的实例上调用方法，其实就是调用原型上的方法

由于类的方法(除constructor外)都是定义在prototype对象上，所以类的新方法可以添加在prototype对象上，添加多个方法可以使用 **Object.assign**方法

```javascript
let fn = ()=>{console.log('1')};
class Point{
    constructor(){
        //do something
    }
};


Object.assign(Point.prototype,{
    tostring(){
        //ssss
    },
    tovalue(){
        //ssss
    },
    fn
});

```

class类一定含有一个construcotr属性，如果在创建class类的时候，没有定义constructor属性，那么这个类会被默认赋予一个空的constructor属性

class也可以使用表达式的形式定义，此时可以省略class后面的关键字

```javascript
const myclass = class{
        constructor(){
        //do something
    }
}
```

[私有方法，私有属性,this指向等](http://es6.ruanyifeng.com/?search=rest&x=0&y=0#docs/class#%E7%A7%81%E6%9C%89%E6%96%B9%E6%B3%95%E5%92%8C%E7%A7%81%E6%9C%89%E5%B1%9E%E6%80%A7)

class的静态方法

类相当于实例的原型，所有在类中定义的方法都会被实例继承，如果在一个方法前面加上static关键字，就表示该方法不会被实例继承，而是通过类调用。此时如果在实例上调用这个方法，就会抛出错误

```javascript
class foo{
    static classmethod(){
        //do something
    }
}
foo.classmethod() //
```

父类的静态方法可以被子类继承

```javascript
class foo{
    static classmethod(){
        //do something
    }
}
class bar extends foo{}

bar.classmethod()
```

## 继承

class可以通过extends关键字实现继承，例如上面的例子

子类必须在constructor方法中调用super方法，否则创建实例时以及使用this关键字会报错，这是因为子类没有自己的this对象，而是继承父类的this对象，然后对其进行加工。如果不调用super方法，子类就得不到this对象

````javascript
class point extends sd{
    constructor(x,y){
        this.x = 1; //报错
        super(x,y)
        this.y = 2; //正常
    }
}
Object.getPrototypeof(point) === sd //true
````

super()就是调用了一次父类的构造函数

super关键字可以当做函数使用，也可以当做对象使用，当当做函数使用时，只可以用在类的constructor中，用在其他地方会抛出错误，且当子类继承父类时必须调用一次super()方法

```javascript
class A{}
class B extends A{
    constructor(){
        super();
    }
}
```

当super当作对象使用时，在普通方法中指向父类的原型对象。同时，因为super指向父类的原型对象，所以定义在父类实例上的方法或者属性是无法通过super调用的

```javascript
class A{
    p(){
        //
    }
}
class B extends A{
    constructor(){
        super();
        console.log(super.p());
    }
}
//属性同理
```

当且仅当子类调用了super()方法后，子类可以定义新的属性或方法，也可以重写父类中已有的属性或方法

## Module

ES6的模块功能主要由两个命令构成：export和import。

###export

export命令用于规定模块的对外接口，import命令用于输入其他模块提供的功能

```javascript
export let a = 'a';
export let b = 'b';

let a = 'a';
let b = 'b';
export {a,b}
```



export命令规定的是对外的接口，必须与模块内部的变量建立一一对应关系

```javascript
//报错
export 1;
//报错
var m = 1;
export m;
```

上面两种写法都会报错，因为没有提供对外的接口。1只是一个值，不是接口

```javascript
//写法一
export var m = 1;
//写法二
var m = 1;
export{m};
//写法三
var n = 1;
export{n as m} 
//以别名m输出
```

同样的，function和class的输出也必须采用这样的写法

```javascript
//报错
let f = ()=>{};
export f;
//写法一
export let f = ()=>{}
//写法二
let f = ()=>{}
export {f};
```

export语句输出的接口与其对应的值是动态绑定关系，即通过该接口可以取到模块内部实时的值

```javascript
export var foo = 'bar'
setTimeout(()=>foo = 'baz',500);
```

export命令以及import命令可以出现在模块的任意位置，只要保证其在模块顶层就可以，如果处于块级作用域内，就会报错

### import

```javascript
import {a,b,c} from './profile';//不需要加后缀名
```

如果想重命名输入的变量，可以通过as关键字

```javascript
import {lastname as name} from './profile';//可以为绝对路径
```

import命令具有提升效果，会提升到整个模块的头部并首先执行，因此，下面的写法是不会报错的

```javascript
foo();
import {foo} from './bundle';
```

由于ES6的模块倡导的是静态优化，所以import是静态执行的，因此不能在其中使用表达式和变量，以及只有在运行时才能得到结果的语法结构

目前，通过Babel转码，commonjs的命令和ES6的模块化命令，可以写在一个模块里，但这并不被支持。因为import会在静态解析阶段执行，会优先于commonjs的模块化命令，可能会得不到想要的结果

### 模块整体加载

可以使用(*)来指定一个对象，所有输出值都加载在这个对象上

```javascript
//cilcle.js
let a = ()=>{}
//bundle.js
import * as circle form './circle';
circle.a();
```

同时需要注意的是，模块整体加载所在的对象应该是可以静态分析的，所以不允许运行时改变

````javascript
import * as circle from './circle';

circle.foo = 'a';//报错
circle.area = ()=>{};//报错
````

### export default

export default规定了默认输出，默认输出有且仅有一个。

export default输出的函数默认为匿名函数，需要使用时重新命名，所以即使默认输出了一个有名字的函数，这个名字也仅限于在本模块生效。

export default命令的本质是将该命令后面的值赋给default变量后再默认，所以输出变量或者函数时不用加花括号，因为此时已经存在接口，默认为default,import引入的时候也不需要加花括号

```javascript
export default function foo(){
    //
}
//或者
let foo = ()=>{}
export default foo;
//正确
export var a = 1;
//正确
var a = 1;
export default a;
//错误
export default var a = 1;
//默认将a的值赋给default，所以上面这种写法会报错
```

在载入模块的时候，可以同时输入其他接口

```javascript
import as from 'file';
import as,{each,one} from 'file'

//export default也可以用来输出类

export default class{...}

import myclass from 'file';
let a = new myclass();
```

export与import的复合写法，如果需要在一个模块中输入后输出同一个模块

```javascript
export {foo,bar} from 'my';
//等同于
import {foo,bar} from 'my';
export {foo,bar};

//接口改名
export {foo as myfoo} from 'my';
//整体输出
export * from 'my';
//默认接口
export {default} from 'my';
//具名接口改为默认接口
export {es6 as default} from 'my';
//等同于
import {es6} from 'my';
export default es6;
//默认接口改为具名接口
export {default as es6} from 'my'
```

上面的整体输出可以实现模块的继承

```javascript
export * from 'circle';
export var e = 'a';
export default ()=>{}；


```

export *命令会忽略circle模块的default方法。

## 数组的扩展方法

### Array.map()



**map()** 方法创建一个新数组，其结果是该数组中的每个元素都调用一个提供的函数后返回的结果。

```javascript
let new_array = arr.map(function callback(currentValue, index, array) { 
    // Return element for new_array 
}[, thisArg])
```

`callback`

- `currentValue`

  `callback` 的第一个参数，数组中正在处理的当前元素。

- `index`

  `callback` 的第二个参数，数组中正在处理的当前元素的索引。

- `array`

  `callback` 的第三个参数，`map` 方法被调用的数组。

`thisArg`可选的。执行 `callback` 函数时 使用的`this` 值。 

`map` 方法会给原数组中的每个元素都按顺序调用一次  `callback` 函数。`callback` 每次执行后的返回值组合起来形成一个新数组。 `callback` 函数只会在有值的索引上被调用；那些从来没被赋过值或者使用 `delete` 删除的索引则不会被调用。

`callback` 函数会被自动传入三个参数：数组元素，元素索引，原数组本身。

如果 `thisArg` 参数有值，则每次 `callback` 函数被调用的时候，`this` 都会指向 `thisArg`参数上的这个对象。如果省略了 `thisArg ``参数,``或者赋值为 null` 或 `undefined`，则 this 指向全局对象 。

`map `不修改调用它的原数组本身（当然可以在 `callback` 执行时改变原数组）。

使用 map 方法处理数组时，数组元素的范围是在 callback 方法第一次调用之前就已经确定了。在 map 方法执行的过程中：原数组中新增加的元素将不会被 callback 访问到；若已经存在的元素被改变或删除了，则它们的传递到 callback 的值是 map 方法遍历到它们的那一时刻的值；而被删除的元素将不会被访问到。

 

### Array.filter()

**filter()** 方法创建一个新数组, 其包含通过所提供函数实现的测试的所有元素。 

```javascript
var words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];

const result = words.filter(word => word.length > 6);

console.log(result);
// expected output: Array ["exuberant", "destruction", "present"]
```

```javascript
var new_array = arr.filter(callback(element[, index[, array]])[, thisArg])
```

`callback`

	用来测试数组的每个元素的函数。调用时使用参数 (element, index, array)。
	返回true表示保留该元素（通过测试），false则不保留。它接受三个参数：

- **element**

  当前在数组中处理的元素

- **index（可选）**

  正在处理元素在数组中的索引

- **array（可选）**

  调用了filter筛选器的数组

`thisArg（可选）`

	可选。执行 `callback` 时的用于 `this` 的值。

这个方法会返回一个新的通过测试的元素的集合的数组，如果没有通过测试则返回空数组

`filter` 为数组中的每个元素调用一次 `callback` 函数，并利用所有使得 `callback` 返回 true 或 [等价于 true 的值](https://developer.mozilla.org/en-US/docs/Glossary/Truthy) 的元素创建一个新数组。`callback` 只会在已经赋值的索引上被调用，对于那些已经被删除或者从未被赋值的索引不会被调用。那些没有通过 `callback` 测试的元素会被跳过，不会被包含在新数组中。

`callback` 被调用时传入三个参数：

1. 元素的值
2. 元素的索引
3. 被遍历的数组

如果为 `filter` 提供一个 `thisArg` 参数，则它会被作为 `callback` 被调用时的 `this` 值。否则，`callback` 的 `this` 值在非严格模式下将是全局对象，严格模式下为 `undefined`。
The `this`value ultimately observable by `callback` is determined according to [the usual rules for determining the`this` seen by a function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this).

（ 回调函数最终观察到 "this" 的值是根据[通常函数所看到的 "this"的规则](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/this)确定的。）

`filter` 不会改变原数组，它返回过滤后的新数组。

`filter` 遍历的元素范围在第一次调用 `callback` 之前就已经确定了。在调用 `filter` 之后被添加到数组中的元素不会被 `filter` 遍历到。如果已经存在的元素被改变了，则他们传入 `callback` 的值是 `filter` 遍历到它们那一刻的值。被删除或从来未被赋值的元素不会被遍历到。

### Array.some()

**some()**方法测试数组中的某些元素是否通过由提供的函数实现的测试。

```javascript
var array = [1, 2, 3, 4, 5];

var even = function(element) {

  // checks whether an element is even

  return element % 2 === 0;

};

console.log(array.some(even));

// expected output: true

```

```javascript
arr.some(callback[, thisArg])
```

如果回调函数返回任何数组元素的[truthy](https://developer.mozilla.org/en-US/docs/Glossary/truthy)值，则返回**true**；否则为**false**。

`callback`

- `currentValue`

  数组中正在处理的元素。

- `index` 可选

  数组中正在处理的元素的索引值。

- `array`可选

  `some()`被调用的数组。

`thisArg`可选执行 `callback` 时使用的 `this` 值。

`some` 为数组中的每一个元素执行一次 `callback` 函数，直到找到一个使得 callback 返回一个“真值”（即可转换为布尔值 true 的值）。如果找到了这样一个值，`some` 将会立即返回 `true`。否则，`some` 返回 `false`。`callback` 只会在那些”有值“的索引上被调用，不会在那些被删除或从来未被赋值的索引上调用。

`callback` 被调用时传入三个参数：元素的值，元素的索引，被遍历的数组。

如果为 `some` 提供了一个 `thisArg` 参数，将会把它传给被调用的 `callback`，作为 `this` 值。否则，在非严格模式下将会是全局对象，严格模式下是 `undefined`。

`some` 被调用时不会改变数组。

`some` 遍历的元素的范围在第一次调用 `callback`. 时就已经确定了。在调用 `some` 后被添加到数组中的值不会被 `callback` 访问到。如果数组中存在且还未被访问到的元素被 `callback`改变了，则其传递给 `callback` 的值是 `some` 访问到它那一刻的值。

### Array.every()

**every()** 方法测试数组的所有元素是否都通过了指定函数的测试。

与some相对，接收的参数都是相同的。

数组的所有元素都返回true，才返回true。否则返回false

### Array.reduce()

**reduce()** 方法对累加器和数组中的每个元素（从左到右）应用一个函数，将其减少为单个值。



```javascript
const array1 = [1, 2, 3, 4];
const reducer = (accumulator, currentValue) => accumulator + currentValue;

// 1 + 2 + 3 + 4
console.log(array1.reduce(reducer));
// expected output: 10

// 5 + 1 + 2 + 3 + 4
console.log(array1.reduce(reducer, 5));
// expected output: 15
```

```javascript
arr.reduce(callback[, initialValue])
```

`callback`

执行数组中每个值的函数，包含四个参数：


`accumulator`

- `currentValue`

  数组中正在处理的元素。

- `currentIndex`可选

  数组中正在处理的当前元素的索引。 如果提供了`initialValue`，则索引号为0，否则为索引为1。

- `array`可选

  调用`reduce`的数组

`initialValue`可选

用作第一个调用 `callback`的第一个参数的值。 如果没有提供初始值，则将使用数组中的第一个元素。 在没有初始值的空数组上调用 reduce 将报错。

如果不传入初始值，且数组只有一个元素，那么callback将不会被执行

`reduce`为数组中的每一个元素依次执行`callback`函数，不包括数组中被删除或从未被赋值的元素，接受四个参数：

- `accumulator `
- `currentValue `
- `currentIndex `
- `array`

回调函数第一次执行时，`accumulator` 和`currentValue`的取值有两种情况：调用`reduce`时提供`initialValue`，`accumulator`取值为`initialValue`，`currentValue`取数组中的第一个值；没有提供 `initialValue`，`accumulator`取数组中的第一个值，`currentValue`取数组中的第二个值。

每一次执行回调函数，第一个参数为上一次回调函数所return出来的值，如果函数不返回任何值，那么将为undefined。如果传入初始值，那么第一个参数将为初始值，否则为数组第一个元素的值

## Set

ES6提供了新的数据结构，Set类似于数组，但其成员的值都是唯一的，没有重复。

Set本身是一个构造函数

```javascript
const s = new Set();
[2,3,4,5,2].forEach(x=>s.add(x));
for(let i of s){
    console.log(i)
}
// 2 3 4 5
```

Set函数可以接收一个数组(或者具有iterable接口的其他数据结构)作为参数，用来初始化。

````javascript
const set = new Set([1,2,3,4,5]);
[...set]
//[1,2,3,4,5]
//去除数组的重复成员
[...new Set(array)]
````

Set的实例具有以下属性。

```javascript
Set.prototype.size //返回Set实例的成员总数
const s = new Set();
s.size //0
```

Set的实例具有以下方法

```javascript
add(value) //添加某个值，返回Set结构本身
delete(value) //删除某个值，返回一个布尔值，表示删除是否成功
has(value) //返回一个布尔值，表示参数是否为Set的成员
clear() //清除所有成员，无返回值
```

```javascript
s.add(1).add(2).add(2)

s.size //2

s.has(1) //true
s.has(3) //false

s.delete(2);
s.has(2) //false
```

