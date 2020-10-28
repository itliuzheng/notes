## 函数的扩展

### 函数参数的默认值

#### 基本用法

```javascript
function foo(x = 4){
    ...
}
    
let x = 99;
    
    //参数默认值是惰性求值		
function foo(p = x + 1){
    console.log(p);
}
foo()  //100
    
x = 100;
foo()  // 101
//每调用一次foo 都会重新计算x+1
```

#### 与解构赋值默认值结合使用

```javascript
function foo({x,y=5}){
    console.log(x,y);
}
foo({})		//undefined,5
foo({x:1})	//1,5
foo({x:1,y:2})	//1,2
foo()		//TypeError:Cannot read property 'x' of undefined


//这种写法不能省略第二个参数
function fetch(url,{method = 'GET',body = ''}){
    console.log(method);
}

/* 没有第二个参数时，函数参数的默认值就会生效，然后才是解构赋值的默认值生效*/
// 函数参数的默认值是空对象，但是设置了对象解构赋值的默认值
function m1({x = 0,y = 0} = {}){
    return [x,y]
}
// 函数参数的默认值是一个有具体属性的函数，但是没有设置对象解构赋值的默认值
function m2({x,y} = {x:0,y:0}){
    return [x,y]
}

m1()			//[0,0]
m2() 			//[0,0]

m1({x:3,y:8})	//[3,8]
m2({x:3,y:8})	//[3,8]

m1({x:3})		//[3,0]
m2({x:3})		//[3,undefined]

m1({})			//[0,0]
m2({})			//[undefined,undefined]

m1({z:3})		//[0,0]
m2({z:3})		//[undefined,undefined]

```

#### 参数默认值的位置

通常情况下，定义了默认值的参数应该是函数的尾参数。

```javascript
function f(x,y=5,z){
    return [x,y,z]
}
f()				//[undefined,5,undefined]
f(1)			//[1,5,undefined]
f(1,,2)			//报错
f(1,undefined,2)//[1,5,2]    只有传undefined才会触发默认赋值，null无效
```



#### 函数的length属性

指定了默认值以后，函数的length属性将返回没有指定默认值的参数个数。

**设置了默认值以后，length属性将失真**

默认值的参数不是尾参数，那么length属性也不再计入后面的参数。

#### 作用域

一旦设置了参数的默认值，函数进行声明初始化时，参数会形成一个单独的作用域 **context**。等到初始化结束，这个作用域就会消失。

不设置默认值时不会出现这种语法。

```javascript
var x = 1;
function f(x,y = x){
    console.log(y);
}

f(2)  //2

/*
	(x,y=x) 这段会形成一个单独的作用域。
	在这个作用域里 默认值x指向第一个参数x，而不是全局变量x
*/
```



```javascript
var x = 1;
function foo(x,y = function(){x = 5;}){
    var x = 3
    y()
    console.log(x)
}
foo()  	//3
x 		//1


var x = 1;
function foo(x,y = function(){x = 5;}){
    x = 3
    y()
    console.log(x)
}
foo()  	//2
x 		//1
```



#### 应用



## async 函数

### 同步执行代码

```javascript
// 写法一
let [foo, bar] = await Promise.all([getFoo(), getBar()]);

// 写法二
let fooPromise = getFoo();
let barPromise = getBar();
let foo = await fooPromise;
let bar = await barPromise;
```

