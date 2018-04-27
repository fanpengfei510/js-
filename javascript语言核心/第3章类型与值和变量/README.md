## 第三章 类型、值与变量
javascript的数据类型分两类：
> 原始类型：数字、字符串、布尔值(特殊原始值：null、nudefined)  
> 对象类型：属性的集合  

### 3.1 数字类型
``` javascript
// 整数直接量
0
3
1000000

// 浮点直接量
3.14
2345.19
.3333333
6.02e23   // 6.02 X 10的23次方

// javascript中的算数运算
+ // 加法运算符
- // 剪发运算符
* // 乘法运算符
/ // 除法运算符
% // 求余运算符

infinity                    // 将一个可读/写的变量初始化为infinity
Number.POSITIVE_INFINITY    // 同样的值，可读
1/0                         // 这样是同样的值
Number.MAX_VALUE + 1        // 计算结果还是infinity
Number.NEGATIVE_INFINITY    // 该表达式表示了负无穷大
-infinity
-1/0
-Number.MAX_VALUE + 1
NaN                         // 将一个可读/写的变量初始化为NaN
Number.NaN                  // 同样的值，但是可读
0/0                         // 计算结果是NaN
Number.MIN_VALUE / 2        // 发生下溢：计算结果为0
-Number.MIN_VALUE / 2       // 负零
-1/Infinity                 // 同样是负零
-0

/******************************/
var zero = 0;   // 正常的零值
var negz = 0;   // 负零值
zero === negz;  // true：正零值和负零值相等
1/zero === 1/zero;  // false：正无穷大和负无穷大不相等
```

### 3.2 文本
``` javascript
// 字符串直接量
""          // 空字符串：包含0哥字符
'testing'
"3.14"
"Hello World"
"two\nlines"    // 这里定义了一个显示为两行的字符串
// 用三行代码定义了显示为当行的字符串，只在ECMAScript5中可用
"one\           
 long\
 line"
```

#### 3.2.2 转义字符
> 在javascript字符串中，反斜线`(\)`有着特殊的用途，反斜线符号后加一个字符，就不在表示他们的字面含义了。  

| 转义字符 | 含义 |
| ------- | ---- |
| \o | NUL字符(\u0000) |
| \b | 退格符(\u0008) |
| \t | 水平制表符(\u0009) |
| \n | 换行符(\u000A) |
| \v | 垂直制表符(\u000B) |
| \f | 换页符(\u000C) |
| \r | 回车符(\u000D) |
| \\" | 双引号(\u0022) |
| \\' | 撇号或单引号(\u0027) |
| \\\ | 反斜线(\u005C) |
| \xXX | 由两位十六进制数XX制定的Latin-1字符 |
| \uXXXX | 由4位十六进制数XXXX制定的Unicode |  

#### 3.2.3 字符串的使用
``` javascript
msg = "Hello," + "World";    // 生成字符串：Hello,World

//除了.length属性，字符串还提供了许多可以调用的方法
var s = "hello,world";
s.chartAt(0);             // "h"：第一个字符串
s.charAt(s.length - 1);   // "d"：最后一个字符
s.substring(1,4);         // "ell"：第2-4个字符
s.slice(1,4);             // "ell"：同上
s.slice(-3);              // "rld"：最后三个字符
s.indexOf("l");           // 2：字符串l首次出现的位置
s.astIndexOf("l");        // 10：字符l最后一次出现的位置
s.indexOf("l",3);         // 3：在位置3及之后首次出现字符l的位置
s.split(", ");            // ["hello","world"]分隔字符串
s.replace("h","H");       // "Hello,world"：全文字符替换
s.toUpperCase();          // "HELLO,WORLD",字符串大写
```
> 在javascript中字符串是固定不变的，类似`replace()`和`toUpperCase()`的方法都返回新字符串，原字符串本身并不发生改变。  
``` javascript
// 字符串可以当做只读数组，除了使用charAt()方法，也可以使用方括号来访问字符串中的单个字符(16位值)
var s = "hello,world";
s[0];                 // "h"
s[s.length - 1];      // "d"
```

#### 3.2.4 匹配模式
> javascript定义了`RegExp()`构造函数，用来创建表示文本匹配模式的对象。String和RegExp对象均定义了利用正则表达式进行模式匹配和查找与替代的函数。  

尽管RegExp并不是语言中的基本数据类型，但是他们依然具有直接量写，可以直接在js程序中使用。在两条斜线中间的文本构成了一个正则表达式直接量。第二条斜线之后也可以根据一个或多个字母，用来修饰匹配模式的含义。
``` javascript
/^HTML/             // 匹配以HTML开始的字符串
/[1-9][0-9]*/       // 匹配所有包含一个或多个数字的实例
/\bjavascript\b/i   // 匹配单词'javascript'，忽略大小写
```

RegExp对象定义了很多有用的方法，字符串同样具有可以接受RegExp参数的方法
``` javascript
var text = "testing : 1, 2, 3";   // 文本示例
var pattern = /\d+/g;             // 匹配所有包含一个或多个数字的实例
pattern.test(text);               // true：匹配成功
text.search(pattern);             // 9：首次匹配成功的位置
text.match(pattern);              // ["1","2","3"]：所有匹配组成的数组
text.replace(pattern,"#");        // "testing:#,#,#"
text.split(/\D+/);                // ["","1","2","3"]：用非数字字符截取字符串
```

### 3.3 布尔值
> 布尔值是指真或假、开与关、是与否。这个类型只有两个值，保留字true和false。

布尔值通常用于js中的控制结构中。例如，js中的if/else语句。
``` javascript
// 如果为true，执行第一段逻辑，返回1。否则，执行下面的代码，返回2。
var a = 4;
if(a == 4){
  return 1;
}else{
  return 2;
}
```

> 下面的这些值会被转换为false
``` javascript
undefined
null
0
-0
NaN
""      // 空字符串
```

### 3.4 null和undefined

null定义：
> null是js语言的关键字，它表示一个特殊值，常用来描述"空值"。  
> 对null执行typeof预算，结果返回字符串"object"，也就是说，可以将null认为是一个特殊的对象值，含义是“非对象”。  

undefined定义：
> js还有第二个值来表示值的空缺。用未定义的值表示更深层次的“空值”。
> 他是变量的一种取值，表明变量没有初始化，如果要查询对象属性或数组元素的值时返回undeginded则说明这个属性或元素不存在。  

### 3.5 全局对象

全局对象(global object)在js中有着重要的用途：
> 全局对象的属性是全局定义的符号，js程序可以直接使用。当js解析器启动时，他将创建一个新的全局对象，并给他一组定义的初始属性。
* 全局属性：undefined、Infinity、NaN
* 全局函数：isNan()、parseInt()、eval()
* 构造函数：Date()、RegExp()、String()、Object()、Array()
* 全局对象：Math()、JSON  

全局对象的初始属性并不是保留字，但他们应该当做保留字来对待。

> 在代码的最顶级，不在任何函数内的js代码，可以使用js关键字this来引用全局对象。  
> 在客户端js中，在其表示的浏览器窗口中的所有js代码中，Window对象充当了全局对象。这个全局Window对象有一个属性window引用其自身，它可以代替this引用全局对象。Window对象定义了核心全局属性，但它也针对web浏览器和客户端js定义了一少部分其他全局属性  
> 当初次创建的时候，全局对象定义了js中所有的预定义全局值。这个特殊对象同样包含了为程序定义的全局值。如果代码声明了一个全局变量，这个全局变量就是全局对象的一个属性。
``` javascript
var global = this;  //定义一个引用全局对象的局部变量
```

### 3.6 包装对象
> * 存取字符串、数字或布尔值的属性时创建的临时对象称作包装对象，他只是偶尔用来区分字符串值和字符串对象、数字和数值对象以及布尔值和布尔对象。  
> * 由于字符串、数字、布尔值的属性都是只读的，并且不能给他们定义新属性，因此你需要明白他们是用于对象的。  
> * js对象是一种复合值：他是属性或已命名值的集合。通过`"."`符号来引用属性值。当属性值是一个函数的时候，称其为方法。通过fn.method()来调用对象fn中的方法。
``` javascript
var str = 'hello world';
var value = str.substring(str.indexOf(" ") + 1,str.length);
console.log(value); // world

var s = 'test', n = 1, b = true;    // 一个字符串、数字、布尔值
var S = new String(s);              // 一个字符串包装对象
var N = new Number(n);              // 一个数字包装对象
var B = new Boolean(b);             // 一个布尔值包装对象
```

### 3.7 不可变的原始值和可变的对象引用
> js中的原始值(nudefined、null、布尔值、数字和字符串)与对象(包括数组和函数)有着根本区别。  
> 原始值是不可更改的：任何方法都无法更改(或“突变”一个原始值)。对数字和布尔值来说显然如此----改变数字的值本身就说不通，而对字符串来说就不那么明显了，因为字符串看起来像由字符组成的数组，我们期望可以通过制定索引来修改字符串中的字符。  
> 实际上，js是禁止这样做的。字符串中所有的方法看上去返回了一个修改后的字符串，实际上返回的是一个新字符串
``` javascript
var s = 'hello';      // 定义一个由小写组成的字符串
s.toUpperCase();      // 返回"HELLO"，但并没有改变s的值
console.log(s);       // 'hello'：原始字符串的值并未改变
```

对象和原始值不同，首先，对象是可变的----他们的值是可修改的：
``` javascript
var obj = { x:1};       // 定义一个对象
obj.x = 2;              // 通过修改对象属性值来更改对象
obj.y = 3;              // 再次更改这个对象，给他添加一个新属性

var arr = [1,2,3];      // 数组也是可修改的
arr[0] = 0;             // 更改数组的一个元素
arr[3] = 4;             // 给数组添加一个新元素
```

对象的比较并非值的比较：即使两个对象包含同样的属性及相同的值，他们也是不相等的。各个索引元素完全相等的两个数组也不相等。
``` javascript
var obj1 = { x:1 }, obj2 = { x:1 };
obj1 == obj2;         // false：两个独立的对象永不相等
obj1 === obj2;        // false

var arr1 = [], arr2 = [];
arr1 == arr2;         // false：两个独立的数组永不相等
arr1 === arr2;        // false
```

对象的值都是引用，对象的比较均是引用的比较：当他们引用同一个对象时，他们才相等。
``` javascript
var a = [];       // 定义一个引用空数组的变量a
var b = a;        // 变量b引用同一个数组
b[0] = 1;         // 通过变量b来修改引用的数组
a[0];             // => 1：变量a也会修改
a === b;          // true：a和b引用同一个数组，因此他们相等

// 得到一个对象或者数组的副本，则必须复制对象的每个属性和数组的元素
var arr = ['a','b','c'];
var arr1 = [];
for(var i=0, len = arr.length; i < len; i++){
  arr1[i] = arr[i]
}

// 如果我们想比较两个单独的对象或者数组，则必须比较他们的属性或元素
function equalArrays(a,b){
  if(a.length != b.length) true false;        // 两个长度不同的数组不相等
  for(var i=0, len = a.length; i<len; i++)    // 循环便利所有元素
    if(a[i] !== b[i]) return false;           // 如果有任意元素不等，则数组不相等
  return true;                                // 否则他们相等
}
```

### 3.8 类型转换
javascript类型转换表
> 转换为数字的清醒比较微妙。那些以数字表示的字符串可以直接转换Wie数组，也允许在开始和结尾处带有空格。
> 但在开始和结尾处的任意非空格字符都不会被当成数字直接量的一部分，进而造成字符串转换为数字的结果为`NaN`。  
> true转换为1，flase、空字符串转换为0。

| 值 | 转换为字符串 | 数字 | 布尔值 | 对象 |
| -- | ----------- | --- | ------ | ---- |
| undefined | 'undefind' | NaN | false | thros TypeError |
| null | 'null' | 0 | false | thros TypeError |
| true | 'true' | 1 |   | new Boolean(true) |
| false | 'false' | 0 |   | new Boolean(false) |
| "" (空字符串) |  | 0 | false | new String("") |
| "1.2" (非空，数字) |  | 1.2 | true | new String("1.2") |
| "one" (非空，非数字) |  | NaN | true | new String("one") |
| 0 | '0' |   | false | new Number(0) |
| -0 | '0' |   | false | new Number(-0) |
| NaN | 'Nan' |   | false | new Number(NaN) |
| Infinity | 'Infinity' |   | true | new Number(Infinity) |
| -Infinity | '-Infinity' |   | true | new Number(-Infinity) |
| 1 (无穷大，非零) | '1' |   | true | new Number(1) |
| {} (任意对象) | 3.8.3章节 | 3.8.3章节 | true |  |
| [] (任意数组) | "" | 0 | true |  |
| [9] (1个数字元素) | "9" | 9 | true |  |
| ['a'] (其他数组) | 使用join()方法 | Nan | true |  |
| function(){} (任意函数) | 3.8.3章节 | Nan | true |  |


#### 3.8.1 转换为相等性
> 需要特别注意的是，一个值转换为另一个值并不意味这两个值相等。  
``` javascript
// == 相等运算符相等的含义，以下结果都为true
null == undefined;      // 认为相等
"0" == 0;               // 在比较前字符串转为数字
0 == false;             // 在比较前布尔值转换为数字
"0" == false;           // 在比较浅字符串和布尔值都转换为数字
```

#### 3.8.2 显式类型转换
> 尽管js可以自动做许多类型转换，但有时仍需要做显式类型转换，或者为了使代码变得清晰易读而做显式转换。  

**除了`null`和`undefined`之外的任何值都具有toString()方法，这个方法执行结果通常和String()方法的返回结果一致。**  
``` javascript
// 最简单的方法：Boolean()、Number()、String()、Object()函数
Number("3");       // 3
String(false);     // "false" 或使用 false.toString()
Boolean([]);       // true
Object(3);         // new Number(3)

// 一元运算符 “+”操作数转换为数字。“!”操作数转换布尔值取反。
x + "";     // 等价于String(x)
+x;         // 等价于 Number(x)，可以写成 x - 0;
!!x;        // 等价于Boolean(x)，双叹号

/*
  指数计数法，Number类为这些数字到字符串的类型转换定义了三个方法：
  toFixed()：根据小数点后的制定位数将数字转换为字符串，它从不使用指数计数法
  toExponential()：使用指数计数法将数字转换为指数形式的字符串，其中小数点前只有一位，小数点后的位数则由参数制定
  toPrecision()：根据制定的有效数字位数将数字转换为字符串，如果有效数字的位数少于数字整数部分的位置，则转换成指数形式。
*/
var num = 123456.789;
num.toFixed(0);         // "123457"
num.toFixed(2);         // "123456.79"
num.toFixed(5);         // "123456.78900"
num.toExponential(1);   // 1.2e+5
num.toExponential(3);   // 1.235e+5
num.toPrecision(4);     // 1.235e+5
num.toPrecision(7);     // 123456.8
num.toPrecision(10);    // 123456.7890

/*
parseInt()和parseFloat()函数，他们是全局函数，不从属与任何类的方法。
parseInt()：只解析整数
parseFloat()：可以解析整数和浮点数
*/
parseInt("3 bind mice");      // 3
parseFloat(" 3.14 meters");   // 3.14
parseInt("-12.34");           // -12
parseInt("0xFF");             // 255
parseInt("-0XFF");            // -255
parseFloat(".1");             // 0.1
parseInt("0.1");              // 0
parseInt(".1");               // NaN：整数不能以"."开始
parseFloat("$72.47");         // NaN：整数不能以"$"开始

// parseInt()可以接收第二个可选参数，这个参数制定数字转换的基数合法的范围是2~36
parseInt("11",2);       // 3 (1*2+1)
parseInt("ff",16);      // 255 (15*16+15)
parseInt("zz",36);      // 1295 (35*36+35)
parseInt("077",8);      // 63 (7*8+7)
parseInt("077",10)      // 77 (7*10+7)
```

#### 3.8.3 对象转换为原始值
> 所有的对象集成了两个转换方法  
> toString()：它的作用是返回一个反映这个对象的字符串。  
> valueOf()：如果存在任意原始值，他就默认将对象转换为表示它的原始值。对象是复合值，而且大多数对象无法真正表示一个原始值，因此默认的valueOf()方法简单的返回对象本身，而不是返回一个原始值。
``` javascript
// toString()
[1,2,3].toString();                // 1,2,3
(function(x){f(x);}).toString();   // function(x){\n f(x);\n}
/\d+\/g.toString();                // /\\d+/g
new Date(2010,0,1).toString();     // Fri Jan 01 2010 00:00:00 GMT+0000 (UTC)

// valueOf()
var d = new Date(2010,0,);        // 2010-01-01T00:00:00.000Z
d.valueOf();                      // 1262304000000

// 日期对象和“+”、“-”，“==”、“>”的运行结果
var date = new Date();          // 创建一个日期对象
typeof (date + 1);              // "string"：“+”将日期转换为字符串
typeof (data - 1);              // "number"：“-”使用对象数字的转换
date == date.toString();        // true：隐式的和显式的字符转换
date > (date - 1);              // true：“>”将日期转换为数字
```

### 3.9 变量声明
> js程序中，使用一个变量之前应当先声明，变量是使用关键字`var`来声明的。  
``` javascript
var i;
var sum;

// 可以同时声明多个变量
var i,sum;

// 将变量的初始复制和变量声明写在一起
var message = "hello";
var i = 0; j = 0; k = 0;
```
**重要的声明和遗漏的声明**
> 如果你师徒读取一个没有声明的变量的值，js会报错。  
> 在非严格模式下，如果给一个为生命的变量赋值，js实际上会给全局对象穿件一个同名属性，并且它工作起来像一个真正声明的全局变量。这意味着你可以侥幸不声明变量，但这是一个不好的习惯会造成很多bug，因此，你应该当使用使用var来声明变量。  

### 3.10 变量作用域
> 一个变量的作用域(scope)是程序源码中定义这个变量的区域。  
> 全局变量拥有全局作用域，在js代码中的任何地方都是由定义的。  
> 然而在函数内声明的变量只在函数体内由定义，他们是局部变量，作用域是局部性的。  
> 函数参数也是局部变量，他们只在函数体内由定义。

``` javascript
// 在函数体内，局部变量优先级高于全局变量，如果重名，全局变量会被局部变量覆盖
var scope = "global";       // 全局变量
function checkScope(){
  var scope = "local";      // 局部变量
  return scope;
}
checkScope();               // local

// 全局作用域编写代码是可以不谢var语句，但局部变量必须使用var语句
scope = "global";         // 全局变量
function checkScope(){
  scope = "local";        // 修改了全局重名的变量
  myScope = "local";      // 显式的声明了一个全局变量
  return [scope,myScope]
}
checkScope();             // ["local","local"]：产生了副作用
scope;                    // local：全局变量被局部变量给修改了
myScope;                  // local：全局命名空间搞乱了

// 函数定义是可以嵌套的。会出现几个布局作用域嵌套的情况
var scope = "global scope";     // 全局变量
function checkScope(){
  var scope = "local scope";    // 局部变量
  function nested(){
    var scope = "nested scope"; // 嵌套作用域内的局部变量
    return scope;
  }
  return nested();
}
checkScope();                   // nested scope
```