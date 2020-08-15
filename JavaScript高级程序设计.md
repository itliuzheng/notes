# JavaScript高级程序设计（第三版）

## JavaScript简介

## 在HTML中使用JavaScript

## 基本概念

## 变量、作用域和内存问题

## 引用类型

### 函数内部属性

#### arguments

1. callee   该属性是一个指针，指向拥有这个arguments对象的函数

   ```javascript
   function factorial(num){
   	if(num <= 1){
   		return 1
   	}else{
   		return num * factorial(num - 1)
   	}
   }
   ```

   

   ```javascript
   function factorial(num){
   	if(num <= 1){
   		return 1
   	}else{
   		return num * arguments.callee(num - 1)
   	}
   }
   ```

2. this

   引用的是函数据以执行的环境对象

3. caller

   这个属性中保存着调用当前函数的函数的引用。如果在全局作用域中调用当前函数，它的值为`null`

   ```javascript
   function a(){
       b()
   }
   function b(){
       alert(a.caller)
   }
   a()
   
   
   
   function a(){
       b()
   }
   function b(){
       alert(arguments.callee.caller)
   }
   ```

   

   

   在严格模式下  访问 `arguments.callee`会导致错误

## 面向对象的程序设计

### 理解对象

#### 属性类型 	defineProperty

 1. 数据属性

    `[[Configurable]]`   能否通过`delete`删除属性从而重新定义属性，能否修改属性的特性，或者能否把属性修改为访问器属性。

    `[[Enumerable]]`	 是否可枚举。能否通过for-in 循环返回属性

    `[[Writable]]`	 	能否修改属性的值

    `[[Value]]`			   包含这个属性的数据值

    `Object.defineProperty('属性所在的对象','属性的名字','一个描述符对象')`

    一个描述符对象：

    ​	configurable		

    ​	enumerable

    ​	writable				

    ​	value

    ```javascript
    var person = {}
    Object.defineProperty(person,'name',{
        writable:false,
        value:'liuzheng'
    })
    alert(person.name)   //liuzheng
    person.name = 'xxxx'
    alert(person.name)	 //liuzheng
    ```

    

 2. 访问器属性     

    `[[Configurable]]`   能否通过`delete`删除属性从而重新定义属性，能否修改属性的特性，或者能否把属性修改为访问器属性。

    `[[Enumerable]]`	 是否可枚举。能否通过for-in 循环返回属性

    `[[Get]]`	 	在读取属性时调用的函数 默认值 `undefined`

    `[[Set]]`		 在写入属性时调用的函数  默认值 `undefined`

    ```javascript
    var book = {
        _year:2020,
        edition:1
    };
    
    Object.defineProperty(book,'year',{
        get:function(){
            return this._year
        },
        set:function(newValue){
            if(newValue > 2020){
             	this._year = newValue;
                this.deition += newValue - 2020;
            }
        }
    })
    
    book.year = 2021
    alert(book.edition)   //2
    ```

####  定义多个属性

```javascript
var book = {}

Object.defineProperty(book,{
    _yaer:{     //数据属性
        writable:false,
        value:'2020'
    },
    year:{		//访问器属性
        get:function(){
            return this._year
        },
        set:function(newValue){
            this._year = newValue
        }
    }
})

//唯一区别是这里的属性都是同一时间创建的
```

#### 读取属性的特性   getOwnPropertyDescriptor()

```javascript
var desc = Object.getOwnPropertyDescriptor('属性所在的对象','要读取其描述符的属性名称')
```

返回值是一个对象（**数据属性**  或  **访问器属性**）



### 创建对象

#### 工厂模式

```javascript
function createPerson(name,age,job){
    var o = new Object();
    o.name = name;
    o.age = age;
    o.job = job;
    o.sayName = function(){
        alert(this.name)
    };
    return o;	
}
var person1 = createPerson("","","");
var person2 = createPerson("","","");

//解决了创建多个相似对象的问题
//问题是：没有解决对象识别的问题（怎么知道一个对象的类型）

```

#### 构造函数模式

```javascript
function Person(name,age,job){
    this.name = name;
    this.age = age;
    this.job = job;
    this.sayName = function(){
        alert(this.name)
    }
}

var person1 = new Person('liuzheng',28,'g')
var person2 = new Person('liu',2,'g3')

/*
	没有显式地创建对象
	直接将属性和方法赋给了this对象
	没有return语句
*/

/*	使用 new 操作符
	1. 创建一个新对象
	2. 将构造函数的作用域赋给新对象（this就指向了这个对象）
	3. 执行构造函数中的代码
	4. 返回新对象
*/

person1.constructor == Person   //true
person2.constructor == Person   //true


//检测对象类型  instanceof 更可靠一些

person1 instanceof Object   //true
person1 instanceof Person   //true

person2 instanceof Object   //true
person2 instanceof Person   //true
```

##### 1.将构造函数当做函数

##### 2.构造函数的问题

​	构造函数内部的方法不是同一个Function的实例

​	等于说 **不同实例上的同名函数是不相等的**

#### 原型模式

```javascript
functin Person(){
}

Person.name = 'liuzheng';
Person.sayName = function(){
    alert(this.name)
}
var person1 = new Person();
var person2 = new Person();

person1.sayName == person2.sayName   //true
```

##### 1. 理解原型对象

​		Person构造函数      Person的原型对象（Person.prototype）     Person的实例

​		Person构造函数的prototype 指向了 原型对象（Person.prototype）

​		原型对象（Person.prototype）的 constructor 又指回了 Person构造函数

​		Person的实例的内部属性（`__prototype__`）只指向了原型对象（Person.prototype）   ==》与构造函数没有直接关系

```javascript
//Object.getPrototypeOf()    返回的对象 实际上就是这个对象的原型

Object.getPrototypeOf(person1) == Person.prototype   //true
Object.getPrototypeOf(person1).name    //liuzheng

```



当为对象实例添加一个属性时，这个属性会**屏蔽**原型对象同名属性

```javascript
// hasOwnProperty()  可以检测一个属性是存在于实例上还是原型中
// 这个方法是在给定属性存在于对象实例中 才会返回 true
```



##### 2. 原型与in操作符

​	有2种方式使用in操作符

​		单独使用：通过对象能够访问给定属性时返回true（原型、实例都返回true）

​		for-in：所有能够通过对象访问的、可枚举（enumerated）属性（原型、实例）

```javascript
function hasPrototypeProperty(object,name){
    return !Object.hasOwnProperty(name) && ( name in object)
}
//原型 true
//实例 false
```



##### 3. 更简单的原型语法

```javascript
function Person(){
}

Person.prototype = {
    name : 'liuzheng',
    sayName:function(){
        alert(this.name)
    }
}

// constructor 属性不再指向Person   
// 这种写法 本质上 重写了默认的 prototype 对象  
// instanceof 能返回正确的结果

var person = new Person();

person instanceof Object	//true
person instanceof Person	//true
person.constructor == Person	//false
person.constructor == Object	//true


//解决方法 一
function Person(){
}

Person.prototype = {
    constructor:Person,  //会导致属性变成 可枚举
    name : 'liuzheng',
    sayName:function(){
        alert(this.name)
    }
}
//解决方法 二
function Person(){
}

Person.prototype = {
    name : 'liuzheng',
    sayName:function(){
        alert(this.name)
    }
}
//重设构造函数
Object.defineProperty(Person.prototype,'constructor',{
    enmuerable:false,
    value:Person
})
```

##### 4. 原型的动态性

​	因为实例与原型之间的连接只不过是一个指针，而非一个副本

​	如果重写原型对象，就等于切断了构造函数与最初原型之间的联系

​	**实例中的指针仅指向原型，而不指向构造函数**

```javascript
function Person(){
}
var frined = new Person();
Person.prototype = {
    constructor:Person,  
    name : 'liuzheng',
    sayName:function(){
        alert(this.name)
    }
}
frined.sayName() // error

```

##### 5. 原生对象的原型

```java
String.prototype.startsWith = function(text){
    return this.indexOf(text) == 0
}
```

##### 6. 原型对象问题

​	最大的问题就是其共享的本性所导致。

​	引用类型最为突出

```javascript
function Person(){
}
var frined = new Person();
Person.prototype = {
    constructor:Person,  
    name : 'liuzheng',
    friends:['liu'],
    sayName:function(){
        alert(this.name)
    }
}

var person1 = new Person()
var person2 = new Person()

person1.friends.push('2')

person1.friends //  ['liu','2']
person2.friends //  ['liu','2']
```

#### 组合使用构造函数模式和原型模式

```javascript
function Person(name,job){
    this.name = name;
    this.job = job;
    this.friends = ['1','2'];
}
Person.prototype = {
    constructor:Person,  
    sayName:function(){
        alert(this.name)
    }
}
```

#### 动态原型模式

```javascript
function Person(name,job){
    this.name = name;
    this.job = job;
    this.friends = ['1','2'];

	if(typeof this.sayName != "function"){
       Person.prototype.sayName = function(){
           alert(this.name)
       }
    }
}
```

#### 寄生构造函数模式

```javascript
//这个模式跟工厂模式其实一模一样，除了使用 new 操作符
function SpicalArray(){
    var values = new Array();
    valurs.push.apply(values,arguments);
    varlus.toPipedString = function(){
        return this.join('|')
    }
    return values
}
var colors = new SpicalArray('1','2'，'3')；
colors.toPipedString()   // 1|2|3
```

**返回的对象与构造函数或者与构造函数的原型属性之间没有关系**

不建议使用这种模式

#### 稳妥构造函数模式

没有公共属性，其方法也不引用this的对象

```javascript
function Person(name,age,job){
    var o = new Object();
    o.sayName = function(){
        alert(name)
    }
}
```



### 继承

​	许多OO语言都支持两种继承方式：

​		接口继承：只继承方法签名

​		实现继承：继承实际的方法

​	由于函数没有签名，ECMAScript无法实现接口继承，只支持实现继承。

#### 原型链

```javascript
function SuperType(){
    this.property = true;
}
SuperType.prototype.getSuperValue = function(){
    return this.property;
}
function SubType(){
    this.subproperty = false;
}
//继承
SubType.prototype = new SuperType();
SubType.prototype.getSubValue = function(){
    return this.subproperty
}
var instance = new SubType();
instance.getSuperValue()	//true
```

##### 1.别忘记默认的原型

​	Object.prototype

##### 2.确定原型和实例的关系

​	1) instanceof

```javascript
instance instanceof Object		//true
instance instanceof SuperType	//true
instance instanceof SubType		//true
```

​	2) isPrototypeOf()

```javascript
Object.prototype.isPrototypeOf(instance) 		//true
SuperType.prototype.isPrototypeOf(instance) 	//true
SubType.prototype.isPrototypeOf(instance) 		//true
```



##### 3.谨慎地定义方法

​	给原型添加方法的代码一定要放在替换原型的语句之后.

##### 4.原型链的问题

​	**第一个问题是包含引用类型值的原型**

```javascript
function SuperType(){
    this.colors = ["red","blue","green"];
}
function SubType(){
}
//继承
SubType.prototype = new SuperType();
var instance1 = new SubType();
instance1.colors.push("black")
instance1.colors   // ["red","blue","green","black"]

var instance2 = new SuperType()
instance2.colors   // ["red","blue","green","black"]
```

**第二个问题是 在创建子类型的实例时，不能想超类型的构造函数中传递参数**

​	实际上，应该说是没有办法在不影响所有对象实例的情况下，给超类型的构造函数传递参数。

#### 借用构造函数（ constructor stealing ）(伪造对象、经典继承)

​	技术思想：在子类型构造函数的内部调用超类型构造函数

```javascript
function SuperType(){
    this.colors = ["red","blue","green"];
}
function SubType(){
    SuperType.call(this)
}
var instance1 = new SubType();
instance1.colors.push("black")
instance1.colors   // ["red","blue","green","black"]

var instance2 = new SuperType()
instance2.colors   // ["red","blue","green"]
```

##### 1.传递参数

`SuperType.call(this,'参数')`

##### 2.借用构造函数的问题

方法都在构造函数中定义，函数复用就无从谈起了

#### 组合继承（ combination inheritance）（伪经典继承）

将原型链和借用构造函数的技术组合到一起

```javascript
function SuperType(name){
    this.name = name;
    this.colors = ["red","blue","green"];
}
SuperType.prototype.sayName = function(){ 
    return this.name
}
function SubType(name,age){
    SuperType.call(this,name)			 //第二次调用 SuperType()
    this.age = age;
}
SubType.prototype = new SuperType();     //第一次调用 SuperType()
SubType.prototype.constructor = SubType
SubType.prototype.sayAge = function(){
    alert(this.age)
}

var instance1 = new SubType("liuzheng",29)
instance1.colors.push("black");
instance1.colors   //["red","blue","green","black"]
instance1.sayName()  //liuzheng
instance1.sayAge()  //29

var instance2 = new SubType("2",3)
instance2.colors   //["red","blue","green"]
instance2.sayName()  //2
instance2.sayAge()  //3

```

##### 组合继承的不足，最大的问题

无论什么情况下，都会调用两次超类型构造函数

一是创建子类型原型的时候

二是在子类型构造函数内部

#### 原型式继承

道格拉斯·克罗克福德

```javascript
function object(o){
    function F(){}
    F.prototype = o;
    return new F();
}
```

```javascript
var person = {
    name:'liuzheng',
    friends:["red","blue","green"]
}
var anotherPerson = object(person);
anotherPerson.name = "Wuningning";
anotherPerson.friends.push("black");

var yetAnotherPerson = object(person);
yetAnotherPerson.name = "ning";
yetAnotherPerson.friends.push("grey");

person.friends   //["red","blue","green","black","grey"]
```

##### Object.create()

规范了原型式继承。

`Object.create(“一个用作新对象原型的对象”,"（可选）一个为新对象定义额外属性的对象")`

在传入一个参数的情况下，与 上述 object() 方法的行为相同

```javascript
var person = {
    name:'liuzheng',
    friends:["red","blue","green"]
}
var anotherPerson = Object.create(person);
anotherPerson.name = "grod"
anotherPerson.friends.push("black")

var yetAtherPerson = Object.create(person);
yetAtherPerson.name = "wuningning"
yetAtherPerson.friends.push("grey")

yetAtherPerson.friends  //["red", "blue", "green", "black", "grey"]
```

```javascript
var person = {
    name:'liuzheng',
    friends:["red","blue","green"]
}
var anotherPerson = Object.create(person,{
    name : {
        value:"wuningning"
    }
});
anotherPerson.name // wuningning
```

#### 寄生式继承

思路：与 寄生构造函数 和 工厂模式 类似

​	创建一个仅用于封装继承过程的函数，

​	该函数在内部以某种方式来增强对象，

​	最后再像真地是它坐了所有工作一样返回对象

```javascript
function createAnother(original){
    var clone = object(original);  //通过调用函数创建一个新对象
    clone.sayHi = function(){		//以某种方式来增强这个对象
        alert("hi")
    }
    return clone					//返回这个对象
}
//object函数不是必需；任何能够返回新对象的函数都适用此模式
```

#### 寄生组合式继承（引用类型最理想的继承范式）

##### 解决组合继承的不足

通过借用构造函数来继承属性，通过原型链的混成形式来继承方法。

思路：不必为了指定子类型的原型而调用超类型的构造函数，我们所需要的无非就是超类型原型的一个副本。本质上，就是使用寄生式继承来继承超类型的原型。然后再将结果指定给子类型的原型

```javascript
function inheritPrototype(subType,superType){
    var prototype = Object(superType.prototype);   //创建对象
    prototype.constructor = subType;				//增强对象
    subType.prototype = prototype;					//指定对象
}

function SuperType(name){
    this.name = name;
    this.colors = ["red","blue","green"];
}
SuperType.prototype.sayName = function(){ 
    return this.name
}
function SubType(name,age){
    SuperType.call(this,name)			 //一次调用 SuperType()
    this.age = age;
}
inheritPrototype(SubType,SuperType)      //解决两次调用超类型构造函数
//SubType.prototype = new SuperType();     
//SubType.prototype.constructor = SubType
SubType.prototype.sayAge = function(){
    alert(this.age)
}
```



## 函数表达式

最重要的特质 **函数申明提升**



**匿名函数-----拉姆达函数**

function关键字没有name标识符

```javascript
var functionName = function(name1,name2,name3){}
//匿名函数 函数表达式   不存在函数申明提升
```

### 递归

```javascript
function factorial(num){
    if(num <= 1){
       return 1;
	}else{
        return num * factorial(num - 1);
    }
}

var anotherFactorial = factorial;
factorial = null;
anotherFactorial(4)  //出错   因为内部函数又调用 factorial 

//解决方法   arguments.callee  指向正在执行的函数的指针
//但是在严格模式下 不能通过脚本访问 arguments.callee  会报错
function factorial(num){
    if(num <= 1){
       return 1;
	}else{
        return num * arguments.callee(num - 1);
    }
}
```

```javascript
//这种就ok
var factorial = (function f(num){
    if(num <= 1){
       return 1;
	}else{
        return num * f(num - 1);
    }
})
```

### 闭包

**指有权访问另一个函数作用域中的变量的函数**

#### 闭包与变量

#### 关于this对象

#### 内存泄漏

### 模仿块级作用域

```javascript
(function(){
    //这里是块级作用域
})()
```

**以上代码定义并立即调用了一个匿名函数。**

将函数申明包含在一对圆括号中，表示它实际上是一个函数表达式。而紧随其后的另一对圆括号会立即调用这个函数。



函数申明后面不能跟圆括号

函数表达式后面可以跟圆括号

要将函数申明转换成函数表达式只需要加圆括号就行。

### 私有变量

**特权方法**

​	有权访问私有变量和私有函数的公有方法

 1. 在构造函数中定义特权方法

    ```javascript
    function MyObjiect(){
        //私有变量和私有函数
        var privateVariable = 10;
        function privateFunction(){
            return false
        }
        
        //特权方法
        this.publicMethod = function(){
            privateVariable++;
            return privateFunction();
        }
    }
    ```

	2. x

#### 静态私有变量

```javascript
(function(){
    var v = 10;
    function vF(){
        return false
    }
    //通过不给变量声明，会自动创建全局变量，但是在严格模式下会报错
    MyObject = function(){}    
   
    MyObject.prototype.public = function(){
        v++;
        return vF()
    }
})()
```

#### 模块模式

为单例创建私有变量和特权方法。

##### 单例

​	只有一个实例的对象，本质上 对象字面量定义的是单例的公共接口

```javascript
var singleton = {
    name:value,
    method: function(){
        
    }
}
```

```javascript
var singleton = function(){
    
    //私有变量和私有函数
    var privateVariable = 10;
    function privateFunction(){
        return false
    }
    
    return {
        privateProperty:true,
        publicMethod:function(){
            privateVariable++;
            return privateFunction()
        }
    }
}
```

#### 增强的模块模式

```javascript
var singleton = function(){
    
    //私有变量和私有函数
    var privateVariable = 10;
    function privateFunction(){
        return false
    }
    
    var object = new CustomType();   //某种类型的实例
    object.privateProperty = true,
	object.publicMethod = function(){
        privateVariable++;
        return privateFunction()
    }
    return object
}
```



## BOM

### window对象

#### 全局作用域

#### 窗口关系及框架

#### 窗口位置

```javascript
var leftPos = (typeof window.screenLeft == 'number')?window.screenLeft:window.screenX;
var topPos = (typeof window.screenTop == 'number')?window.screenTop:window.screenY;
```

#### 窗口大小

`innerWidth`   `innerHeight`

​	该容器中页面视图区的大小（减去边框宽度）   可见视口

`outerWidth`   `outerHeight`

​	IE9+ Safari  Firefox   浏览器窗口本身的尺寸

​	Opera	页面视图容器大小  

​	Chrome  视口大小  打开操作台后 高度与inner不一致

​					是标签页下面整个网页大小 （全屏时  = `innerWidth`   `innerHeight`）

```javascript
var pageWidth = window.innerWidth,
    pageHeight = window.innerHeight;
if(typeof pageWidth != 'number'){
    if(document.compatMode == 'CSS1Compat'){
        pageWidth = document.documentElement.clientWidth;
        pageHeight = document.documentElement.clientHeight;
    }else{
        pageWidth = document.body.clientWidth;
        pageHeight = document.body.clientHeight;
    }
}
```

#### 导航与打开窗口

```javascript
window.open("要加载的URL","窗口目标","一个特性字符串","新页面是否取代浏览器历史记录中当前加载页面的布尔值")
//通常只需要传递第一个参数就行，最后一个参数只在不打开新窗口的情况下使用
```

##### 1.弹出窗口

##### 2.安全限制

##### 3.弹出窗口屏蔽程序

```javascript
var blocked = false;
try{
    var wroxWin = window.open("http://www.baidu.com","_block");
    if(wroxWin == null){
    	blocked = true;   
	}
} catch(err){
    blocked = true
}
if(blocked){
    alert("这个窗口被屏蔽了")
}
```

#### 间歇调用和超时调用

##### setTimeout()

##### setInterval()



#### 系统对话框

##### alert

##### confirm

##### prompt



### location对象

window.location    document.location  引用的是同一个对象

| 属性名   | 例子                 | 说明                       |
| -------- | -------------------- | -------------------------- |
| hash     | #contents            | #后面                      |
| host     | www.baidu.com:80     | 返回服务器名称和端口号     |
| hostname | www.baidu.com        | 返回不带端口号的服务器名称 |
| href     | http://www.baidu.com | 完整URL                    |
| pathname | /mulu/               | URL中的目录或文件名        |
| port     | 8080                 | URL中指定的端口号          |
| protocol | http:                | 协议                       |
| search   | ?q=xxxx              | 查询字符串                 |

#### 查询字符串参数

```javascript
function getQueryStringArgs(){
    var qs = (location.search.length > 0?location.search.substring(1):""),
        args = {},
        items = qs.length?qs.split('&'):[],
        item = null,
        name = null,
        value = null,
        len = items.length;
    for(let i = 0,i<len;i++){
        item = items[i].split("=");
        name = decodeURIComponent(item[0]);
        value = decodeURIComponent(item[1]);
        if(name.length){
           args[name] = value;
        }
    }
    return args;
}
```

#### 位置操作

```javascript
//效果一样
window.location = "http://www.baidu.com";
location.href = "http://www.baidu.com";

location.reload();   //重新加载（有可能从缓存中加载）
location.reload(true);	//重新加载（从服务器重新加载）
```



#### navigator对象

navigator.userAgent   浏览器的用户代理字符串

#### 检测插件

### 注册处理程序

**RSS源的处理程序**

​	例如：RSS阅读器    在线电子邮件程序

### screen对象

浏览器窗口外部的显示器信息

### history对象

```javascript
history.go(-1)  //后退一页
history.go(1)	//前进一页

history.back()
history.forward()

if(history.length == 0){
    //这应该是用户打开窗口的第一个页面
}
```



## 客户端检测

### 能力检测（特性检测）

第一个概念是先检测打成目的的最常用的特性。

第二个概念是必须测试实际要用到的特性

#### 更可靠的能力检测

```javascript
function isHostMethod(object,property){
    var t = typeof object[property];
    return t == 'function' || (!!(t == 'object' && object[property])) || t == 'unknown'
}
```

### 怪癖检测

想要知道浏览器存在什么缺陷（bug）

### 用户代理检测

待看

## DOM

## DOM扩展

## DOM2和DOM3

## 事件

## 表单脚本

## 使用Canvas绘图

## HTML5脚本编程

## 错误处理与调试

## JavaScript与XML

## E4X

## JSON

## Ajax与Comet

## 高级技巧

## 离线应用与客户端存储

## 最佳实践

## 新兴的API



