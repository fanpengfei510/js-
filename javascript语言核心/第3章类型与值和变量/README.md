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
> js对象是一种复合值：他是属性或已命名值的集合。通过`"."`符号来引用属性值。当属性值是一个函数的时候，称其为方法。通过fn.method()来调用对象fn中的方法。
``` javascript
var str = 'hello world';
var value = str.substring(str.indexOf(" ") + 1,str.length);
console.log(value); // world
```
