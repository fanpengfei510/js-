## 第2章 语法结构
> 编程语言的语法结构是一套基础性规则，用来描述如何使用这门语言和编写程序。  
> 作为语法的基础，它规定了注入变量名是什么样的、怎么写注释，以及程序语句之间如何分隔等规则。

### 2.1 字符集
> javascript程序使用Unicode字符集编写的。[资料参考](https://baike.baidu.com/item/Unicode/750500?fr=aladdin)  

#### 2.1.1 区分大小写
javascript是区分大小写的语言，也就是说，关键字、变量、函数名和所有的标识符(identifier)都必须采取一致的大小写形式。  
但需要注意的是，HTML并不区分大小写(尽管XHTML区分大小写)。

#### 2.1.2 空格、换行符和格式控制符
javascript会忽略程序中标识的空格
除了可以识别普通的空格符 ` (\u0020) `，javascript还可以识别如下这些标识空格的字符：
``` javascript
水平制表符 (\u0009)
垂直制表符 (\u000B)
换页符 (\u000C)
不中断空白 (\u00A0)
字节序标记 (\uFEFF)
```

javascript将如下字符识别为行结束符：
``` javascript
换车符 (\u000A)
回车符 (\u000D)
行分隔符 (\u2008)
段分隔符 (\u2029)
```

#### 2.1.3 Unicode转义序列
在有些计算机硬件和软件里，无法显示或输入Unicode字符全集。
``` javascript
// 例如字符的 é 的Unicode转义写法为\u00E9
"café" === "caf\u00E9";   // true
```

#### 2.1.4 标准化
Unicode允许使用多种方法对同一个字符进行编码。  
比如：字符 “é” 可以使用Unicode字符 `\u00E9` 表示，也可以使用普通的ASSCII字符e跟随一个语调符 `u0301`。

### 2.2 注释
javascript支持两种格式的注释
``` javascript
// 当行注释
/* 这里是一段注释 */
/*
 * 这里是块级注释
 * 可以注释多行代码
 */
```

### 2.3 直接量
所谓直接量(literal)，就是程序中直接使用的数据只。
``` javascript
12              // 数字
1.2             // 小数
'hello world'   // 字符串文本
"Hi"            // 字符串文本
true            // 布尔值
false           // 布尔值
/javascript/gi  // 正则表达式直接量(用作模式匹配)
{x:1,y:2}       // 对象
['a','b','c']   // 数组
```

### 2.4 标识符和保留字
javascript标识符必须以`字母`、`下划线(_)`、`美元符号($)`开始。
``` javascript
// 合法的标识符
i
my_js
_number
$str
```

#### 保留字
javascript把一些标识符拿出来用作子集的关键字。因此，就不能在程序中把这些关键字用作标识符。

保留字 | 保留字 | 保留字 | 保留字 | 保留字 
- | - | - | - | -  
break | delte | function | return | typeof 
case | do | if | switch | var
catch | else | in | this | void
continue | false | instanceof | throw | while
debugger | finally | new | true | with
default | for | null | try | class
const | enum | export | extends | import
super |
---

下面的保留字在普通javascript里是合法的，在严格模式下是保留字：
保留字 | 保留字 | 保留字 | 保留字 | 保留字 
- | - | - | - | -  
implements | let | private | public | yield 
interface | package | protected | static
---

javascript预定义了很多全局变量和函数，应当避免把他们的名字用作变量名和函数名：
保留字 | 保留字 | 保留字 | 保留字 | 保留字 
- | - | - | - | -  
arguments | encodeURI | Infinity | Number | RegExp 
Array | encodeURIComponent | isFinite | Object  | String
Boolaen | Error | isNaN | parseFloat  | SyntaxError
Date | eval | JSON | parseInt  | TypeError
decodeURI | EvalError | Math | RangeError  | undefined
decodeURIComponent | Function | NaN | ReferenceError  | URIError

### 2.5 可选的分号
和其他许多编程语言一样，javascript使用分号(;)将语句分隔开。
``` javascript
// 因为两条语句用行亮书写，第一个分号是可以忽略的
a = 3
b = 4;

// 如果按照如下格式书写，第一个分号则不能忽略掉
a = 3; b = 4;
```
> #### 示例
``` javascript
var a
a
=
3
console.log(a)
// javascript将其解析为：
var a; a = 3; console.log(a);

/****************************/

var y = x + f
(a + b).toString();
// javascript将其解析为：
var y = x + f(a + b).toString();

/****************************/

var x = 0   //这里忽略了分号
;[x,x+1,x+2].forEach(console.log);    //前面的分号保证了正确的语句解析

/****************************/

return
true;
// javascript将其解析为：
return; true;

/****************************/

x
++
y
// javascript将其解析为：
x; ++y
```