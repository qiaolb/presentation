# 引人的ECMAScript
Joe



# ECMAScript简介
<!-- section data-transition="zoom" -->


## ECMAScript历史
* 2015年6月17日，ECMAScript 2015发布
* 2009年12月，ECMAScript 5 <!-- .element: class="fragment" -->
* 1999年12月，ECMAScript 3 <!-- .element: class="fragment" -->
* 1998年06月，ECMAScript 2 <!-- .element: class="fragment" -->
* 1997年06月，ECMAScript 1 <!-- .element: class="fragment" -->



## ECMAScript简介
<!-- section data-transition="slide-in fade-out" -->
* 由Ecma国际通过ECMA-262标准化的脚本程序设计语言。
* JavaScript是ECMAScript的实现和扩展


## ECMAScript定义
* 语言语法 – 语法解析规则、关键字、语句、声明、运算符等。
* 类型 – 布尔型、数字、字符串、对象等。
* 原型和继承
* 内建对象和函数的标准库 – JSON、Math、数组方法、对象自省方法等。



## ECMAScript不定义
* HTML
* CSS
* 类似DOM的Web API



## ECMAScript & Javascript
* ECMAScript：JavaScript，JScript，ActionScript
* JavaScript：ECMAScript，DOM和BOM



## 模板字符串
```
console.log(`I'm a "String"`);
I'm a "String"
```

```
function authorize(user, action) {
    if (!user.hasPrivilege(action)) {
    throw new Error(
    `用户 ${user.name} 未被授权执行 ${action} 操作。`);
    }
}
```
<!-- .element: class="fragment" -->

```
$(“#wumai").html(`
西安雾霾
遛狗不见狗，狗绳提在手，
见绳不见手，狗叫我才走。
`);
```
<!-- .element: class="fragment" -->

Note:

* 模板占位符中的代码可以是任意JavaScript表达式，所以函数调用、算数运算等这些都可以作为占位符使用，你甚至可以在一个模板字符串中嵌套另一个，模板套构（template inception）。
* 如果这两个值都不是字符串，可以按照常规将其转换为字符串。例如：如果action是一个对象，将会调用它的.toString()方法将其转换为字符串值。
* 如果你需要在模板字符串中书写反撇号，你必须使用反斜杠将其转义：`\``等价于"`"。
* 同样地，如果你需要在模板字符串中引入字符$和{。无论你要实现什么样的目标，你都需要用反斜杠转义每一个字符：`\$`和`\{`。



## const，let
```
const DELAY = 1000;

let count = 0;
count = count + 1;
```

* 放弃var
* 块级作用域。
<!-- .element: class="fragment" -->



## for循环
```
for (let index = 0; index < myArray.length; index++) {
  console.log(myArray[index]);
}
```

```
myArray.forEach(function (value) {
  console.log(value);
});
```
<!-- .element: class="fragment" -->

```
for (let index in myArray) {
  console.log(myArray[index]);
}
```
<!-- .element: class="fragment" -->

Note:

forEach不能使用break语句中断循环，也不能使用return语句返回到外层函数。

for-in，index是字符串“0”、“1”、“2”，此时很可能在无意之间进行字符串算数计算，例如：“2” + 1 == “21”，这给编码过程带来极大的不便。
作用于数组的for-in循环体除了遍历数组元素外，还会遍历自定义属性。举个例子，如果你的数组中有一个可枚举属性myArray.name，循环将额外执行一次，遍历到名为“name”的索引。就连数组原型链上的属性都能被访问到。
最让人震惊的是，在某些情况下，这段代码可能按照随机顺序遍历数组元素。
简而言之，for-in是为普通对象设计的，你可以遍历得到字符串类型的键，因此不适用于数组遍历。



## for-of循环
```
for (let value of myArray) {
  console.log(value);
}
```


* 这是最简洁、最直接的遍历数组元素的语法
* 这个方法避开了for-in循环的所有缺陷
* 与forEach()不同的是，它可以正确响应break、continue和return语句
* for-in遍历对象属性，for-of遍历数据—例如数组中的值
* 支持大多数类数组对象，例如DOM NodeList对象
* 支持字符串遍历
* 支持Map和Set对象遍历



## 箭头函数
```
[1,2,3].map((function(x) {
  return x + 1;
}).bind(this));
```

```
[1,2,3].map(x => x + 1);  // [2,3,4]
```
<!-- .element: class="fragment" -->



## import 和 export

```
// 全部引入
import React from 'react';
```

```
// 引入部分
import {browserHistory} from 'react-router';
```

```
// 导出默认
export default HeaderComponent;
```

```
// 引入全部并作为 i18n 对象
import * as i18n from '../../../sources/i18n';
```

```
// 部分导出
export HeaderComponent;
```



## 析构赋值
```
// 对象 const user = { name: 'Joe', age: 2 };
 const { name, age } = user;

console.log(`${name} : ${age}`);
// Joe : 2

let { user } = this.props;
 // 数组 const arr = [1, 2]; 
const [foo, bar] = arr; 
console.log(foo);  // 1
```



## Spread Operator
```
// 可用于组装数组。
 const todos = ['Learn es6']; 
[...todos, 'Learn react'];  // ['Learn es6', 'Learn react']
```

```
// 也可用于获取数组的部分项。 
const arr = ['a', 'b', 'c']; 
const [first, ...rest] = arr; // first: 'a'; rest: ['b', 'c']
```

```
// 还可收集函数参数为数组，可变参数 
function directions(first, ...rest) {}
```

```
// 对于 Object 而言，用于组合成新的 Object 。(ES2017 stage-2) 
const foo = {a: 1, b: 2}; 
const bar = {b: 3, c: 2};
 const d = 4;  
const ret = { ...foo, ...bar, d }; // { a:1, b:3, c:2, d:4 }
```



## 生成器 Generators
```
function* quips(name) {
  yield "你好 " + name + "!";
  yield "欢迎来到威发大讲坛! ";
  if (name.startsWith("Joe")) {
    yield "哦，你是 " + name + "， 太帅了！";
  }
  yield "再见！" + name;
}
```


```
> let iter = quips('Joe');
undefined
> iter.next();
{ value: '你好 Joe!', done: false }
> iter.next();
{ value: '欢迎来到威发大讲坛! ', done: false }
> iter.next();
{ value: '哦，你是 Joe， 太帅了！', done: false }
> iter.next();
{ value: '再见！Joe', done: false }
> iter.next();
{ value: undefined, done: true }
```


* 生成器不是线程
* 生成器是迭代器
* 使用function*声明
* 关键字yield

Note:

* 普通函数使用function声明，而生成器函数使用function*声明。
* 在生成器函数内部，有一种类似return的语法：关键字yield。二者的区别是，普通函数只可以return一次，而生成器函数可以yield多次（当然也可以只yield一次）。在生成器的执行过程中，遇到yield表达式立即暂停，后续可恢复执行状态。
* 获取异常尺寸的结果。你无法构建一个无限大的数组，但是你可以返回一个可以生成一个永无止境的序列的生成器，每次调用可以从中取任意数量的值。
* 重构复杂循环。你是否写过又丑又大的函数？你是否愿意将其拆分为两个更简单的部分？现在，你的重构工具箱里有了新的利刃——生成器。当你面对一个复杂的循环时，你可以拆分出生成数据的代码，将其转换为独立的生成器函数，然后使用for (var data of myNewGenerator(args))遍历我们所需的数据。
* 构建与迭代相关的工具。ES6不提供用来过滤、映射以及针对任意可迭代数据集进行特殊操作的扩展库。借助生成器，我们只须写几行代码就可以实现类似的工具。



## Class
```
class Shape { 
  get color() { 
      return this._color; 
  } 
  set color(c) {
     this._color = parseColorAsRGB(c); 
    // this.markChanged();
    //稍后重绘Canvas 
  }
 } 
```



## 继承
```
class Circle extends Shape { 
  constructor(radius) { 
  this.radius = radius; 
  }
  
   static draw(circle, canvas) {
  // Canvas 绘制代码 
  }  
  
  area() { 
    return Math.pow(this.radius, 2) * Math.PI; 
  }

   get radius() { 
    return this._radius; 
  } 
  
  set radius(radius) { 
     this._radius = radius; 
  } 
} 
```



# 什么时候用ES2015？



## 浏览器支持情况
[http://kangax.github.io/compat-table/es6/](http://kangax.github.io/compat-table/es6/)



## Babel
* Bable CLI
* Webpack
