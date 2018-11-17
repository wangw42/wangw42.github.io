---
layout: post
title:  "Learning Advanced JavaScript"
subtitle: "学习笔记"
date:   2018-11-17 16:17:45
categories: [tool]
---

**Reference:** [Learning Advanced JavaScript](https://johnresig.com/apps/learn/)<br>
Courses: Web2.0 Programming.<br>
实用工具参考: [Repl.it](https://repl.it/repls)<br>
学习笔记参考: [blog.zhenly.cn](https://blog.zhenly.cn/Web/web_js_learning/)<br>
JS相关学习网站推荐：[MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript)<br>
**Attention:** <br>
本博客为个人学习笔记，因此比较大部分内容来自他人博客或笔记，大多标明了来源。(有一些没有标的可能也来自于[上面的博客(blog.zhenly.cn)](https://blog.zhenly.cn/Web/web_js_learning/)，是个不错的博客，推荐！［因为后面有点偷懒没有挨着标出处了就在开头大力推荐一哈！也可以直接去看那篇博客，我这里只是做下整理，再添一些自己没能理解的内容，方便自己学习］)

___

### [2: Goal: To be able to understand this function:](#2)
### [3: Some helper methods that we have:](#3)
<br>

### [5: What ways can we define functions?](#5)
### [6: Does the order of function definition matter?](#6)
### [7: Where can assignments be accessed?](#7)
### [8:Can functions be defined below return statements?](#8)
<br>

### [10: We can refer to a function, within itself, by its name.](#10)
### [11: What is the name of a function?](#11)
### [12: We can even do it if we're an anonymous function that's an object property.](#12)
### [13: But what happens when we remove the original object?](#13)
### [14: Let's give the anonymous function a name!](#14)
### [15: What if we don't want to give the function a name?](#15)
<br>

### [17: How similar are functions and objects?](#17)
### [18: How similar are functions and objects?](#18)
### [19: Is it possible to cache the return results from a function?](#19)
### [20: QUIZ: Can you cache the results of this function?](#20)
### [21: One possible way to cache the results:](#21)
<br>

### [23: What happens if a function is an object property?](#23)
### [24: What exactly does context represent?](#24)
### [25: How can we change the context of a function?](#25)
### [26: Different ways of changing the context:](#26)
### [27: QUIZ: How can we implement looping with a callback?](#27)
### [28: A possible solution for function looping:](#28)
<br>

### [30: What does the new operator do?](#30)
### [31: We have a 'this' context that is a Ninja object.](#31)
### [32: QUIZ: Add a method that gives a name to the ninja.](#32)
### [33: Add a new property and method to the object.](#33)
### [34: What happens when we forget to use the new operator?](#34)
### [35: What happens when we forget to use the new operator? (cont.)](#35)
### [36: We need to make sure that the new operator is always used.](#36)
### [37: QUIZ: Is there another, more generic, way of doing this?](#37)
### [38: A solution using arguments.callee.](#38)
<br>

### [40: Using a variable number of arguments to our advantage.](#40)
### [41: How can we find the Min/Max number in an array?](#41)
### [42: Another possible solution:](#42)
### [43: Uh oh, what's going wrong here?](#43)
### [44: QUIZ: We must convert array-like objects into actual arrays. Can any built-in methods help?](#44)
### [45: We can use built-in methods to our advantage.](#45)
### [46: QUIZ: Implement a multiplication function (first argument by largest number).](#46)
### [47: We can use call and apply to build a solution.](#47)
<br>

### [49: A basic closure.](#49)
### [50: But why doesn't this work?](#50)
### [51: Closures are frequently used for callbacks.](#51)
### [52: They're also useful for timers.](#52)
### [53: and they're also frequently used when attaching event listeners.](#53)
### [54: Private properties, using closures.](#54)
### [55: QUIZ: What are the values of the variables?](#55)
### [56: The last one is quite tricky, we'll revisit it.](#56)
<br>

### [58: Self-executing, temporary, function](#58)
### [59: Now we can handle closures and looping.](#59)
### [60: The anonymous wrapper functions are also useful for wrapping libraries.](#60)
### [61: Another way to wrap a library:](#61)
### [62: QUIZ: Fix the broken closures in this loop!](#62)
### [63: A quick wrapper function will do the trick.](#63)
<br>

### [65: Adding a prototyped method to a function.](#65)
### [66: Properties added in the constructor (or later) override prototyped properties.](#66)
### [67: Prototyped properties affect all objects of the same constructor, simultaneously, even if they already exist.](#67)
### [68: QUIZ: Make a chainable Ninja method.](#68)
### [69: The chainable method must return this.](#69)
<br>

### [71: Examining the basics of an object.](#71)
### [72: We can still use the constructor to build other instances.](#72)
### [73: QUIZ: Make another instance of a Ninja.](#73)
### [74: QUIZ: Use the .constructor property to dig in.](#74)
<br>

### [76: The basics of how prototypal inheritance works.](#76)
### [77: QUIZ: Let's try our hand at inheritance.](#77)
### [78: The result is rather straight-forward.](#78)
<br>

### [80: We can also modify built-in object prototypes.](#80)
### [81: Beware: Extending prototypes can be dangerous.](#81)
<br>

### [83: What happens when we try to bind an object's method to a click handler?](#83)
### [84: We need to keep its context as the original object.](#84)
### [85: Add a method to all functions to allow context enforcement.](#85)
### [86: Our final target (the .bind method from Prototype.js).](#86)
<br>

### [88: How does a function's length property work?](#88)
### [89: We can use it to implement method overloading.](#89)
### [90: How method overloading might work, using the function length property.](#90)


___
<h2 id="2">2: Goal: To be able to understand this function:</h2>

```javascript
// The .bind method from Prototype.js 
Function.prototype.bind = function(){ 
  var fn = this, args = Array.prototype.slice.call(arguments), object = args.shift(); 
  return function(){ 
    return fn.apply(object, 
      args.concat(Array.prototype.slice.call(arguments))); 
  }; 
};
```
 上述代码中，
 
**prototype**是函数的一个属性，并且是函数的原型对象。引用它的必然是函数。<br>
**call**是函数的一个方法，关于这个方法，它也是只有函数才能够调用的，它的作用是：调用引用它的函数。<br>
slice(start[,end])是js的一个原生数组函数，作用是获取数组中从start下标开始到end下标结束的元素。<br>
**arguments**是js函数对象的一个属性，作用是获取函数的实参，返回的是一个以函数实参为属性元素的对象。<br>而Array是js中生成数组的关键字，数组的关键字Array不能这样子Array.xx直接调用js的数组函数，而是要用Array.prototype来调用数组函数。(给原型对象增加属性，也就是给对象增加公用的属性）<br>
Array.prototype是一个数组，String.prototype是一个字符串，Object.prototype是一个对象。<br>
[reference.](http://www.cnblogs.com/loveyoume/p/6139681.html)

args=Array.prototype.slice.call(arguments)将调用**bind**函数时参数集合arguments转换为数组array。

object=args.shift()将args数组第一个元素取出作为当前对象

匿名函数中，调用args.concat(Array.prototype.slice.call(arguments))是为了将调用匿名函数时传入的参数与调用bind时参数合并成一个参数数组

以一个调用示例来看上述过程:
```javascript
var obj = { x: 'prop x' };
//args = Array.prototype.slice.call(arguments)后args = [obj, 12, 23 ]
//object=args.shift()后，args =[12, 23] ，object =obj

var boundExample = example.bind(obj, 12, 23); 
boundExample(36, 49); // arguments => 36, 49 ,调用args.concat(Array.prototype.slice.call(arguments))后，arguments that our example() function receives => [12, 23, 36, 49]
```
参考[链接](https://www.cnblogs.com/GongQi/p/4041460.html)


<h2 id="3">3: Some helper methods that we have:</h2>

```javascript
assert( true, "I'll pass." ); //undefined
assert( "truey", "So will I." ); //undefined
assert( false, "I'll fail." ); //{ [AssertionError [ERR_ASSERTION]: I'll fail.]
  //generatedMessage: false,
  //name: 'AssertionError [ERR_ASSERTION]',
  //code: 'ERR_ASSERTION',
  //actual: false,
  //expected: true,
  //operator: '==' }
assert( null, "So will I." ); //{ [AssertionError [ERR_ASSERTION]: So will I.]
  //generatedMessage: false,
  //name: 'AssertionError [ERR_ASSERTION]',
  //code: 'ERR_ASSERTION',
  //actual: null,
  //expected: true,
  //operator: '==' }
log( "Just a simple log", "of", "values.", true ); //ReferenceError: log is not defined
error( "I'm an error!" ); //ReferenceError: error is not defined
// Terminal node v10.13.0
```
判断值是否为真值有以下两个断言测试函数

1. assert(value[, message])
这个测试函数在 【Boolean(value)】 为 【true】时通过断言测试，否则抛出 【AssertionError】。（ value 为false，则抛出一个带有 message 属性的 【AssertionError】，其中 message 属性的值等于传入的 message 参数的值。 如果 message 参数为 undefined，则赋予默认的错误信息。）
2. assert.ok(value[, message])
assert.ok() 与 assert()的作用是一样的，都是测试【value】是否为真值。而且用法也一样，所以可以将assert()视为assert.ok()的语法糖

参考[链接](https://blog.csdn.net/sgs595595/article/details/78633142)


<h2 id="5">5: What ways can we define functions?</h2>

```javascript
function isNimble(){ return true; } 
var canFly = function(){ return true; }; 
window.isDeadly = function(){ return true; }; 
log(isNimble, canFly, isDeadly);
```

<h2 id="6">6: Does the order of function definition matter?</h2>

```javascript
var canFly = function(){ return true; }; 
window.isDeadly = function(){ return true; }; 
assert( isNimble() && canFly() && isDeadly(), "Still works, even though isNimble is moved." ); 
function isNimble(){ return true; }
```
函数可定义在任何地方，次序不重要，javascript在执行之前会将所有的变量和函数进行升级(define promotion)。


<h2 id="7">7: Where can assignments be accessed?</h2>

```javascript
assert( typeof canFly == "undefined", "canFly doesn't get that benefit." ); //[AssertionError [ERR_ASSERTION]: canFly doesn't get that benefit.]
assert( typeof isDeadly == "undefined", "Nor does isDeadly." ); 
var canFly = function(){ return true; }; //undefined
window.isDeadly = function(){ return true; };
```
如果是**赋值方式**定义函数指针的话，必须得在调用该函数指针之前定义，否则将无法访问。在javascript中函数的定义和变量的定义都为提升到global域当中，但变量只有定义会提升，**其值并不提升**，因此你会看到undefined。赋值的命名函数其函数名只在函数内部可以识别出.。

**提升**（Hoisting）是 JavaScript 默认将当前作用域提升到前面去的的行为。

**提升**（Hoisting）应用在变量的声明与函数的声明。
使用**表达式定义函**数时无法提升。

eg. var x = function (a, b) {return a * b}; //表达式声明<br>
JavaScript 函数可以通过一个表达式定义。函数表达式可以存储在变量中；在函数表达式存储在变量后，变量也可作为一个函数使用；实际上是一个匿名函数 (函数没有名称)。函数存储在变量中，不需要函数名称，通常通过变量名来调用。

<h2 id="8">8: Can functions be defined below return statements?</h2>

```javascript
function stealthCheck(){ 
  assert( stealth(), "We'll never get below the return, but that's OK!" ); 
 
  return stealth(); 
 
  function stealth(){ return true; } 
} //undefined
 
stealthCheck();//true
```
stealthCheck函数在执行之前会对所有内部的函数和变量进行升级。

<h2 id="10">10: We can refer to a function, within itself, by its name.</h2>

```javascript
function yell(n){ 
  return n > 0 ? yell(n-1) + "a" : "hiy"; 
} //yell(4)=='hiyaaaa'
assert( yell(4) == "hiyaaaa", "Calling the function by itself comes naturally." ); 
```

<h2 id="11">11: What is the name of a function?</h2>

```javascript
var ninja = function myNinja(){ 
  assert( ninja == myNinja, "This function is named two things - at once!" ); 
};  //undefined
ninja(); //true
//myNinja(); //ReferenceError: myNinja is not defined
assert( typeof myNinja == "undefined", "But myNinja isn't defined outside of the function." ); //true
log( ninja );//console.log(typeof(ninja)): functioin
//typeof myNinja == 'undefined'
```
可以将一个匿名函数做为一个对象的属性<br>
以var fn= function doSth(){}这种形式定义的函数，在全局中只能以fn为名来调用。

<h2 id="12">12: We can even do it if we're an anonymous function that's an object property.</h2>

```javascript
var ninja = { 
  yell: function(n){ 
    return n > 0 ? ninja.yell(n-1) + "a" : "hiy"; 
  } 
}; //ninja.yell(4) == 'hiyaaaa'
assert( ninja.yell(4) == "hiyaaaa", "A single object isn't too bad, either." );
```
可以将一个对象的属性继承给另一个对象。

<h2 id="13">13: But what happens when we remove the original object?</h2>

```javascript
var ninja = { 
  yell: function(n){ 
    return n > 0 ? ninja.yell(n-1) + "a" : "hiy"; 
  } 
}; //ninja.yell(4) == 'hiyaaaa'
assert( ninja.yell(4) == "hiyaaaa", "A single object isn't too bad, either." ); 
 
var samurai = { yell: ninja.yell }; 
var ninja = null; //!! compared with #14
 
try { 
  samurai.yell(4); 
} catch(e){ 
  assert( false, "Uh, this isn't good! Where'd ninja.yell go?" ); //AssertionError [ERR_ASSERTION]
}
```
如果原始对象为空，则不能发生继承。<br>
匿名函数作为对属性时，不会被声明，只在被调用时执行。<br>因而当对应属性被删除时，再调用该函数则无效。<br>

<h2 id="14">14: Let's give the anonymous function a name!</h2>

```javascript
var ninja = { 
  yell: function yell(n){ 
    return n > 0 ? yell(n-1) + "a" : "hiy"; 
  } 
}; 
assert( ninja.yell(4) == "hiyaaaa", "Works as we would expect it to!" ); 
 
var samurai = { yell: ninja.yell }; 
var ninja = {}; //!!!!! not null
assert( samurai.yell(4) == "hiyaaaa", "The method correctly calls itself." ); //samurai.yell(4) == 'hiyaaaa'
```
当属性中的函数具名时,在属性被创建并赋值时，便声明了以属性键名为名的函数。及时属性之后被清空，函数依然存在。

<h2 id="15">15: What if we don't want to give the function a name?</h2>

```javascript
var ninja = { 
  yell: function(n){ 
    return n > 0 ? arguments.callee(n-1) + "a" : "hiy"; 
  } 
}; //ninja.yell(4) == 'hiyaaaa'
assert( ninja.yell(4) == "hiyaaaa", "arguments.callee is the function itself." );
```
*arguments和数组类似但不是数组、它保存着函数调用时传递过来的所有参数、下标从0开始顺序接收。arguments对象不是一个Array、它类似于Array，但不具有除了length方法的任何方法，例如 sort方法、pop方法等 ，但它可以被转换为一个真正的Array。*<br>
**callee**是arguments对象的一个属性、用来指向当前执行的函数。<br>
在匿名函数中，可以用arguments.callee调用函数自身


<h2 id="17">17: How similar are functions and objects?</h2>

```javascript
var obj = {}; 
var fn = function(){}; 
assert( obj && fn, "Both the object and function exist." );
```

>**Function**<br>
函数就是对象,代表函数的对象就是函数对象。所有的函数对象是被 Function 这个函数对象构造出来的。也就是说，Function 是最顶层的构造器。它构造了系统中所有的对象，包括用户自定义对象，系统内置对象，甚至包括它自已。<br>
**Object**<br>
Object 是最顶层的对象，所有的对象都将继承 Object 的原型，你也要知道 Object 也是一个函数对象，所以说 Object 是被 Function 构造出来的。

**Function 与 Object 关系图：**

```javascript
var Foo= function(){}  
var f1 = new Foo();  
console.log(f1.__proto__ === Foo.prototype);  //true
console.log(Foo.prototype.constructor === Foo);  //true
var o1 =new Object();  
console.log(o1.__proto__ === Object.prototype);  //true
console.log(Object.prototype.constructor === Object); //true 
console.log(Foo.prototype.__proto__ === Object.prototype);  //true

//Function and Object  
console.log(Function.__proto__ === Function.prototype);  //true
console.log(Object.__proto__ === Function.prototype);  //true
console.log(Object.prototype.__proto__);  //null
console.log(Object.__proto__ === Function.prototype);  //true
```
[Reference.](http://wiki.jikexueyuan.com/project/brief-talk-js/function-and-object.html)

<h2 id="18">18: How similar are functions and objects?</h2>

```javascript
var obj = {}; 
var fn = function(){}; 
obj.prop = "some value"; 
fn.prop = "some value";  //obj.prop == fn.prop, true
assert( obj.prop == fn.prop, "Both are objects, both have the property." );
```
<h2 id="19">19: Is it possible to cache the return results from a function?</h2>

```javascript
function getElements( name ) { 
  var results; 
 
  if ( getElements.cache[name] ) { 
    results = getElements.cache[name]; 
  } else { 
    results = document.getElementsByTagName(name); 
    getElements.cache[name] = results; 
  } 
 
  return results; 
} 
getElements.cache = {}; 
 
log( "Elements found: ", getElements("pre").length );
log( "Cache found: ", getElements.cache.pre.length );
//Elements found:  0
//Cache found:  0
```
>这里要说的大概是函数是一个对象，因此可以具有各种属性，那么就自然可以把数据保存在自身的属性里面，这里面的cache就是这个函数的其中一个属性。函数把运行结果存储在getElements.cache.pre里面。展示了函数作为对象的优势.

<h2 id="20">20: QUIZ: Can you cache the results of this function?</h2>

```javascript
function isPrime( num ) { 
  var prime = num != 1; // Everything but 1 can be prime 
  for ( var i = 2; i < num; i++ ) { 
    if ( num % i == 0 ) { 
      prime = false; 
      break; 
    } 
  } 
  return prime; 
} 
 
assert( isPrime(5), "Make sure the function works, 5 is prime." ); 
assert( isPrime.cache[5], "Is the answer cached?" );
//isPrime(5) true;
//isPrime.cache[5] TypeError: Cannot read property '5' of undefined
```
这是一道问题，仿照上一题就很容易做出来
```javascript
function isPrime(num) {
  if (isPrime.cache[num]) {
    return isPrime.cache[num];
  } else {
    var prime = num != 1; // Everything but 1 can be prime
    for (var i = 2; i < num; i++) {
      if (num % i == 0) {
        prime = false;
        break;
      }
    }
    isPrime.cache[num] = prime;
    return prime;
  }
}
isPrime.cache = {}; // 要初始化cache，否则访问其子元素会报错
assert(isPrime(5), "Make sure the function works, 5 is prime.");
assert(isPrime.cache[5], "Is the answer cached?");

```

<h2 id="21">21: One possible way to cache the results:</h2>

```javascript
function isPrime( num ) { 
  if ( isPrime.cache[ num ] != null ) 
    return isPrime.cache[ num ];
     //If the parm cached,return corresponding result
   
  var prime = num != 1; // Everything but 1 can be prime 
  for ( var i = 2; i < num; i++ ) { 
    if ( num % i == 0 ) { 
      prime = false; 
      break; 
    } 
  } 
  
  isPrime.cache[ num ] = prime //cached the parm&result
  
  return prime; 
} 
 
isPrime.cache = {}; 
 
assert( isPrime(5), "Make sure the function works, 5 is prime." ); 
assert( isPrime.cache[5], "Make sure the answer is cached." );
//isPrime(5) true;
//isPrime.cache[5] true
```
函数作为一个对象，可以在其子对象中进行数据缓存。(作者给出的quiz的解决方法)

<h2 id="23">23: What happens if a function is an object property?</h2>

```javascript
var katana = { 
  isSharp: true, 
  use: function(){ 
    this.isSharp = !this.isSharp; 
  } 
}; 
katana.use(); 
assert( !katana.isSharp, "Verify the value of isSharp has been changed." );
//!katana.isSharp: true
```
当一个匿名函数作为一个对象的属性的时候，那么this就是指这个对象，函数可以访问并修改对象的属性

 1. Katana is an object (created using the { ... } notation). "use" is the name of the property of the object whose value will be the anonymous function (which is also an object).
2. The function inverts the value of isSharp (so from true to false or false to true).
3. It is asserting that isSharp is something which does not evaluate to true (this is nearly everything except undefined, null, false, 0, etc). In this case, since isSharp is always either true or false, it is asserting that it is false.

The main point (and cool part) of the sample is this line:

    katana.use();

This first fetches the value of the "use" property from the katana object (that's the katana.use part). The value is the anonymous function from before. Then, that function is executed (that's the () part). The really cool part is that it is executed on behalf of the katana object -- that means this in the anonymous function is a reference to the katana object when it's called that way.
>1) Katana is an object. Katana.use is a function. Its a property that contains a function as value. The value it contains happens to be an anonymous function.
The distinction is that Katana.use is a property of Katana and that the value of Katana.use is a function. use is a key defined on Katana since Katana["use"] also works.
>2) It's setting isSharp to NOT isSharp so either true -> false or false -> true
>3) the assert is saying katana.isSharp === false which it should be since it was orginally true but then set to false.

[Reference](https://stackoverrun.com/cn/q/1303771)


<h2 id="24">24: What exactly does context represent?</h2>

```javascript
function katana(){ 
  this.isSharp = true; 
} 
katana(); 
assert( isSharp === true, "A global object now exists with that name and value." ); 
//true
 
var shuriken = { 
  toss: function(){ 
    this.isSharp = true; 
  } 
}; 
shuriken.toss(); 
assert( shuriken.isSharp === true, "When it's an object property, the value is set within the object." );
//true
```
这里想要说的大概是this下绑定的变量是绑定在上一级函数作用域下的。如果是处于Global的函数，那么他的this绑定的就是全局变量。

<h2 id="25">25: How can we change the context of a function?</h2>

```javascript
var object = {}; 
function fn(){ 
  return this; 
} 
assert( fn() == this, "The context is the global object." ); 
//true
assert( fn.call(object) == object, "The context is changed to a specific object." );
//true
```
Function.prototype.call()方法调用一个函数, 其具有一个指定的this值和分别地提供的参数(参数的列表)。
我们可以通过call这个方法来改变一个函数的context.

```javascript
unction Product(name, price) {
  this.name = name;
  this.price = price;
}

function Food(name, price) {
  Product.call(this, name, price);
  this.category = 'food';
}

console.log(new Food('cheese', 5).name);
console.log(new Food('cheese', 5).price);
// "cheese" 5
```

<h2 id="26">26: Different ways of changing the context:</h2>

```javascript
function add(a, b){ 
  return a + b; 
} 
assert( add.call(this, 1, 2) == 3, ".call() takes individual arguments" ); 
//true
assert( add.apply(this, [1, 2]) == 3, ".apply() takes an array of arguments" );
//true
```
**Function.prototype.apply()**<br>
apply() 方法调用一个具有给定this值的函数，以及作为一个数组（或类似数组对象）提供的参数。<br>
语法：`func.apply(thisArg, [argsArray])`<br>
**参数:**<br>
thisArg<br>
可选的。在 func 函数运行时使用的 this 值。请注意，this可能不是该方法看到的实际值：如果这个函数处于非严格模式下，则指定为 null 或 undefined 时会自动替换为指向全局对象，原始值会被包装。<br>
argsArray<br>
可选的。一个数组或者类数组对象，其中的数组元素将作为单独的参数传给 func 函数。如果该参数的值为 null 或  undefined，则表示不需要传入任何参数。
**返回值:**<br>
调用有指定this值和参数的函数的结果。<br>
>**注意**：call()方法的作用和 apply() 方法类似，区别就是call()方法接受的是参数列表，而apply()方法接受的是一个参数数组。

```javascript
var numbers = [5, 6, 2, 3, 7];

var max = Math.max.apply(null, numbers);

console.log(max);
// 7

var min = Math.min.apply(null, numbers);

console.log(min);
// 2
```
[Reference: MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)

<h2 id="27">27: QUIZ: How can we implement looping with a callback?</h2>

```javascript
function loop(array, fn){ 
  for ( var i = 0; i < array.length; i++ ) { 
    // Implement me! 
  } 
} 
var num = 0; 
loop([0, 1, 2], function(value){ 
  assert(value == num++, "Make sure the contents are as we expect it."); 
  assert(this instanceof Array, "The context should be the full array."); 
});
```
填入：
```
fn.call(array, array[i]);
```

<h2 id="28">28: A possible solution for function looping:</h2>

```javascript
function loop(array, fn){ 
  for ( var i = 0; i < array.length; i++ ) 
    fn.call( array, array[i], i ); 
} 
var num = 0; 
loop([0, 1, 2], function(value, i){ 
  assert(value == num++, "Make sure the contents are as we expect it."); 
  assert(this instanceof Array, "The context should be the full array."); 
});
```
<h2 id="30">30: What does the new operator do?</h2>

```javascript
function Ninja(){ 
  this.name = "Ninja"; 
} 
 
var ninjaA = Ninja(); 
assert( !ninjaA, "Is undefined, not an instance of Ninja." ); 
 
var ninjaB = new Ninja(); 
assert( ninjaB.name == "Ninja", "Property exists on the ninja instance." );
```
new 运算符创建一个用户定义的对象类型的实例或具有构造函数的内置对象的实例。<br>
**语法**: `new constructor[([arguments])]`<br>
*constructor*<br>
一个指定对象实例的类型的类或函数。<br>
*arguments*<br>
一个用来被constructor 调用的参数列表。<br>

>**描述：**
创建一个用户自定义的对象需要两步：
>1. 通过编写函数来定义对象类型。
>2. 通过new来创建对象实例。

>创建一个对象类型，需要创建一个指定其名称和属性的函数；对象的属性可以指向其他对象，看下面的例子：
当代码 new Foo(...) 执行时，会发生以下事情：
(1) 一个继承自 Foo.prototype 的新对象被创建。<br>
(2) 使用指定的参数调用构造函数 Foo ，并将 this 绑定到新创建的对象。new Foo 等同于 new Foo()，也就是没有指定参数列表，Foo 不带任何参数调用的情况。<br>
(3) 由构造函数返回的对象就是 new 表达式的结果。如果构造函数没有显式返回一个对象，则使用步骤1创建的对象。（一般情况下，构造函数不返回值，但是用户可以选择主动返回对象，来覆盖正常的对象创建步骤）<br><br>	
你始终可以对已定义的对象添加新的属性。<br>
例如， car1.color = "black" 语句给 car1 添加了一个新的属性 color ， 并给这个属性赋值 "black"。但是，这不会影响任何其他对象。要将新属性添加到相同类型的所有对象，你必须将该属性添加到Car对象类型的定义中。<br>
你可以使用 Function.prototype 属性将共享属性添加到以前定义的对象类型。这定义了一个由该函数创建的所有对象共享的属性，而不仅仅是对象类型的其中一个实例。下面的代码将一个值为null的color属性添加到car类型的所有对象，然后仅在实例对象car1中用字符串“black”覆盖该值。详见 prototype。

```javascript
    function Car() {}
    car1 = new Car()
    
    console.log(car1.color)           // undefined
    
    Car.prototype.color = null
    console.log(car1.color)           // null
    
    car1.color = "black"
    console.log(car1.color)           // black
```
顺便说一下，一个对象被实例化之后，我们仍然可以通过修改Ninja.prototype给所有之前定义的实例来添加属性。如果之前的实例已经拥有这个属性了，那么将无法覆盖。产生这种结果是因为JavaScript基于原型的继承设计。[参考资料](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)

<h2 id="31">31: We have a 'this' context that is a Ninja object.</h2>

```javascript
function Ninja(){ 
  this.swung = false; 
   
  // Should return true 
  this.swingSword = function(){ 
    this.swung = !this.swung; 
    return this.swung; 
  }; 
} 
 
var ninja = new Ninja(); 
assert( ninja.swingSword(), "Calling the instance method." ); 
//true
assert( ninja.swung, "The ninja has swung the sword." ); 
//true
 
var ninjaB = new Ninja(); 
assert( !ninjaB.swung, "Make sure that the ninja has not swung his sword." );
//true 
//ninjaB not swingSword()
//var ninjaB = new Ninja(); 
//console.log( ninjaB.swingSword()); //true
//console.log( !ninjaB.swung); //false
```

<h2 id="32">32: QUIZ: Add a method that gives a name to the ninja.</h2>

```javascript
function Ninja(name){ 
  // Implement! 
} 
 
var ninja = new Ninja("John"); 
assert( ninja.name == "John", "The name has been set on initialization" ); 
 
ninja.changeName("Bob"); 
assert( ninja.name == "Bob", "The name was successfully changed." );
```
Implement:

    this.name = name;
    this.changeName = function(name2){
    	this.name = name2;
    }


<h2 id="33">33: Add a new property and method to the object.</h2>

```javascript
function Ninja(name){
  this.changeName = function(name){
    this.name = name;
  };

  this.changeName( name );
}

var ninja = new Ninja("John");
assert( ninja.name == "John", "The name has been set on initialization" );

ninja.changeName("Bob");
assert( ninja.name == "Bob", "The name was successfully changed." );
```

<h2 id="34">34: What happens when we forget to use the new operator?</h2>

```javascript
function User(first, last){ 
  this.name = first + " " + last; 
} 
 
var user = User("John", "Resig"); 
assert( typeof user == "undefined", "Since new wasn't used, the instance is undefined." );
//true
```
当我们没有使用new的时候，this没办法指定在返回的对象里面，而是函数所在的作用域。

<h2 id="35">35: What happens when we forget to use the new operator? (cont.)</h2>


```javascript
function User(first, last){ 
  this.name = first + " " + last; 
} 
 
window.name = "Resig"; 
var user = User("John", name); 
 
assert( name == "John Resig", "The name variable is accidentally overridden." );
//true 
```
<h2 id="36">36: We need to make sure that the new operator is always used.</h2>

```javascript
function User(first, last){ 
  if ( !(this instanceof User) ) // 判断当前上下文是否在User中
    return new User(first, last); 
   
  this.name = first + " " + last; 
} 
 
var name = "Resig"; 
var user = User("John", name); 
 
assert( user, "This was defined correctly, even if it was by mistake." ); 
//User { name: 'John Resig' }
assert( name == "Resig", "The right name was maintained." );
//true
```
**instanceof**运算符用于测试构造函数的prototype属性是否出现在对象的原型链中的任何位置. 
```javascript
function Car(make, model, year) {
  this.make = make;
  this.model = model;
  this.year = year;
}
var auto = new Car('Honda', 'Accord', 1998);

console.log(auto instanceof Car);
// true

console.log(auto instanceof Object);
// true

```
**语法**

    object instanceof constructor

**参数**<br>
**object:** 要检测的对象.<br>
**constructor:** 某个构造函数<br>
[Reference.](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/instanceof)

<h2 id="37">37: QUIZ: Is there another, more generic, way of doing this?</h2>

```javascript
function User(first, last){ 
  if ( !(this instanceof ___) ) 
    return new User(first, last); 
   
  this.name = first + " " + last; 
} 
 
var name = "Resig"; 
var user = User("John", name); 
 
assert( user, "This was defined correctly, even if it was by mistake." ); 
assert( name == "Resig", "The right name was maintained." );
```

<h2 id="38">38: A solution using arguments.callee.</h2>

```javascript
function User(first, last){ 
  if ( !(this instanceof arguments.callee) ) 
    return new User(first, last); 
   
  this.name = first + " " + last; 
} 
 
var name = "Resig"; 
var user = User("John", name); 
 
assert( user, "This was defined correctly, even if it was by mistake." ); 
assert( name == "Resig", "The right name was maintained." );
```
callee 在函数的名称未知时很有用.
但是在严格模式下，ES5是禁止使用arguments.callee的。

<h2 id="40">40: Using a variable number of arguments to our advantage.</h2>

```javascript
function merge(root){ 
  for ( var i = 1; i < arguments.length; i++ ) 
    for ( var key in arguments[i] ) 
      root[key] = arguments[i][key]; 
  return root; 
} 
 
var merged = merge({name: "John"}, {city: "Boston"}); 
assert( merged.name == "John", "The original name is intact." ); 
//true
assert( merged.city == "Boston", "And the city has been copied over." );
//true
```
for in: key<br>
for of: value<br>
**arguments** is an Array-like object accessible inside functions that contains the values of the arguments passed to that function.

<h2 id="41">41: How can we find the Min/Max number in an array?</h2>

```javascript
function smallest(array){ 
  return Math.min.apply( Math, array ); 
} 
function largest(array){ 
  return Math.max.apply( Math, array ); 
} 
assert(smallest([0, 1, 2, 3]) == 0, "Locate the smallest value."); 
assert(largest([0, 1, 2, 3]) == 3, "Locate the largest value.");
```
The static function **Math.min()** returns the lowest-valued number passed into it, or NaN if any parameter isn't a number and can't be converted into one.<br>
**Syntax**: Math.min([value1[, value2[, ...]]]) <br>
！！不接受数组参数

<h2 id="42">42: Another possible solution:</h2>

```javascript
function smallest(){ 
  return Math.min.apply( Math, arguments ); 
} 
function largest(){ 
  return Math.max.apply( Math, arguments ); 
} 
assert(smallest(0, 1, 2, 3) == 0, "Locate the smallest value."); 
assert(largest(0, 1, 2, 3) == 3, "Locate the largest value.");
```

<h2 id="43">43: Uh oh, what's going wrong here?</h2>

```javascript
function highest(){ 
  return arguments.sort(function(a,b){ 
    return b - a; 
  }); 
} 
assert(highest(1, 1, 2, 3)[0] == 3, "Get the highest value."); 
assert(highest(3, 1, 2, 3, 4, 5)[1] == 4, "Verify the results.");
```
arguments 并不是数组，是**类数组**。<br>
**arr.sort([compareFunction])**，sort() 方法用原地算法对数组的元素进行排序，并返回数组。排序不一定是稳定的。默认排序顺序是根据字符串Unicode码点。

**类数组ArrayLike**
* 拥有length属性，其它属性（索引）为非负整数(对象中的索引会被当做字符串来处理，这里你可以当做是个非负整数串来理解)。
* 不具有数组所具有的方法。

javascript中常见的类数组有arguments对象和DOM方法的返回结果。<br>
比如 document.getElementsByTagName()。<br>
**Array.prototype.slice.call(arrayLike)** 的结果是将arrayLike对象转换成一个Array对象。<br>
**Array.from()** 方法从一个类似数组或可迭代对象中创建一个新的数组实例。第二个参数指定map函数，第三个参数指定context。<br>
* **语法**：<br>
**Array.from(arrayLike[, mapFn[, thisArg]])**<br>
arrayLike：想要转换成数组的伪数组对象或可迭代对象。
mapFn (可选参数)：如果指定了该参数，新数组中的每个元素会执行该回调函数。<br>
thisArg (可选参数)：可选参数，执行回调函数 mapFn 时 this 对象。<br>

改写：
```javascript
function highest(){ 
  return Array.prototype.slice.call(arguments).sort(function(a,b){ 
    return b - a; 
  }); 
} 
console.log(highest(1, 1, 2, 3)[0] ); 
// 3
console.log(highest(3, 1, 2, 3, 4, 5)[1] );
// 4
```

<h2 id="44">44: QUIZ: We must convert array-like objects into actual arrays. Can any built-in methods help?</h2>

```javascript
// Hint: Arrays have .slice and .splice methods which return new arrays. 
function highest(){ 
  return makeArray(arguments).slice(1).sort(function(a,b){ 
    return b - a; 
  }); 
} 
 
function makeArray(array){ 
  // Implement me! 
} 
 
// Expecting: [3,2,1] 
assert(highest(1, 1, 2, 3)[0] == 3, "Get the highest value."); 
// Expecting: [5,4,3,2,1] 
assert(highest(3, 1, 2, 3, 4, 5)[1] == 4, "Verify the results.");
```

    return Array.from(array);

<h2 id="45">45: We can use built-in methods to our advantage.</h2>

```javascript
function highest(){ 
  return makeArray(arguments).sort(function(a,b){ 
    return b - a; 
  }); 
} 
 
function makeArray(array){ 
  return Array().slice.call( array ); 
} 
 
assert(highest(1, 1, 2, 3)[0] == 3, "Get the highest value."); 
assert(highest(3, 1, 2, 3, 4, 5)[1] == 4, "Verify the results.");
```
<h2 id="46">46: QUIZ: Implement a multiplication function (first argument by largest number).</h2>

```javascript
function multiMax(multi){ 
  // Make an array of all but the first argument 
  var allButFirst = ___; 
 
  // Find the largest number in that array of arguments 
  var largestAllButFirst = ___; 
 
  // Return the multiplied result 
  return multi * largestAllButFirst; 
} 
assert( multiMax(3, 1, 2, 3) == 9, "3*3=9 (First arg, by largest.)" );
```
[Reference](https://blog.zhenly.cn/Web/web_js_learning/)
```javascript
function multiMax(multi){
  // Make an array of all but the first argument
  var allButFirst = Array.from(arguments).slice(1);

  // Find the largest number in that array of arguments
  var largestAllButFirst = allButFirst.sort().pop();
  
  // Return the multiplied result
  return multi * largestAllButFirst;
}
assert( multiMax(3, 1, 2, 3) == 9, "3*3=9 (First arg, by largest.)" );
```
**pop()** 方法用于删除数组的最后一个元素并返回删除的元素。<br>
**注意**：此方法改变数组的长度！<br>
**提示：** 移除数组第一个元素，请使用 shift() 方法。<br>
**shift()** 方法用于把数组的第一个元素从其中删除，并返回第一个元素的值。<br>
**sort():** 默认升序。<br>

<h2 id="47">47: We can use call and apply to build a solution.</h2>

```javascript
function multiMax(multi){ 
  // Make an array of all but the first argument 
  var allButFirst = Array().slice.call( arguments, 1 ); 
 
  // Find the largest number in that array of arguments 
  var largestAllButFirst = Math.max.apply( Math, allButFirst ); 
 
  // Return the multiplied result 
  return multi * largestAllButFirst; 
} 
assert( multiMax(3, 1, 2, 3) == 9, "3*3=9 (First arg, by largest.)" );
```

<h2 id="49">49: A basic closure.</h2>

```javascript
var num = 10; 
 
function addNum(myNum){ 
  return num + myNum; 
} 
 
assert( addNum(5) == 15, "Add two numbers together, one from a closure." );
```
JavaScript中的函数会形成闭包。 闭包是由函数以及创建该函数的词法环境组合而成。**这个环境包含了这个闭包创建时所能访问的所有局部变量**。

<h2 id="50">50: But why doesn't this work?</h2>

```javascript
var num = 10; 
 
function addNum(myNum){ 
  return num + myNum; 
} 
 
num = 15; 
 
assert( addNum(5) == 15, "Add two numbers together, one from a closure." );
```
num  = 15；<br>
addNum(5) == 20


<h2 id="51">51: Closures are frequently used for callbacks.</h2>

```javascript
var results = jQuery("#results").html("<li>Loading...</li>"); 
 
jQuery.get("test.html", function(html){ 
  results.html( html ); 
  assert( results, "The element to append to, via a closure." ); 
});

```
callbacks: 回调函数

<h2 id="52">52: They're also useful for timers.</h2>

```javascript
var count = 0; 
 
var timer = setInterval(function(){ 
  if ( count < 5 ) { 
    log( "Timer call: ", count ); 
    count++; 
  } else { 
    assert( count == 5, "Count came via a closure, accessed each step." ); 
    assert( timer, "The timer reference is also via a closure." ); 
    clearInterval( timer ); 
  } 
}, 100);
```

<h2 id="53">53: and they're also frequently used when attaching event listeners.</h2>

```javascript
var count = 1; 
var elem = document.createElement("li"); 
elem.innerHTML = "Click me!"; 
elem.onclick = function(){ 
  log( "Click #", count++ ); 
}; //closure
document.getElementById("results").appendChild( elem ); 
assert( elem.parentNode, "Clickable element appended." );
```

<h2 id="54">54: Private properties, using closures.</h2>

```javascript
function Ninja(){ 
  var slices = 0; 
   
  this.getSlices = function(){ 
    return slices; 
  }; 
  this.slice = function(){ 
    slices++; 
  }; 
} 
 
var ninja = new Ninja(); 
ninja.slice(); //slices++
assert( ninja.getSlices() == 1, "We're able to access the internal slice data." ); 
//true
assert( ninja.slices === undefined, "And the private data is inaccessible to us." );
//true
```
闭包一般使用的是私有属性，从外部并不能访问。

<h2 id="55">55: QUIZ: What are the values of the variables?</h2>

```javascript
var a = 5; 
function runMe(a){ 
 assert( a == ___, "Check the value of a." ); 
 
 function innerRun(){ 
   assert( b == ___, "Check the value of b." ); 
   assert( c == ___, "Check the value of c." ); 
 } 
 
 var b = 7; 
 innerRun(); 
 var c = 8; 
} 
runMe(6); 
 
for ( var d = 0; d < 3; d++ ) { 
 setTimeout(function(){ 
   assert( d == ___, "Check the value of d." ); 
 }, 100); 
}
```

<h2 id="56">56: The last one is quite tricky, we'll revisit it.</h2>

```javascript
var a = 5; 
function runMe(a){ 
 assert( a == 6, "Check the value of a." ); 
 // 这时传入的变量明显在作用链上比全局变量先找到，因此是6
 
 function innerRun(){ 
   assert( b == 7, "Check the value of b." ); 
   //在调用这个函数的时候，b已经等于7了
   assert( c == undefined, "Check the value of c." ); 
   //在调用函数之前，c并没有定义，由于变量提升但赋值不提升，因此为undefined
 } 
 
 var b = 7; 
 innerRun(); //innerRun在c之前
 var c = 8; 
} 
runMe(6); 
 
for ( var d = 0; d < 3; d++ ) { 
 setTimeout(function(){ 
   assert( d == 3, "Check the value of d." ); 
   //当函数被调用的时候，d已经是等于3了，因此3次调用都是为3
 }, 100); 
}
```
```javascript
for ( var d = 0; d < 3; d++ ) { 
  	console.log(d);
 	setTimeout(function(){ 
  	console.log( d); 
   //当函数被调用的时候，d已经是等于3了，因此3次调用都是为3
 }, 100); 
	(function(){
    	console.log(d);
 	})();
}
// 0 0 1 1 2 2 undefined 3 3 3 
```

<h2 id="58">58: Self-executing, temporary, function</h2>

```javascript
(function(){ 
  var count = 0; 
 
  var timer = setInterval(function(){ 
    if ( count < 5 ) { 
      log( "Timer call: ", count ); 
      count++; 
    } else { 
      assert( count == 5, "Count came via a closure, accessed each step." ); 
      assert( timer, "The timer reference is also via a closure." ); 
      clearInterval( timer ); 
    } 
  }, 100); 
})(); 
 
assert( typeof count == "undefined", "count doesn't exist outside the wrapper" ); 
assert( typeof timer == "undefined", "neither does timer" );
```
这里涉及到变量的作用域范围，由于var定义的变量是在当前函数作用域是有效的（ES6中的let是块级作用域）因此离开了这个函数，外部就无法访问了。

<h2 id="59">59: Now we can handle closures and looping.</h2>

```javascript
for ( var d = 0; d < 3; d++ ) (function(d){ 
 setTimeout(function(){ 
   log( "Value of d: ", d ); 
   assert( d == d, "Check the value of d." ); 
 }, d * 200); 
})(d);
//d: 0 1 2
```
这个和上面的#55形成了一个对比，这个通过函数闭包将d的作用域限定在里面，因此这里有三个函数，每个函数中的d都是不同的，通过参数传进去的。因此在各自的函数定义域中各不影响，输出了1、2、3

<h2 id="60">60: The anonymous wrapper functions are also useful for wrapping libraries.</h2>

```javascript
(function(){ 
  var myLib = window.myLib = function(){ 
    // Initialize 
  }; 
 
  // ... 
})();
```
这是一个封装库的方法，就是通过匿名包装器函数。只把接口暴露出去，其他的变量都保留在里面。

<h2 id="61">61: Another way to wrap a library:</h2>


```javascript
var myLib = (function(){ 
  function myLib(){ 
    // Initialize 
  } 
 
  // ... 
   
  return myLib; 
})();
```
这里通过return封装库，和上面的功能也是一样的。并没有上面特别的操作。

<h2 id="62">62: QUIZ: Fix the broken closures in this loop!</h2>


```javascript
var count = 0; 
for ( var i = 0; i < 4; i++ ) { 
  setTimeout(function(){ 
    assert( i == count++, "Check the value of i." ); 
  }, i * 200); 
}
```
[Reference](https://blog.zhenly.cn/Web/web_js_learning/)
>他提出了一个问题，如何用闭包解决这个问题，也很容易解决，只要把i定义分别在不同函数作用域里面就好，下面是我的解决方法。直接把i作为参数传入进去，由于setTimeout的运行方式，会提前把参数传了进去，形成了闭包。
```javascript
var count = 0;
for ( var i = 0; i < 4; i++ ) {
  setTimeout(function(i){
    assert( i == count++, "Check the value of i." );
  }, i * 200, i);
}
```
<h2 id="63">63: A quick wrapper function will do the trick.</h2>

```javascript
var count = 0; 
for ( var i = 0; i < 4; i++ ) (function(i){ 
  setTimeout(function(){ 
    assert( i == count++, "Check the value of i." ); 
  }, i * 200); 
})(i);
```
他的解决方案是在setTimeout外面用一个立刻执行的函数

<h2 id="65">65: Adding a prototyped method to a function.</h2>

```javascript
function Ninja(){} 
 
Ninja.prototype.swingSword = function(){ 
  return true; 
}; 
 
var ninjaA = Ninja(); 
assert( !ninjaA, "Is undefined, not an instance of Ninja." ); 
 
var ninjaB = new Ninja(); 
assert( ninjaB.swingSword(), "Method exists and is callable." );
```
>这里首先定义了一个Ninja的函数，然后通过prototype向这个对象添加了一个方法。
然后第一次不使用new直接赋值，由于函数并没有返回任何东西，因此ninjaA自然是未定义的undefined，下面用了new返回了一个对象，具体的原因可以看上一篇博客中关于new的运行方式的解释。

<h2 id="66">66: Properties added in the constructor (or later) override prototyped properties.</h2>

```javascript
function Ninja(){ 
  this.swingSword = function(){ 
    return true; 
  }; 
} 
 
// Should return false, but will be overridden 
Ninja.prototype.swingSword = function(){ 
  return false; 
}; 
 
var ninja = new Ninja(); 
assert( ninja.swingSword(), "Calling the instance method, not the prototype method." );
//true
```
>这里看上去有点玄学，为什么明明重写了但是还是return true呢。其实这只是一个错觉。实际上是里面的重写了外面的属性。<br>
让我们来分析一下他的过程。<br>
首先，定义了一个叫做Ninja的构造函数。在这个构造函数里面为自己添加了一个swingSword的方法。但是注意，这个构造函数并没有被执行。<br>
然后，为Ninja这个对象添加了一个swingSword的方法，这是这个方法第一次被添加到这个对象里面，return的是false<br>
再接着，用new来实例化。根据new的运行过程，此时上面定义的构造函数才被调用，重写了swingSword这个方法，这时候，return的自然就是true了。<br>
这样一看，是不是清晰明了了。<br>

<h2 id="67">67: Prototyped properties affect all objects of the same constructor, simultaneously, even if they already exist.</h2>

```javascript
function Ninja(){ 
  this.swung = true; 
} 
 
var ninjaA = new Ninja(); 
var ninjaB = new Ninja(); 
 
Ninja.prototype.swingSword = function(){ 
  return this.swung; 
}; 
 
assert( ninjaA.swingSword(), "Method exists, even out of order." ); 
assert( ninjaB.swingSword(), "and on all instantiated objects." );
```
>这个标题所表达的意思很简单，就是通过prototype添加的属性，是会被添加到所有已经实例化的对象里面的。由于原型链继承的设计，他们是可以顺着原型链找到这个方法的。

<h2 id="68">68: QUIZ: Make a chainable Ninja method.</h2>

```javascript
function Ninja(){ 
  this.swung = true; 
} 
 
var ninjaA = new Ninja(); 
var ninjaB = new Ninja(); 
 
// Add a method to the Ninja prototype which 
// returns itself and modifies swung 
 
assert( !ninjaA.swing().swung, "Verify that the swing method exists and returns an instance." ); 
assert( !ninjaB.swing().swung, "and that it works on all Ninja instances." );
```

<h2 id="69">69: The chainable method must return this.</h2>

```javascript
function Ninja(){ 
  this.swung = true; 
} 
 
var ninjaA = new Ninja(); 
var ninjaB = new Ninja(); 
 
Ninja.prototype.swing = function(){ 
  this.swung = false; 
  return this; 
}; 
 
assert( !ninjaA.swing().swung, "Verify that the swing method exists and returns an instance." ); 
assert( !ninjaB.swing().swung, "and that it works on all Ninja instances." );
```

<h2 id="71">71: Examining the basics of an object.</h2>

```javascript
function Ninja(){} 
 
var ninja = new Ninja(); 
 
assert( typeof ninja == "object", "However the type of the instance is still an object." );   
assert( ninja instanceof Ninja, "The object was instantiated properly." ); 
assert( ninja.constructor == Ninja, "The ninja object was created by the Ninja function." );
```
（instanceof的相关内容上面提到过。）

<h2 id="72">72: We can still use the constructor to build other instances.</h2>


```javascript
function Ninja(){} 
var ninja = new Ninja(); 
var ninjaB = new ninja.constructor(); 
 
assert( ninjaB instanceof Ninja, "Still a ninja object." );
```

<h2 id="73">73: QUIZ: Make another instance of a Ninja.</h2>

```javascript
var ninja = (function(){ 
 function Ninja(){} 
 return new Ninja(); 
})(); 
 
// Make another instance of Ninja 
var ninjaB = ___; //new. ninja.constructor()
 
assert( ninja.constructor == ninjaB.constructor, "The ninjas come from the same source." );
```

<h2 id="74">74: QUIZ: Use the .constructor property to dig in.</h2>

```javascript
var ninja = (function(){ 
 function Ninja(){} 
 return new Ninja(); 
})(); 
 
// Make another instance of Ninja 
var ninjaB = new ninja.constructor(); 
 
assert( ninja.constructor == ninjaB.constructor, "The ninjas come from the same source." );
```

<h2 id="76">76: The basics of how prototypal inheritance works.</h2>

```javascript
function Person(){} 
Person.prototype.dance = function(){}; 
 
function Ninja(){} 
 
// Achieve similar, but non-inheritable, results 
Ninja.prototype = Person.prototype;  // Ninja继承于Person
Ninja.prototype = { dance: Person.prototype.dance }; 
 // 这破坏了继承链，如果去掉那么下面就可以通过
 
assert( (new Ninja()) instanceof Person, "Will fail with bad prototype chain." ); 
 
// Only this maintains the prototype chain 
Ninja.prototype = new Person(); 
 
var ninja = new Ninja(); 
assert( ninja instanceof Ninja, "ninja receives functionality from the Ninja prototype" ); 
assert( ninja instanceof Person, "... and the Person prototype" ); 
assert( ninja instanceof Object, "... and the Object prototype" );
//都继承于object
```

<h2 id="77">77: QUIZ: Let's try our hand at inheritance.</h2>

```javascript
function Person(){} 
Person.prototype.getName = function(){ 
  return this.name; 
}; 
 
// Implement a function that inherits from Person 
// and sets a name in the constructor 
 
var me = new Me(); 
assert( me.getName(), "A name was set." );
```

<h2 id="78">78: The result is rather straight-forward.</h2>

```javascript
function Person(){} 
Person.prototype.getName = function(){ 
  return this.name; 
}; 
 
function Me(){ 
  this.name = "John Resig"; 
} 
Me.prototype = new Person(); 
 
var me = new Me(); 
assert( me.getName(), "A name was set." );
```

<h2 id="80">80: We can also modify built-in object prototypes.</h2>

```javascript
if (!Array.prototype.forEach) { 
  Array.prototype.forEach = function(fn){ 
    for ( var i = 0; i < this.length; i++ ) { 
      fn( this[i], i, this ); 
    } 
  }; 
} 
 
["a", "b", "c"].forEach(function(value, index, array){ 
  assert( value, "Is in position " + index + " out of " + (array.length - 1) ); 
});
```
（built-in 内置）
可以修改内置对象的原型。

<h2 id="81">81: Beware: Extending prototypes can be dangerous.</h2>


```javascript
Object.prototype.keys = function(){ 
  var keys = []; 
  for ( var i in this ) 
    keys.push( i ); 
  return keys; 
}; 
 
var obj = { a: 1, b: 2, c: 3 }; 
 
assert( obj.keys().length == 3, "We should only have 3 properties." ); 
 
delete Object.prototype.keys;
```
>上面一个提到我们可以修改原生库里面的原型，但是也是一种**危险**的做法。<br>
比如在这里，他为Object添加了一个keys的方法。然后使用for…in 遍历this的所有属性，这时候this上多了一个keys的属性，那么他的length自然就变成了4，并不是我们想要的结果。

<h2 id="83">83: What happens when we try to bind an object's method to a click handler?</h2>

```javascript
var Button = { 
  click: function(){ 
    this.clicked = true; 
  } 
}; 
 
var elem = document.createElement("li"); 
elem.innerHTML = "Click me!"; 
elem.onclick = Button.click; 
document.getElementById("results").appendChild(elem); 
 
elem.onclick(); 
assert( elem.clicked, "The clicked property was accidentally set on the element" );
```
>这里进行了一些常规操作。简单来说就是建立一个Button对象，里面有个click事件，然后把这个事件绑定到新建的元素里面，然后调用一下，然后elem作为this，那个clicked就变成了true了.


<h2 id="84">84: We need to keep its context as the original object.</h2>

```javascript
function bind(context, name){ 
  return function(){ 
    return context[name].apply(context, arguments); 
  }; 
} 
 
var Button = { 
  click: function(){ 
    this.clicked = true; 
  } 
}; 
 
var elem = document.createElement("li"); 
elem.innerHTML = "Click me!"; 
elem.onclick = bind(Button, "click"); 
document.getElementById("results").appendChild(elem); 
 
elem.onclick(); 
assert( Button.clicked, "The clicked property was correctly set on the object" );
```
>这里和上面有点不同，这里把context绑定在Button这个对象里面，因此我们虽然调用的是elem的onclick事件，但是事件执行的上下文是在Button里面的。也属于常规操作。

<h2 id="85">85: Add a method to all functions to allow context enforcement.</h2>


```javascript
Function.prototype.bind = function(object){ 
  var fn = this; 
  return function(){ 
    return fn.apply(object, arguments); 
  }; 
}; 
 
var Button = { 
  click: function(){ 
    this.clicked = true; 
  } 
}; 
 
var elem = document.createElement("li"); 
elem.innerHTML = "Click me!"; 
elem.onclick = Button.click.bind(Button); 
document.getElementById("results").appendChild(elem); 
 
elem.onclick(); 
assert( Button.clicked, "The clicked property was correctly set on the object" );
```
>这里和上面不同的是把bind放在了Function的原型里面（虽然标准库里面本身就有了），然后我们就可以更加优雅地绑定事件运行时的上下文。挺好的，其他细节部分和上面都是一样的。

<h2 id="86">86: Our final target (the .bind method from Prototype.js).</h2>

```javascript
Function.prototype.bind = function(){ 
  var fn = this, args = Array.prototype.slice.call(arguments), object = args.shift(); 
  return function(){ 
    return fn.apply(object, 
      args.concat(Array.prototype.slice.call(arguments))); 
  }; 
}; 
 
var Button = { 
  click: function(value){ 
    this.clicked = value; 
  } 
}; 
 
var elem = document.createElement("li"); 
elem.innerHTML = "Click me!"; 
elem.onclick = Button.click.bind(Button, false); 
document.getElementById("results").appendChild(elem); 
 
elem.onclick(); 
assert( Button.clicked === false, "The clicked property was correctly set on the object" );
```

<h2 id="88">88: How does a function's length property work?</h2>

```javascript
function makeNinja(name){} 
function makeSamurai(name, rank){} 
assert( makeNinja.length == 1, "Only expecting a single argument" ); 
assert( makeSamurai.length == 2, "Multiple arguments expected" );
```
>这里告诉我们，一个函数具有一个length的属性，而这个属性的值就是等于参数列表的个数。

<h2 id="89">89: We can use it to implement method overloading.</h2>


```javascript
function addMethod(object, name, fn){ 
  // Save a reference to the old method 
  var old = object[ name ]; 
 
  // Overwrite the method with our new one 
  object[ name ] = function(){ 
    // Check the number of incoming arguments, 
    // compared to our overloaded function 
    if ( fn.length == arguments.length ) 
      // If there was a match, run the function 
      return fn.apply( this, arguments ); 
 
    // Otherwise, fallback to the old method 
    else if ( typeof old === "function" ) 
      return old.apply( this, arguments ); 
  }; 
}
```
>先给对象添加一个方法，通过判断函数参数的长度，决定调用的是新加入的方法还是之前的老方法，这样可以解决掉一些添加新功能后的兼容性问题。

<h2 id="90">90: How method overloading might work, using the function length property.</h2>

```javascript
function addMethod(object, name, fn){ 
  // Save a reference to the old method 
  var old = object[ name ]; 
 
  // Overwrite the method with our new one 
  object[ name ] = function(){ 
    // Check the number of incoming arguments, 
    // compared to our overloaded function 
    if ( fn.length == arguments.length ) 
      // If there was a match, run the function 
      return fn.apply( this, arguments ); 
 
    // Otherwise, fallback to the old method 
    else if ( typeof old === "function" ) 
      return old.apply( this, arguments ); 
  }; 
} 
 
function Ninjas(){ 
  var ninjas = [ "Dean Edwards", "Sam Stephenson", "Alex Russell" ]; 
  addMethod(this, "find", function(){ 
    return ninjas; 
  }); 
  addMethod(this, "find", function(name){ 
    var ret = []; 
    for ( var i = 0; i < ninjas.length; i++ ) 
      if ( ninjas[i].indexOf(name) == 0 ) 
        ret.push( ninjas[i] ); 
    return ret; 
  }); 
  addMethod(this, "find", function(first, last){ 
    var ret = []; 
    for ( var i = 0; i < ninjas.length; i++ ) 
      if ( ninjas[i] == (first + " " + last) ) 
        ret.push( ninjas[i] ); 
    return ret; 
  }); 
} 
 
var ninjas = new Ninjas(); 
assert( ninjas.find().length == 3, "Finds all ninjas" ); 
assert( ninjas.find("Sam").length == 1, "Finds ninjas by first name" ); 
assert( ninjas.find("Dean", "Edwards").length == 1, "Finds ninjas by first and last name" ); 
assert( ninjas.find("Alex", "X", "Russell") == null, "Does nothing" );
   
function addMethod(object, name, fn){
  // Save a reference to the old method
  var old = object[ name ];

  // Overwrite the method with our new one
  object[ name ] = function(){
    // Check the number of incoming arguments,
    // compared to our overloaded function
    if ( fn.length == arguments.length )
      // If there was a match, run the function
      return fn.apply( this, arguments );

    // Otherwise, fallback to the old method
    else if ( typeof old === "function" )
      return old.apply( this, arguments );
  };
}

function Ninjas(){
  var ninjas = [ "Dean Edwards", "Sam Stephenson", "Alex Russell" ];
  addMethod(this, "find", function(){
    return ninjas;
  });
  addMethod(this, "find", function(name){
    var ret = [];
    for ( var i = 0; i < ninjas.length; i++ )
      if ( ninjas[i].indexOf(name) == 0 )
        ret.push( ninjas[i] );
    return ret;
  });
  addMethod(this, "find", function(first, last){
    var ret = [];
    for ( var i = 0; i < ninjas.length; i++ )
      if ( ninjas[i] == (first + " " + last) )
        ret.push( ninjas[i] );
    return ret;
  });
}

var ninjas = new Ninjas();
assert( ninjas.find().length == 3, "Finds all ninjas" );
assert( ninjas.find("Sam").length == 1, "Finds ninjas by first name" );
assert( ninjas.find("Dean", "Edwards").length == 1, "Finds ninjas by first and last name" );
assert( ninjas.find("Alex", "X", "Russell") == null, "Does nothing" );

```
>这里作者向我们展示了一种更加骚的操作，通过上一个样例的方法，为find这个方法添加了三种不同的方法，实现不同参数调用不同的函数的功能

<br><br>
___
This tutorial contains code and discussion from the upcoming book Secrets of the [JavaScript Ninja](https://www.amazon.com/gp/product/193398869X/ref=as_li_qf_sp_asin_il_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=193398869X&linkCode=as2&tag=emotastic-20&linkId=6VMJQCURPKUH5LYY) by John [Resig](https://johnresig.com/).