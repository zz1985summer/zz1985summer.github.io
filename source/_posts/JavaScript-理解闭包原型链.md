---
title: JavaScript 理解闭包原型链
date: 2017-12-23 10:39:37
tags:
---

# 首先此文是学习过程中的个人理解，如有偏颇，欢迎斧正  

# 关于闭包  
<pre><code>
function foo(){  
	var i=999;  
	return function (){  
		console.log(i+1000);  
	}  
}  

var f1=foo();  
f1();  			//1999  
</code></pre>  

foo 里面的那个匿名函数就叫闭包，在没有这个闭包之前，外层函数 f1, 是无法调用foo 函数局部变量 i 的值的.

所以闭包可以说就是解决外层函数 f1 要读取某函数 foo 的局部变量，正常情况作用域变量只允许局部作用域往上读取外层的全局作用域变量。所以这里通过 foo 函数的内层匿名函数（也可以写成非匿名函数，最后将内层函数名作为返回值返回）往上读取 foo 的变量 i ，并将结果返回给外层函数。

一句话概括:闭包就是某函数的外层函数通过该函数的闭包调用该函数的局部变量进行操作。

<strong style="color:red">注意</strong>: 局部变量 i 这里是不会自动释放的，虽然它是局部变量，但是被闭包函数引用了，而闭包函数又被外层 f1 函数引用了，所以需要手动的 f1=null; 来释放 foo 的局部变量 i .  


# 函数作用域  

<pre><code>
ex1:

function globalvr(){
	x=1;
	console.log(x);   //1
}

console.log(x);    //1

ex2:

function globalvr2(){
	var x=1;
	console.log(x);   //1
}

console.log(x);     //ReferenceError  

</code></pre>  

这里 ex1 里面 x 变量没有定义，函数会现在 globalvr 局部作用域查找，没有找到，在往上一层 window 全局查找，如果也没有找到，则在 window 全局作用域中自动生成一个变量 x 因此 ex1 里面的内外 x 值都为 1。
## 名词：
全局作用域 Window  
函数作用域 Activation Object  
  
```
var a=10;
function fun(){
	console.log(a);
	var a=100;
	console.log(a);
}
fun();
console.log(a);
```  
## 作用域链：

![](/images/jsprototype/scopetrain.jpeg)  

1. js 运行时创建一个 ECS Execute Context Stack 函数执行上下文栈，浏览器主程序运行在这个栈中会先 new 一个 window 全局作用域对象，用来存储所有变量。
2. 全局作用域声明的变量 a 和 function fun 存储在window作用域对象中，其中 fun 引用类型实际指向 function 的定义位置，而function 中隐藏的属性 scope 由指回创建它的根 window 以标记它从哪调用创建出来。因此函数 window.fun() 这样屌用也是可以的。
3. 当函数 fun 被调用运行时，在 ECS 函数执行上下文中运行 fun 而此时 fun 生成其自己的局部作用域 AO 
4. fun 内定义的变量 a 会存在 AO 中，而 AO 有一个 _parent_ 属性，指向其父源 window （也有可能是别的父对象）js 在查找使用变量时会先从最内层 AO 查找，如果 AO 没有则往其父源作用域中查找，一直往上链状查找，就形成了作用域链。  

# 原型对象
prototype 在定义构造函数时，函数自动创建一个原型对象 prototype 用来集中保存子对象共有成员。

# 继承  

![](/images/jsprototype/inherit.jpeg)  

1.new 方法让新对象的 \_proto\_ 属性指向父辈的 prototype 对象。
2.因此 prototype 中的方法变量子对象可以共用，即为继承父对象方法变量。

<pre><code>
ex:
Person.prototype.sayName=function(){
	console.log("hello,I'm"+this.name+"I'm"+this.age+"years old now.");
}
</code></pre>


# 原型链  

![](/images/jsprototype/prototype.png)  

Array 构造函数中存储了所有数组共用的方法

<pre><code>
var arr=new Array();
console.log(arr._proto_==Array.prototype);  //true	
</code></pre>

原型链就是由多级继承形成的这种链式结构就是原型链  
![](/images/jsprototype/prototrain.jpeg)


