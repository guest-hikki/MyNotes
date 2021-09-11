# Javascript基础

### 一、基础概念

1. JS是一种运行在客户端的脚本语言

2. JS的组成：ECMAScript（JS语法）、DOM（页面文档对象模型）、BOM（浏览器对象模型）

3. JS的书写位置：行内（直接在元素属性时设置）、内嵌（在<head>中创建的<script>中书写）、外部（创建.js文件并引入）

4. HTML中使用双引号，JS中使用单引号

5. 注释方法：与C语言相同

6. JS语句后方的分号可加可不加

7. 浏览器：

   > 浏览器可以分为两个部分：渲染引擎和JS引擎
   >
   > * 渲染引擎：用来解析HTML和CSS，俗称内核
   > * JS引擎：称为JS解释器
   
8. Javascript的组成：

   > 1. ECMAScript：JavaScript语法 —— 学习JS的基本语法
   > 2. DOM：页面文档对象模型
   > 3. BOM：浏览器对象模型

9. API：是一些预先定义的函数

   > 简单的来理解API是给程序员提供的一种工具，以便能更轻松的实现想要完成的功能
   >
   > 而Web API：浏览器提供的一套操作浏览器功能（BOM）和页面元素（DOM）的API

### 二、ECMAScript

#### ① - 输入和输出语句

|                    方法                    |                          说明                           |  归属  |
| :----------------------------------------: | :-----------------------------------------------------: | :----: |
|                 alert(msg)                 |                    浏览器弹出警示框                     | 浏览器 |
| console.log(msg) <br>【翻译：控制台.日志】 | 浏览器控制台打印输出信息 （可以通过F12中的Console查看） | 浏览器 |
|                prompt(msg)                 |     浏览器弹出输入框，用户可以输入<br>取值为字符型      | 浏览器 |

#### ② - 声明

> 1. 变量的声明：`var 变量名`
>
> 2. 变量的赋值：`变量名 = 变量取值`
>
>    >  Note:
>    >
>    > 1. 若变量只声明、不赋值，则取值为undefined；
>    > 2. 尽量不要使用name作为变量名
>    > 3. 驼峰命名法：首字母小写，其它单词首字母大写
>
> 3.  集体声明：若要输出多个变量，使用逗号分隔开即可
>
>    ~~~html
>    var a = 9, b = 9, c = 9;            // 集体声明
>    var a = b = c = 9;                  // 相当于var  a = 9;b = 9;c = 9;   >> 其中b和c没有声明
>    ~~~

#### ③ - 数据类型

> 1.  JS属于弱类型语言，不用提前声明数据类型，只有被赋值后，数据类型才会被确定，但确定后，若再给变量赋不同类型的值，变量的类型会发生改变
>
> 2. 简单数据类型（值类型）
>
>    | 简单数据类型 |                             说明                             |  默认值   |
>    | :----------: | :----------------------------------------------------------: | :-------: |
>    |    Number    | 数字型，包含浮点型和整型 八进制：0开头<br>十六进制：0x开头<br>数字型的最大值：Number.MAX_VALUE<br>数值型的最小值：Number.MIN_VALUE<br>无穷大：Infinity<br>无穷小：-Infinity<br>非数字：NaN（Not a Number）<br>判断是否为非数字：isNaN ( ) → 非数字：true \| 数字：false |     0     |
>    |   Boolean    |                           布尔类型                           |   false   |
>    |    String    | 字符串型<br>在字符串中可以使用转义符 字符串长度：String.length<br>字符串拼接：new_str = str1 + 任意类型（通过这个方法控制输出） |    “”     |
>    |  Undefined   | 声明了变量，但没有赋值<br>Undefined + 数字 = NaN Undefined + 字符串 = 'undefined字符串' | undefined |
>    |     Null     |     空值 Null + 数字 = 数字 Null + 字符串 = 'null字符串'     |   null    |
>
>    > 存储位置：栈
>    >
>    > 存储方式：在栈中开辟一个空间存储数据，再将变量名指向栈中开辟的空间
>    >
>    > 传参：在函数传参时，会开辟一个区域存储形参的值并将实参的值赋值给它，故函数中对形参值的修改，对实参没有影响
>
> 3.  复杂数据类型（引用数据类型）：，通过new关键字创建的对象，在存储时变量中存储的仅仅是地址（引用）
>
>     如：[Object](#object)、[Array](#array)、[Date](#date)、[Math](#math)
>
>     > 存储位置：堆
>     >
>     > 存储方式：在堆中开辟一段空间存储数据，再在栈中开辟一个空间保存堆中开辟空间的地址，最后将变量名指向栈中存储的堆地址
>     >
>     > 传参：在函数传参时，会开辟一个区域存储形参的值并将实参的值赋值给它，此时，实参的值为堆中的地址。然后函数中对形参属性的修改是直接对堆中存储的数据进行修改，因为实参和形参存储的堆地址相同，所以通过实参进行存储的值也会被修改
>
> 4.  基本包装类型：把简单数据类型包装为复杂数据类型，这样这个简单数据类型就能使用属性和方法了
>
>     > 基本包装类型的种类：String、Number、Boolean
>
> 5. `typeof 变量`：检测变量类型
>
> 6. 数据类型转换：
>
>    > * 转换为字符串类型：
>    >
>    >   方式一：变量.toString( )
>    >
>    >   方式二：String(变量)
>    >
>    >   方式三【重点】：加号拼接字符串，即加上一个空字符串
>    >
>    > * 转换为数字型：
>    >
>    >   方式一：【重点】parseInt(变量)  >> 转换为int类型  
>    >
>    >   > 字符串：以数字开头将只保留前面的数字；如果以其它元素开头，将返回NaN~[注：NaN也为数字型]~
>    >   >
>    >   > bool：将转换为NaN
>    >
>    >   方式二：【重点】parseFloat(变量)  >> 转换为float类型
>    >
>    >   > 字符串：以数字开头将只保留前面的数字，如果以其它元素开头，将返回NaN
>    >   >
>    >   > bool类型：将转换为NaN
>    >
>    >   方式三：Number(字符串) 
>    >
>    >   > 只要不是全为数字的字符串，都将转换为NaN
>    >
>    >   方式四：利用除”+“以外的算数运算符进行隐式转换
>    >
>    >   > 如"123"*1 或 ”123“ - “12”  >> 只要不是全为数字的字符串，都将转换为NaN  
>    >
>    > * 转化为bool型：Boolean(变量) 
>    >
>    >   > 代表空、否定的值（''、0、NaN、null、undefined）将被转化为false；其它将转换为true

#### ④ - 运算符

> * 算术运算符：`+`、`-`、`*`、`/`、`%`
>
> * 递增运算符：`++`、`--`
>
> * 比较（关系）运算符：`<`、`>`、`>=`、`<=`、`==`、`!=`、`===`、`!==`
>
>   > Note：
>   >
>   > 1. `==`和`!=`会默认使用隐式转换，如：`18=='18'`为`true`
>   > 2. `===`、`!==`则不会采取隐式转换，即可以判断运算符两边的取值和数据类型是否一致，如：`18==='18'`为`false`
>
> * 逻辑运算符：`&&`、`||`、`！`
>
>   > Note：
>   >
>   > 1. 表达式1`&&`表达式2：如果表达式1为真，则返回表达式2；如果表达式1为假，则返回表达式1，且不会去执行表达式2的操作
>   > 2. 表达式1` || `表达式2：如果表达式1为真，则返回表达式1，且不会去执行表达式2的操作；如果表达式1为假，则返回表达式2
>
> * 赋值运算符：`=`、`+=`、`-=`、`*=`、`/=`、`%=`
>
>   >  *运算符的优先级：括号 > 一元运算符 > 算数 > 关系 (>) > 相等(!=) > 逻辑 > 赋值(=) > 逗号* 

#### ⑤ - 流程控制：与C语言语法相同

> * 条件判断：if语句；if-else语句；switch-case语句；?:语句
> * 循环控制：for循环语句；while循环语句；continue语句；break语句
> * Note：
>   1. switch语句匹配是全等匹配
>   2. 设置断点：点击F12 >>点击Sources>>设置断点>>刷新浏览器开始执行

#### ⑥ - 数组

> * 创建数组：
>
>   方法一：`var arr = new Array()`
>
>   方法二：`var 数组名 = [];var 数组名 = [ 'hikki'，1，2，true];`// 先初始化再赋值
>
> * 访问数组元素：数组名[索引号]
>
> * 获取数组元素长度：数组名.length
>
> * 新增数组元素
>
>   方法一：修改数组长度，为赋值的元素值为undefined
>
>   方法二：直接给以添加新增的索引号为下标的元素赋值

#### ⑦ - 函数

> * 声明：
>
>   ~~~javascript
>   /* 命名函数 */
>   function 函数名(参数1, 参数2, …) { 函数体 }
>   /* 匿名函数 */
>   var 变量名 = function(参数1, 参数2, …) { 函数体 }        //变量名不是函数名，该函数没有函数名
>   ~~~
>
> * 调用
>
>   ~~~javascript
>   /* 命名函数 */
>   函数名(参数1, 参数2, …)
>   /* 匿名函数 */
>   变量名(参数1, 参数2, …)
>   ~~~
>
> * 函数形参与实参不匹配问题：
>
> 1. 若 实参数 = 形参数       >> 正常匹配
> 2. 若 实参数 > 形参数       >> 丢弃多余的实参值
> 3. 若 实参数 < 形参数       >> 未匹配的形参未定义（undefined）
>
> * 返回值：若函数体中没有使用return，则返回undefined
>
> * 函数的arguments对象：为一个伪数组对象，存储了函数传递过来的**实参的值**，可以在不指定传参数量的情况下使用
>
> * 作用域：
>
>   > - 分类（es6之前）：全局作用域、局部作用域
>   > - 全局作用域：整个`<script>`标签内或是整个js文件都有效
>   > - 局部作用域：函数内部有效
>   > - 全局变量：函数外部的变量、函数内部没有声明直接赋值的变量（浏览器关闭时销毁）
>   > - 局部变量：在函数内声明的变量、函数的形参（程序执行完毕时销毁）
>   > - 作用域链：内部函数访问外部函数的变量，采取的是链式查找（一层一层查找父函数是否有所需的变量）的方式来决定取值。

#### ⑧ - 预解析

- JS解释器在运行代码时，会分为两个步骤：先进行预解析，再进行代码逐行执行
- 预解析机制：js引擎会把js里面所有的var和function提升到当前作用域的最前面
- 变量提升：把所有的变量声明提升到当前作用域的最前面，但是不会提升赋值操作。注意：函数表达式是采取变量提升方式，故调用函数表达式声明的函数必须先声明再调用
- 函数提升：把所有的函数声明提升到当前作用域的最前面

#### ⑨ -  <span id="object">自定义对象（object）</span>

1. 概念：

   > - 对象：一组无序的相关属性和方法的集合，所有的具体事物都是对象
   > - 属性：事物的特征（用名词表示）
   > - 方法：事物的行为（用动词表示）

2. 创建：

   >  1. 利用字面量创建对象：
   >
   >       ~~~javascript
   >       var  对象名 = {         
   >              属性 ：属性值，
   >              行为：匿名函数
   >       }       
   >       ~~~
   >
   >   2. 利用new Object创建对象
   >
   >       ~~~javascript
   >       var 对象名 = new Object();
   >       对象名.属性 = 属性值
   >       对象名.方法名 = function(参数){函数体}         // 等号后接匿名函数
   >       ~~~
   >
   >   3. 利用构造函数创建对象（构造函数：把对象的属性和方法抽象出来，类比于“类”，封装到函数里面。一般首字母大写）
   >
   >       ~~~javascript
   >       /* 创建构造函数 */
   >       function 构造函数名(参数){
   >           this.属性 = 属性值        
   >           this.方法名 = function(参数){函数体}      // 等号后接匿名函数
   >       }
   >       /* 使用构造函数创建对象 */
   >       var 对象名 = new 构造函数名(参数)           
   >       // Note： new会创建一个空对象，然后使用this会指向这个对象，再执行构造函数中的代码，给这个对象添加属性和方法，然后返回这个对象     
   >       ~~~
   >
   
3. 调用属性：

   > 方法一：对象名.属性名
   >
   > 方法二：对象名[ '属性名' ]

4. 调用对象:

   > 对象名.方法名(函数参数)

5. 使用`for_in`循环遍历对象

   ~~~javascript
   for  (var key in 对象名){
     //在for循环内部，key得到的是属性名，对象名[key]得到的是属性值
     console.log(key)            // 得到的是对象里所有的属性名
     console.log(对象名[key])     // 得到的是对象里所有的属性值
   }
   ~~~

#### ⑩ - 内置对象

##### -- <span id="math">数学对象：Math</span>

~~~javascript
<script>
        // 圆周率
        console.log(Math.PI)
        // 取最大值
        console.log(Math.max(1, 3, 5, 7, -9))
        // 取最小值
        console.log(Math.min(1, 3, 5, 7, -9))
        // 绝对值
        console.log(Math.abs(-1))
        // 向上取整
        console.log(Math.ceil(1.1))
        // 向下取整
        console.log(Math.floor(1.1))
        // 四舍五入取整 >> 遇到.5或以上的情况向上取值；反之向下取整
        console.log(Math.round(1.5))            // 2
        console.log(Math.round(-1.5))           // -1
        // 开方
        console.log(Math.sqrt(4))
        // 指数计算
        console.log(Math.pow(4, 1.5))
        // 【重要】获取0到1之间的随机数 = [0,1)
        console.log(Math.random())
        // 获取两个整数之间的随机整数，并且包含这两个数
        function getRandom(min, max) {
            return Math.floor(Math.random() * (max - min + 1)) + min;
        }
        console.log(getRandom(1, 10))
</script>
~~~

##### -- <span id="date">日期对象：Date</span>

~~~javascript
<script>
    /* Date()日期对象 是一个构造函数 必须使用new来调用创建我们的日期对象 */
    // 不使用参数获得的是当前日期
    var date = new Date()
    console.log(date)
    // 使用参数常用的写法：1.数字型：2002, 12, 26 ；2.字符串型：'2002-12-26 8:8:8'
    var date_bir_01 = new Date(2002, 12, 26)   // 输出的月份为实际月份+1  >> Sun Jan 26 2003 00:00:00 GMT+0800 (中国标准时间)
    console.log(date_bir_01)
    var date_bir_02 = new Date('2002-12-26 8:8:8')
    console.log(date_bir_02)
    /* 格式化日期 */
    console.log(date.getFullYear())         // 返回年份
    console.log(date.getMonth() + 1)        // 返回月份(0月~11月) 故要给输出的月份+1才会输出正确月份
    console.log(date.getDate())             // 返回日期
    console.log(date.getDay())              // 返回星期 注意: Sunday返回为0
    /* 格式化时间 */
    console.log(date.getHours())            // 返回小时数
    console.log(date.getMinutes())          // 返回分钟数
    console.log(date.getSeconds())          // 返回秒数
    /* 获取时间戳 */
    // 方法一：通过vauleOf() getTime()
    console.log(date.valueOf())
    console.log(date.getTime())
    // 方法二：最常用的写法
    var timestamp = +new Date()
    console.log(timestamp)
    // 方法三：H5新增写法
    console.log(Date.now())
</script>
~~~

##### -- <span id = "array">数组对象：Array</span>

> 1. 创建：
>
>    ~~~javascript
>    var arr_01 = new Array(2)                // 创建一个有两个空元素的数组
>    var arr_02 = new Array(2, 5, 8)          // 创建一个内含2，5，8三个元素的数组
>    ~~~
>
> 2. 方法:
>
>    | 作用                                            | 方法                                                         | 参数                                                         |
>    | :---------------------------------------------- | :----------------------------------------------------------- | ------------------------------------------------------------ |
>    | 判断是否为数组                                  | Array.isArray(obj) <br>【等效于：obj instanceof Array】      | obj：需要检测的值                                            |
>    | 在数组末尾添加元素，<br>返回新数组的length属性  | arr.push(element1, …, elementN)                              | element：被添加到数组末尾的元素                              |
>    | 在数组头部添加元素，<br/>返回新数组的length属性 | arr.unshift(element1, …, elementN)                           | element：被添加到数组末尾的元素                              |
>    | 删除数组的最后一个元素，<br>返回其删除的元素    | arr.pop( )                                                   | 无                                                           |
>    | 删除数组头部的第一个元素，<br/>返回其删除的元素 | arr.shift( )                                                 | 无                                                           |
>    | 翻转数组 ，<br>且会修改原数组的值               | arr.reverse( )                                               | 无                                                           |
>    | 数组排序                                        | arr.sort([compareFunction])                                  | compareFunction[可选]： <br/>用来指定按某种顺序进行排列的函数 <br/>默认按照各个字符的Unicode位点排序 |
>    | 返回字符串中是数据的索引号 【从头到尾】         | arr.indexOf(searchValue[, fromIndex])                        | earchValue：待查找字符串的值 <br/>fromIndex[可选]：开始查找的位置 |
>    | 返回字符串中是数据的索引号 【从尾到头】         | arr.lastindexOf(searchValue[, fromIndex])                    | earchValue：待查找字符串的值 <br/>fromIndex[可选]：开始查找的位置 |
>    | 返回数组的字符串形式                            | arr.toString( )<br> 如：[0,1,2,3] -> '0,1,2,3'               | 无                                                           |
>    | 返回使用分隔符转换的字符串                      | arr.join([separator])                                        | separator[可选]：指定的分隔符 <br>默认为`,`                  |
>    | 返回拼接的多个数组 ，<br/>但不会修改原数组的值  | var new_arr = old_arr.concat (value1[, value2[, …[, valueN]]]) | value：拼接的数组或值                                        |
>    | 返回数组的子数组                                | arr.slice([begin[, end]])                                    | begin：开始提取字符的位置（索引值）<br/> end[可选]：结束位置的索引值 <br>默认提取值末尾 |
>    | 修改数组段 ，<br/>且会修改原数组的值            | arr.splice(start[, deleteCount[, item1[, item2[, ...]]]])    | start：指定修改的开始位置 <br/>deleteCount[可选]：表示要移除的数组元素的个数 <br/>item[可选]：要在start位置添加的元素 |
>
> 3. 纯数字数组的排序方法：
>
>    ~~~javascript
>    // 纯数字数组的升序排序
>    arr.sort(
>        function (a, b) {
>            return a - b
>        }
>    )
>    // 纯数字数组的降序排序
>    arr.sort(
>        function (a, b) {
>            return b - a
>        }
>    )
>    ~~~

##### -- 字符串对象

> * 不可变性：字符串里面的值不可变，若是对这个值进行修改，则会重新开辟一段内存，存储新的数据，并把字符串的变量指向新开辟的地址，原有地址中值并不会销毁。所以字符串中所有的方法，都不会修改字符串本身，而是重新生成一个字符串
>
> * 方法：
>
>   |                  作用                   |                            方法                            |                             参数                             |
>   | :-------------------------------------: | :--------------------------------------------------------: | :----------------------------------------------------------: |
>   | 返回字符串中是数据的 索引号【从头到尾】 |           str.indexOf(searchValue[, fromIndex])            | searchValue：待查找字符串的值 <br/>fromIndex[可选]：开始查找的位置 |
>   | 返回字符串中是数据的 索引号【从尾到头】 |         str.lastindexOf(searchValue[, fromIndex])          | searchValue：待查找字符串的值<br/> fromIndex[可选]：开始查找的位置 |
>   |          返回拼接的多个字符串           | str.concat(str2, [,…strN])<br> 【等效于：str+str2+…+strN】 |            str2, [,…strN]：需要连接到str的字符串             |
>   |            返回字符串的子集             |                str.substr(start[, length])                 | start：开始提取字符的位置（索引值）<br> length[可选]：提取的字符数（默认提取值末尾） |
>   |            返回字符串的子串             |             str.slice(beginIndex[, endIndex])              | beginIndex：开始提取字符的位置（索引值） <br>endIndex[可选]：结束位置的索引值 （默认提取值末尾） |
>   |          返回指定位置上的字符           |       str.charAt(index)<br/> 【等效于：str[index]】        |                   index：返回字符的索引值                    |
>   |      返回指定位置上字符的 ASCII码       |                   str.charCodeAt(index)                    |                   index：返回字符的索引值                    |
>   |         返回替换后字符串中的 值         |    str.replace(regexp\|\|substr, newSubStr\|\|function)    | regexp：正则表达式对象或者其字面量<br> substr：被替换的字符串<br/> newSubStr：替换的匹配部分的字符串 <br/>function：函数的返回值作为newSubStr的值 |
>   |           将字符串转化为数组            |                      str.split(limit)                      |                        limit：分隔符                         |

### 三、DOM

#### ① - 介绍

1. 简介：文档对象模型，是处理可扩展标记语言的标准编程接口

2. 作用：可以通过这些DOM接口改变网页的内容、结构和样式

3. <span id="DOMTree">DOM树</span>：

   ![image-20210810225536810](images/Javascript基础/image-20210810225536810.png)

4. Script标签的位置：因为为我们文档页面是从上往下加载，所以先得载入标签，在通过DOM修改。故script标签写在修饰的标签下面、body标签的内部

#### ② - DOM元素

1. 获取元素：

   > - 使用id获取标签：[document.getElementById(id)](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/getElementById)
   > - 使用标签名获取标签：[baseElement.getElementsByTagName(name)    ](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/getElementsByTagName)  →  baseElement：标签的父元素
   > - 使用类名获取标签（H5）：[document.getElementsByClassName(name)](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/getElementsByClassName)
   > - 获取第一个指定选择器的对象（H5）：[document.querySelector(selectors)](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/querySelector)
   > - 获取所有指定选择器的对象（H5）：[document.querySelectorAll(selectors)](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/querySelectorAll)
   > - 获取body标签：[document.body](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/body)
   > - 获取html标签：[document.documentElement](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/documentElement)

2. 操作元素

   > * 获取元素内容：可读写
   >
   >   > - 获取从标签起始位置到最终位置的内容（不识别HTML标签且会去除换行和空格）：[element.innerText](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLElement/innerText)
   >   > - 获取从标签起始位置到最终位置的内容（识别HTML标签且不会去除换行和空格）：[element.innerHTML](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/innerHTML)
   >
   > *  获取元素属性：不可以操作自定义属性
   >
   >   > - 通过【元素.属性】的方式可以获取属性值：适用于样式较少的情况
   >   > - 在CSS中设置预定修改的样式类，通过【元素.className（class为保留字，故不能直接使用class）】的方式修改类名，若要保留原先的类名，则使用多类名选择器的方法，在原先类名的后方添加类名：适用于样式较多的情况
   >
   > * 操作元素属性：保存和使用一些数据
   >
   >   > - 设置自定义属性：直接在标签里面使用自定义的属性名即可
   >   > - 获取元素指定属性：[Element.getAttribute(attributeName)](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/getAttribute)
   >   > - H5新增的获取元素指定属性方法：标签.dataset.自定义属性名
   >   > - 修改或设定元素指定属性：[Element.setAttribute(name, value)](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/setAttribute)
   >   > - 移除元素指定属性：[Element.removeAttribute(attributeName)](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/removeAttribute)
   >
   > * Note：
   >
   >   > * 自定义属性：程序员为了方便操作自己给标签设定的属性值，而有H5的新规定：自定义属性需要以data-开头
   >   >
   >   > \> dataset：一个以data-开头的所有属性（自定义属性）的集合
   >   >
   >   > \> 若自定义属性名data-后接的属性名含有短横线(-)，则需要将(除data外的)用短横线连结的内容使用驼峰命名法来获取
   >   >
   >   > ​	如：data-list-index-name   >>   dataset.listIndexName

#### ③ - 节点

- 节点概述：DOM树中的所有节点均可以通过JS进行访问，所有HTML元素（节点）均可被修改，也可以创建和删除

- 节点属性：nodeType（节点类型）、nodeName（节点名称）、nodeValue（节点值）

- 节点类型：【主要】元素节点、属性节点、文本节点

- 节点的层级关系：父子兄层级关系（参考[DOM树](#DOMTree)）

- 节点介绍：

  |                             节点                             |                             代码                             |
  | :----------------------------------------------------------: | :----------------------------------------------------------: |
  |               返回指定的节点在DOM树中的父节点                | [Node.parentNode](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/parentNode) |
  | 返回包含指定节点的子节点的集合<br> （包含元素节点和文本节点[如：换行]等等，故不常用） | [Node.childNodes](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/childNodes) |
  | 返回包含指定节点的子元素节点的集合 <br>（非标准，但是常用）  |                        Node.children                         |
  |                  返回指定节点的第一个子节点                  | [Node.firstChild](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/firstChild) |
  |                 返回指定节点的最后一个子节点                 | [Node.lastChild](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/lastChild) |
  |                返回指定节点的第一个子元素节点                |                    Node.firstElementChild                    |
  |               返回指定节点的最后一个子元素节点               |                    Node.lastElementChild                     |
  |                 返回指定节点的上一个兄弟节点                 | [Node.previousSibling](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/previousSibling) |
  |                 返回指定节点的下一个兄弟节点                 | [Node.nextSibling](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/nextSibling) |
  |               返回指定节点的上一个兄弟元素节点               |                 Node.previousElementSibling                  |
  |               返回指定节点的下一个兄弟元素节点               |                   Node.nextElementSibling                    |

  > 因为兼容性原因，我们在开发中一般使用Node.Children[0]和Node.Children[Node.length - 1]来获取第一个和最后一个子元素节点

* 节点操作

  > - 创建节点：[Document.createElement(tagName[, options\])](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/createElement)   >> 创建之后还需要添加节点
  >
  > - 添加节点（从父结点的所有子节点后追加节点）：[parentNode.appendChild(aChild)](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/appendChild)
  >
  > - 添加节点（从父结点的指定子节点前插入节点）：[parentNode.insertBefore(newNode, referenceNode)](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/insertBefore)
  >
  > - 删除节点：[parentNode.removeChild(child)](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/removeChild)
  >
  > - 克隆节点：[Node.cloneNode(deep)](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/cloneNode)
  >
  >   \> deep为空或为false：浅拷贝。只克隆节点本身，不克隆里面的子节点
  >
  >   \> deep为true：深度拷贝。复制节点本身以及里面所有的子节点

* 创建标签：

  > \>> 方法一：使用`parentNode.innerHTML`将标签直接添加至父结点下 
  >
  > 例：`parentNode.innerHTML=”<a href='#'>添加的链接</a>“`
  >
  > Note：创建多个标签可通过拼接数组可提高效率
  >
  > \>> 方法二：使用`document.createElement()`创建标签，再将标签添加至父结点下
  >
  > 例：`var newEle = document.createElement('a')`   >>   `parentNode.appendChild(newEle)`

### 四、事件

#### ① - 事件基础

> - 事件三要素：事件源、事件类型、事件处理程序
> - 事件源：触发事件的对象
>
> - 事件类型：触发事件的动作 —— 如：鼠标点击、鼠标经过、按下键盘等
>
> - 事件处理程序：触发事件后执行的操作
>
> - 执行事件的步骤：
>
>   > 1. 获取事件源
>   > 2. 注册事件
>   > 3. 添加事件处理程序

#### ② - 注册事件

> - 传统方式：事件源.事件类型 = function( ){ }
>
> \> 唯一性：同一个元素同一个事件只能设置一个处理函数，最后设置的处理函数将覆盖前面注册的处理函数
>
> - 方法监听[注册方式](https://developer.mozilla.org/zh-CN/docs/Web/API/EventTarget/addEventListener)：EventTarget.addEventListener(type, listener[, useCapture\])
>
> \> 同一个元素同一个事件可以注册多个监听器，按注册顺序执行
>
> \> type类型：[事件参考](https://developer.mozilla.org/zh-CN/docs/Web/Events) 【最常用：click — 点击，使用时要加引号】

#### ③ - 删除事件

> - 传统方式：事件源.事件类型 = none
> - 方法监听[删除方式](https://developer.mozilla.org/zh-CN/docs/Web/API/EventTarget/removeEventListener) ： EventTarget.removeEventListener(type, listener[, useCapture\])
>
>  \> 该方法使用时第二个参数为函数名，故方法监听注册方式中不能最好不要使用匿名函数

#### ④ - DOM的事件流

> * 事件流：事件的传播过程
> * 三个阶段：
>   1. 捕获阶段：事件从Document（根结点）逐层向下传递，直到Dom树的根结点
>   2. 当前目标阶段：事件源处理
>   3. 冒泡阶段：事件从Dom树的根结点逐层向上传递，直到Document（根结点）
> * 作用：根据设置方法监听注册方式的useCapture参数可以设定处理事件流的阶段，根据阶段不同可以设置发生一次事件，不同的事件源处理的顺序

#### ⑤ - 事件对象

> * 事件对象：存储事件相关数据
>
> * 定义方式：—— 一般命名为event、evt、e
>
>   > 1. 传统方式：放在监听函数的( )内
>   > 2. 方法监听注册方式：再放在监听函数的( )内
>
> * 获取方式：直接通过名称获取
>
> * 事件对象的常见属性和方法
>
>   【鼠标事件】
>
>   |  鼠标事件   |     触发条件     |
>   | :---------: | :--------------: |
>   |   onclick   |     鼠标单击     |
>   | onmouseover |     鼠标经过     |
>   | onmouseout  |     鼠标移开     |
>   |   onfocus   |     获得焦点     |
>   |   onblur    |     失去焦点     |
>   | contextmenu | 唤起鼠标右键菜单 |
>   | selectstart |   鼠标开始选中   |
>   | onmousemove |     鼠标移动     |
>   |  onmouseup  |     鼠标弹起     |
>   | onmousedown |     鼠标按下     |
>
>   > 传统方式定义事件：事件名前加on
>   >
>   > 方法监听事件：事件名前无需加on
>
>   【鼠标事件对象】
>
>   | 鼠标事件对象 |                 说明                  |
>   | :----------: | :-----------------------------------: |
>   |  e.clientX   | 返回鼠标相对于浏览器窗口可视区的X坐标 |
>   |  e.clientY   | 返回鼠标相对于浏览器窗口可视区的Y坐标 |
>   |   e.pageX    |     返回鼠标相对于页面文档的X坐标     |
>   |   e.pageY    |     返回鼠标相对于页面文档的Y坐标     |
>   |  e.screenX   |     返回鼠标相对于电脑屏幕的X坐标     |
>   |  e.screenY   |     返回鼠标相对于电脑屏幕的Y坐标     |
>
>   ---
>
>   【键盘事件】
>
>   |  键盘事件  |                           触发条件                           |
>   | :--------: | :----------------------------------------------------------: |
>   |  onkeyup   |                   某个键盘按键被松开时触发                   |
>   | onkeydown  |                   某个键盘按键被按下时触发                   |
>   | onkeypress | 某个键盘按键被按下时触发 （但是它不能识别功能键，比如ctrl、shift、箭头等） |
>
>   >  事件执行顺序：keydown-keypress-keyup
>
>   【键盘事件对象】
>
>   - keyCode：返回触发键盘事件键位的ASCII码值
>   - 使用onkeyup和onkeydown捕获的事件使用keyCode不会区分大小写，但是onkeypress会