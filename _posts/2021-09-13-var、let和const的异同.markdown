---
layout: post
title: "JavaScript中的var、let和const的异同"
date: 2021-09-13 19:50:44
---

​	var、let和const在JavaScript中都是声明变量的关键字，其中let和const是ES6中新增的关键字。虽然这三个关键字都是用来声明变量的，但是它们之间存在一些异同点。

```javascript
var a = 0;
let b = 0;
const c = 0;

a // 0
b // 0
c // 0
```

​	先来看一下它们的相同点。首先是这三者的相同之处，很显然是它们都可以用来声明变量（废话），接下来是三者中两两相同之处，从中也可以看它们之间的不同点。

###### 1.var和let声明的变量都可以重新赋值

```javascript
var a = 0;
let b = 0;
const b = 0;

// 重新赋值
a = 1;
b = 1;
c = 1;

a // 1
b // 1
c // TypeError: Assignment to constant variable.
```

​	可以看出，var和let声明的变量可以修改其中的值，而const声明的变量不可以重新赋值。实际上，const是用来声明常量的，在实际的编程任务中，由于对节省内存空间、进行参数的修改和调整等状况的考虑，我们声明的很多变量是不需要重新赋值的，ES6中const关键字的加入，解决了这些问题。而且const所声明的变量，在其声明的时候必须初始化，不能留到后面的语句里在对其赋值。

```javascript
const a;
// SyntaxError: Missing initializer in const declaration
```

###### 2.let和const都具有块级作用域

​	在ES6之前，JavaScript只存在全局作用域和函数作用域，ES6新增了块级作用域。所谓作用域，指的就是变量和函数可访问的范围，它控制着变量和函数的访问。ES5中，我们在在全局作用域中定义的变量和函数，不论是在函数体外还是函数体内都是可以被访问的，在函数作用域中定义的变量和函数，只能在它被定义的函数的函数体内才能可以被访问。由于ES6以前只有这两种作用域，所以会导致诸如，我们不想让外部访问的变量泄露成了全局变量的问题。例如下面的代码：

```javascript
var arr = [1,2,3]
for(var i = 0; i< arr.length; i++){
    console.log(arr[i]);
    // 1
    // 2
    // 3
}
console.log(i); // 3
```

​	这很显然不是我们所希望看到的，而使用let和const则不会出现这种情况，let和const存在块级作用域，由{ }所包括。

```javascript
var arr = [1,2,3]
for(let i = 0; i< arr.length; i++){
    console.log(arr[i]);
    // 1
    // 2
    // 3
}
console.log(i); // ReferenceError: i is not defined
```

###### 3.let和const都存在暂时性死区

​	暂时性死区在此处指的是这么一种语法现象，就是在块级作用域内使用let或const声明变量之前，使用该变量会报错。因此只能在声明之后使用该变量。

```javascript
if(true){
    a = 0; // ReferenceError: Cannot access 'a' before initialization
    console.log(a); // ReferenceError: Cannot access 'a' before initialization
    let a;
    console.log(a); //undefined
}
```

###### 4.let和const都不存在变量提升

​	使用var声明变量会存在“变量提升”的现象，即变量可以在声明之前使用，而let和const则不可以。

```javascript
console.log(a); // undefined
var a;

console.log(b); // ReferenceError: Cannot access 'b' before initialization
let b;
```

###### 5.let和const不会被添加到全局对象上

​	如果我们使用var声明一个全局变量，它便会被添加到全局对象上，在浏览器环境里会被添加到window对象上，而在Node环境里会被添加到global对象上，而let和const所声明的全局变量不会如此。

```javascript
var a = 1;
let b = 2;
const c = 3;
console.log(window.a,window.b,window.c); // 1 undefined undefined
```

###### 6.let和const不能重复声明变量

​	var可以重复声明变量，而let和const不行。

```javascript
var a = 1; 
var a = 3;
console.log(a); // 3

let b = 1;
let b = 3;
console.log(b); // SyntaxError: Identifier 'b' has already been declared
var a = 3;
console.log(a);

const c = 1
const c = 3;
console.log(c); // SyntaxError: Identifier 'c' has already been declared
```

###### 7.根据上述的比较可以总结出如下的表格：

<img src="/images/var_let_const.png" style="width:40%;height:40%" />
   
