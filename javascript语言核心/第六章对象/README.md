## 第六章 对象
> 对象是js的基本数据类型  
> 对象是一种复合值：它将很多值(原始值或者其他对象)聚合在一起，可以通过名字访问这些值  
> 对象也可以看做是属性的无序集合，每个属性都是一个名/值对  
> 属性名是字符串，因为我们可以把对象看成从字符串到值得映射  
> 这种基本数据结构还有很多种叫法，有些我们已经非常书序，比如：散列(hash)、散列表(hashtable)、字典(dictionary)、关联数据(associativearray)  
> 然而对象不仅仅是字符串到值得映射，除了可以保持自由的属性，js对象还可以从一个称为原型的对象继承属性  
> 对象的方法通常是继承的属性。这种`“原型式继承(prototypal inheritance)”`是js的核心特征  
> 除了字符串、数字、true、false、null和nudefined之外，js中的值都是对象。尽管支付穿、数字和布尔值不是对象、但他们的行为和不可变对象非常类似  
> 对象最常见的方法是创建、设置、查找、删除、检测、枚举他的属性  
> 属性包括名字和值。属性名可以使包含空字符串在内的任意字符串，但对象中不能存在两个同名的属性。值可以使任意js值，或者可以使一个`getter`或`setter`函数。除了名字之外，每个属性还有一些与之相关的值，称为“属性特性”  

* 可写(writable attribute)，标识是否可以设置该属性的值
* 可枚举(enumerable attribute)，标识是否可以通过for/in循环返回该属性
* 可配置(configurable attribute)，标识是否可以删除或修改该属性  

> 在ECMAScript5之前，通过代码给对象创建的所有属性都是可写的、可枚举的和可配置的。在ECMAScript5中则可以对这些特性加以配置。  
> 除了包含属性之外，每个对象拥有三个相关的对象特性  
* 对象的原型(prototype)指向另外一个对象，本对象的属性继承自他的原型对象
* 对象的类(class)是一个标识对象类型的字符串
* 对象的扩展标记(extensible flag)指明了是否可以向该对象添加新数据  

> 最后，我们用下面这些术语来对三类js对象和两类属性作区分
* 内置对象(native object)是由ECMAScript规范定义的对象或类。例如：数字、函数、日期和正则表达都是内置对象
* 自定义对象(user-defined object)是由运行中的js代码创建的对象
* 自由属性(own property)是直接在对象中定义的属性
* 继承属性(inherited property)是在对象的原型对象中定义的属性  

### 6.1 创建对象
> 可以通过对象直接量、关键字new和Object.create()函数来创建对象  

#### 6.1.1 对象直接量
> 创建对象最简单的方法就是在js代码中使用对象直接量。对象直接量是由若干名/值对组成的映射表，名/值对中间用冒号分割，名/值对之间用逗号分隔，整个映射表用花括号包裹起来  
``` javascript
var empty = {};                                     // 没有任何属性的对象
var point = { x : 0, y : 0};                        // 两个属性
var point2 = { x : point.x, y : point.y + 1 };      // 更复杂的值
var book = {
  "main title" : "JavaScript",                      // 属性名里有空格，必须用字符串表示
  "sub-title" : "The Definitive Guide",             // 属性名利有连字符，必须用字符串表示
  "for" : "all audiences",                          // for是保留字，因为必须用引号
  author : {                                        // 这个属性的值是一个对象
    firstname : "David",                            // 注意，这里的属性名都没有引号
    surname : "flanagan"
  }
}
```  
> 对象直接量是一个表达式，这个表达式的每次运算都创建并初始化一个新的对象。每次计算对象直接量的时候，也都会计算他的每个属性值。也就是说，如果在一个重复调用的函数中的循环体内使用了对象直接量，他讲创建很多新对象，并且每次创建的对象的属性值也有可能不同  

#### 6.1.2 通过new创建对象
> `new`运算符创建并初始化一个新对象。关键字`new`后跟随一个函数调用。这里的函数称作`构造函数(constructor)`，构造函数用以初始化一个新创建的对象。js核心语言核心中的原始类型都包含内置构造函数
``` javascript
var o = new Object();             // 创建一个空对象，和{}一样
var a = new Array();              // 创建一个空数组，和[]一样
var d = new Date();               // 创建一个标识当前时间的Date对象
var r = new RegExp("js");         // 创建一个可以进行模式匹配的RegExp对象
```
> 除了这些内置构造函数，用自定义构造函数类初始化新对象也是非常常见的  

#### 6.1.3 原型
> 每一个js对象(null除外)都和另一个对象相关联。“另一个”对象就是我们熟知的原型，每一个对象都从原型继承属性  
> 所有通过对象直接量创建的对象都具有同一个原型对象，并可以通过js代码的`Object.prototype`获得对原型对象的应用。通过关键字new和构造函数调用创建的对象的原型就是构造函数的`prototype`属性的值。因为，同使用{}创建对象一样，通过`new Object()`创建的对象也继承自`Object.prototype`。同样，通过`new Array()`创建的对象的原型就是`Array.prototype`，通过`new Date()`创建的对象的原型就是`Date.prototype`。  

### 6.2 属性的查询和设置
> 可以通过点(.)或方括号([])运算符来获取属性的值。运算符左侧应当是一个表达式，他返回一个对象。对于点(.)来说，右侧必须是一个以属性名称命名的简单标识符。对于方括号来说([])，方括号内必须是一个计算结果为字符串的表达式，这个字符串就是属性的名字  
``` javascript
var author = book.author;             // 得到book的"author"属性
var name = author.surname;            // 得到获得author的“surname”属性
var title = book["main title"];       // 得到book的"main title"属性
```  
> 和查询属性值得写法一样，通过点和方括号也可以创建属性或给属性复制，但需要将他们放在复制表达式的左侧:
``` javascript
book.edition = 6;                     // 给book创建一个名为"edition"的属性
book["main title"] = "ECMAScript";    // 给"main title"属性赋值
```

#### 6.2.1 作为关联数据的对象
``` javascript
object.property;
object['property']
```
> 第一种语法使用点运算符和一个标识符，这和C和java中访问一个结构体或对象的静态字段非常类似。
> 第二种语法使用方括号和一个字符串，看起来更像数组，只是这个数据元素时通过字符串索引而不是数字索引。
> 这种数组就是我们所说的关联数据，也称作散列、映射或字典。js对象都是关联数据。  

> 反过来讲，当通过[]来访问对象的属性时，属性名通过字符串来标识。字符串是js的数据类型，在程序运行时可以修改和创建他们。因此可以在js中使用下面这种代码
``` javascript
// 这段代码读取customer对象的address0,address1,address2,address3属性，并将他们链接起来
var addr = "";
for(i = 0; i < 4; i++){
  addr += customer["address" + i] + '/n'
}

// 假设给portifolio添加新的股票
// 由于用户是在程序运行时输入股票名称，因此在之前无法得知这些股票的名称是什么。而由于在写程序的时候不知道属性名称，因此无法通过点(.)运算符来访问对象portfolio的属性，但可以使用[]运算符，因为他使用字符串值(字符串值是动态的，可以在运行时更改)而不是标识符(标识符是静态的，必须写死在程序中)作为索引对象属性进行访问。
function addstock(portfolio,stockname,shares){
  portfolio[stockname] = shares;
}

// 使用for/in循环遍历关联数据时，就可以清晰的体会到for/in的强大之处
function getvalue(portfolio){
  var total = 0.0;
  for(stock in portfolio){            // 遍历portfolio中的每只股票
    var shares = portfolio[stock];    // 得到每只股票的份额
    var price = getquote(stock);      // 查询股票价格
    total += shares * proce;          // 将结果累加至total中
  }
  return total;                       // 返回total的值
}
```

#### 6.2.2 继承
> js对象具有“自有属性”，也有一些属性是从原型对象继承而来的，为了更好的理解这种继承，必须更深入的了解属性访问的细节
``` javascript 
// 假设要查询对象o的属性x，如果中不存在x，那么将会继续在o的原型对象中查询属性x
// 如果原型对象中也没有x，但这个原型对象也有原型，那么继续在这个原型对象的原型上执行查询，知道找到x或者查找到一个原型是null的对象位置。
// 对象的原型属性构成了一个“链”，通过这个“链”可以实现属性的继承

// 通过原型继承创建一个新对象
// inherit()返回一个继承自原型对象p的属性的新对象
// 如果不存在Object.create()，则退化使用其他方法
function inherit(p){
  if(p == null) throw TypeError();          // p是一个对象，但不能是null
  if(Object.create)                         // 如果Object.create()存在
    return Object.create(p)                 // 直接使用
  var t = typeof p;                         // 进一步检测
  if(t !== "object" && t !== "function") throw TypeError();
  function f(){};                           // 定义一个空构造函数
  f.prototype = p;                          // 将其原型属性设置为p
  return new f();                           // 使用f()创建p的继承对象
}

var o = {};                                 // o从Object.prototype 继承对象的方法
o.x = 1;                                    // 给o定义一个属性x
vr p = inherit(o);                          // p继承o和Object.prototype
p.y = 2;                                    // 给p定义一个属性y
var q = inherit(p);                         // q继承p、o和Object.prototype
q.z = 3;                                    // 给q定义一个属性z
var s = q.toString();                       // toString继承自Object.prototype
q.x + q.y;                                  // 3：x和y分别继承自o和p
```