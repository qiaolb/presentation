# 引人的ECMAScript
Joe



# ECMAScript简介



## ECMAScript历史
* 2015年6月17日，ECMAScript 2015发布
* 2009年12月，ECMAScript 5
* 1999年12月，ECMAScript 3
* 1998年06月，ECMAScript 2
* 1997年06月，ECMAScript 1



## ECMAScript简介
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
```
$(“#wumai").html(`
西安雾霾
遛狗不见狗，狗绳提在手，
见绳不见手，狗叫我才走。
`);
```



## const，let
```
const DELAY = 1000;

let count = 0;
count = count + 1;
```
放弃var
块级作用域。



## for循环
