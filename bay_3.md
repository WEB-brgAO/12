## AJAX学习

* 介绍
  * Ajax是一种技术，通过这种技术，也可以实现客户端和服务器的请求响应过程。这一技术的实现，只需要浏览器执行一小段JS代码即可。

### $.AJAX的使用

```js
  $.ajax({
    type: `GET`,
    url: `common/query-post`,
    dataType: "text",
    success: function(ass) {
      console.log(ass);

    }
  })
```



### 认识数据接口

* 其实在向Ajax向服务器发送请求的时候不但可以请求服务器上的文件资源,也可以请求接口

```js
    $.ajax({
        url: '/common/abc', // 这里这样写
        success: function (result) {
            console.log(result);
        }
    });
```

* 接口: 是后端同学写的
* 接口也是一个网址,通过浏览器或者客户端向这个网址发送请求可以获取到接口返回的结果.

> 我们吧接口可以看做一个带有返回值的函数,可以通过客户端访问接口,就相当于调用该函数,并且得到它的返回值
>
> 有些函数调用需要参数   接口也是如此
>
> 对于一般的项目的接口,都会有一个专门的文档来介绍

### 接口文档使用方法

* 接口文档中记载了后端同学提供的接口的详细信息,大致包括,接口地址/作用/请求方式/请求参数/响应结果等等

*  type : "`请求方式`",
* url:"`请求接口`",
* data:"`请求参数`",
* dataType: "`响应数据格式`",
* success : function ( `返回响应值`) { `返回执行函数`}

```js

```

### 使用$.ajax()方法进行ajax请求

#### **type**

* 1.意义
  * 表示请求的方式(method)
* 最常见的两种请求
  * GET
  * POST
* GET和POST的区别
  * 不同点
    * GET : 是获取 得到.这种请求用于向服务器请求资源(图片文件)他是最重点在于,它之请求, 二不会改变服务器上的资源
    * POST : 派送, 投递 , 这种方式的请求用于向服务器上提交数据,它的重点在于,它可能会修改服务器上的资源
  * 相同点
    * GET和POST 请求都可以发送请求时附带一些数据,例如根据用户名去检查这个用户是否被占用; 使用的就是GET方式
    * 这两种方式都可以从服务器获取返回数据

#### **data**

1. 意义
   - 向接口发送请求的时候，携带的数据，也就是接口文档中的请求参数
2. 写法
   - 对象形式，形如： `{name: 'xxx', content: 'xxx'}`
   - 字符串形式，形如： `name=xxx&content=xxx`

> 无论写法如何，实际上发送给服务器的数据都是 字符串形式。多个请求参数之间，使用 & 符号隔开。GET请求的时候，这个字符串和接口之间使用 ? 隔开	

#### **dataType**

1. 意义
   - 服务器响应数据的格式。
   - 指定该项，jQuery会自动将服务器响应的数据处理成JS数据（数组、对象、字符串、布尔等等）
2. 可选的值
   - `json`，它是==最最常见==的数据传输格式。能够以简单的语法表示复杂的数据
   - `text`，表示服务器返回的是文本类型的数据
   - `xml`，表示服务器返回的是xml格式的数据，目前项目中很少使用它了，这里作为了解
   - `jsonp`、`script`、`html`等其他值

> 当我们已经知道了服务器返回数据的格式，则最好指定 `dataType`



**beforeSend**

1. 意义
   - 在发送Ajax请求之前，允许我们做一些事情
2. 语法

```js
$.ajax({
    beforeSend: function () {
        // 发送请求之前，你需要做什么？可以写到这里
    }
});
```

**complete**

1. 意义
   - 在Ajax请求结束之后，允许我们做一些事情
2. 语法

```js
$.ajax({
    complete: function () {
        // Ajax请求结束了，你想做什么？可以写到这里
    }
});
```



### 使用原生jS来进行AJAX请求

> 元生AJAX实现, 是基于浏览器内置对象XHM.HTTPRequest提供的API实现的.
>
> 

#### 基础语法

#### 1.GET 的方式写法

```js
// 1. 实例化 XMLHttpRequest对象
var xhr = new XMLHttpRequest();
// 2. 通过 open(请求方式, url) 方法，设置请求方式和url
xhr.open('GET', '/common/time');
// 3. 调用 send() 方法，发送请求。 ---> 此步骤，表示开始发送请求
xhr.send();
// 4. 准备一个事件，当请求响应过程结束后，会触发该事件；在事件处理函数中，接收服务器响应的结果
xhr.onload = function () {
    // 使用 xhr.response; 来接收结果
    console.log(xhr.response);
}
```

如果有请求参数的情况添加到请求连接?后 键值对以&符号隔开

```js
xhr.open('GET', '接口地址?参数=值&参数=值....');
```

#### 2.POST方式写法

​	和**GET 请求相比**, 多了一行代码,并且**请求参数的位置**发生变化

```js
var xhr = new XMLHttpRequest();
xhr.open('POST', '/message/addMsg');
// 相比GET方式，POST方式多下面一行代码

xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');

//参数部分需要写到send请求当中 也是以字符串的形式
xhr.send('name=李白&content=举杯邀明月');
xhr.onload = function () {
    console.log(xhr.response);
}
```



#### 原生AJAX 请求中的GET和POST的区别

* 原生GET请求
  * 参数是拼接到url中(url?name=张三&aeg=22)
* 原生js的POST请求
  * 需要设置请求头`xhr.setRequestHeader('content-type','application/x-www-form-urlencoded')`
  * 请求参数是写在send()方法中: send(`"name=zhangsan&age=2"`)

```js
var xhr = new xhr()对象
xhr.posh("请求方式","接口地址");
xhr.send()发送请求
xhr.onload=fun fn(){
    //回调函数中this.respobangs是数据库返回的值
    this.ruspobangs
}
```

### 浏览器中的小问题

#### readyState   和  onreadystatechange

##### readyState   属性

* 既然Ajax请求是一个耗时的操作也就是创建xhr对象,然后调用open/调用send发送请求到服务器(耗时操作)  /  接收到服务器返回的数据  / 完全接受到服务器返回的数据  / 这一整个过程都是耗时的操作  . 即使网速再快也需要时间.
* 换句话说, 在执行AJAX请求响应的剁成中要经历好几个阶段xhr对象提供了一个新的属性  sradyState  ,用它来表示Ajax请求到了那个阶段了

输入xhr.readyState 会得到 0 1 2 3 4 这几个数字

| readyState | 状态描述         | 说明                                                         |
| ---------- | ---------------- | ------------------------------------------------------------ |
| 0          | UNSENT           | 代理（XHR）被创建，但尚未调用 `open()` 方法。                |
| 1          | OPENED           | `open()` 方法已经被调用，建立了连接。                        |
| 2          | HEADERS_RECEIVED | `send()` 方法已经被调用，并且已经可以获取状态行和响应头。    |
| 3          | LOADING          | 响应体（服务器返回的数据）下载中， `responseText` 属性可能已经包含部分数据。 |
| **4**      | **DONE**         | **响应体（服务器返回的数据）下载完成，可以直接使用 responseText或response 获取完整的结果。** |

> 一般不会说Ajax请求响应的几个阶段  , 大多数都说Ajax的几个状态,
>
> **如果请求的数据过大**浏览器就会分配获取请求过来的数据
>
> 这样状态3就会**触发多次**

##### **onreadystatechange**事件

> onload是H5之后增加的事件  , 但是在H5之前  , 都是使用
>
> onreadystatechange事件.

* `on...` 表示一个事件 翻译过来就是"当..时候"  , `readyState` 前面说过,他是一个状态,他就是以数字来表示请求的状态,`change`是改变的意思   ,就是说当Ajax状态发生变化的时候,就会触发这个事件.

```js
var xhr = new XMLHttpRequest()；
// 创建对象后，先打印一次XHR对象的状态，此时状态值为0
console.log(xhr.readyState); // 0

// 添加事件onreadystatechange，每当XHR对象的状态发生变化的时候，就会触发这个事件
// 比如
// xhr对象的状态从0-->1，会触发下面的事件
// xhr对象的状态从1-->2，会触发下面的事件
// xhr对象的状态从2-->3，会触发下面的事件
// xhr对象的状态从3-->4，会触发下面的事件
xhr.onreadystatechange = function () {
    console.log(this.readyState); 
    // 输出1/2/3/4
}
// open 方法的第一个参数的作用就是设置请求的 method
xhr.open('POST', '/query-post')
// 设置 Content-Type 为 application/x-www-form-urlencoded，这行代码不用死记硬背，去复制即可
xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
// 需要提交到服务端的数据可以通过 send 方法的参数传递
// 格式：name=zhangsan&age=18
xhr.send('name=zhangsan&age=18');

```

#### IE中的缓存问题

* 只是IE浏览器会有缓存问题,
* 缓存问题指的是: 两次或者多次AJAX GET请求   **同一个**  URl , IE浏览器在第二次请求的时候 , 并不会重新想服务器发起请求,二三直接使用上次请求的结果.

**解决问题**

* 因为是浏览器会把相同的URL请求认为是重复请求
* 那么就在发送请求的时候使用不同的参数使之URL变得不同,这样就可以解决缓存问题

### 其他API

#### 创建XHR对象的兼容性问题

>  XMLHttpRequest 在老版本浏览器（IE5/6）中有兼容问题，可以通过另外一种方式代替。

```js
var xhr = window.XMLHttpRequest ?
    new XMLHttpRequest() : new ActiveXObject('Microsoft.XMLHTTP')
// xhr 的成员相同，即后续的open、send方法一样使用、onreadystatechange
```

#### responseType

`responseType`  表示预期服务器返回的数据类型 当设置了该属性后, 通过`response` 接收数据的时候 , 会根据该属性的值来自动处理为js能够识别的数据

> responseType  相当于   $.Ajax()方法中的dataType

比如 , 当设置了`responseType = "json"` 后 ,使用  `response`   来接收服务器返回的数据时 , 会自动处理成json 数据为js数组 免去了JSON.pares()

* ""   -------空 ,    表示文本 ,   和text 一样   . 空位默认值; 默认为字符串
* text   - -  -  文本数据  
* json  -  - JSON 格式数据
* document    -- **文档对象** . 当返回结果是XML类型的收, 需要制定为document类型

```js
var xhr = new XMLHttpRequest();
xhr.onload = function () {
    // 因为指定了responseType为json。所以ajax会自动将服务器返回的结果当做json来处理
    // 会自动调用JSON.parse来将结果处理成JS数据
    console.log(this.response);
}
xhr.open('GET', '/getMsg');
// send之前，指定预期服务器返回数据的类型
xhr.responseType = 'json'; // 可选的值 '' 、 text 、 json 、 document
xhr.send();
```

####  原生AJAX 小结

XHR有两个版本

* XHR 1.0版本  -----最初XHR对象提供的AIP , 基本上兼容所有的浏览器
  * open() -----设置请求方式 / 请求url   同步或异步
  * send()  -----发送请求
  * readyState()  ---- Ajax 的状态(0 1 2 3 4 )
  * onreadystatechange   --当readyState的值被重新赋值的时候, 都会触发这个事件
  * responText   ---用于接收服务器返回的`文本类型`结果
* XHR 2.0 新增API，基本上不再支持IE6、IE7、IE8
  - **onload**（2014年新增） -- 当请求响应成功了，会触发
  - onprogress -- 当响应的数据，正在接收中，会触发。数据量比较大的话，可能会触发多次，可以使用它做一个进度条
  - onloadstart -- 当请求开始的时候，会触发
  - onloadend -- 当请求结束的时候，会触发
  - **response** ：可以接收任何的响应结果
  - responseType（2012年新增）：配合response使用的一个属性

> 实际开发中 , 使用原生Ajax 的概率非常少 , 一般使用封装好的库,, 比如JQuery中的$.ajax()

### 同步和异步

#### 异步操作

> 异步指的是一段耗时的js代码在执行的时候不会阻塞后续代码的执行

**异步操作的本质是同一个时间点, 有多个操作同事执行; 耗时操作并不会阻塞后面的代码执行**

```js
// 执行一个输出
console.log(111);

// 中间是一个耗时的ajax请求
var xhr = new XMLHttpRequest();
xhr.open('GET', '/common/time');
xhr.send();
xhr.onload = function () {
    console.log(333);
}

// 再执行一个输出
console.log(222);
```



#### 同步操作

> 既然异步操作指的是在同一个时间点可以同时执行多个操作,那么**同步操作** 指的就是在同个时间点只能执行一个操作

```js
// 执行一个输出
console.log(111);

// 中间是一个耗时的ajax请求
var xhr = new XMLHttpRequest();
xhr.open('GET', '/common/time', false);
xhr.onload = function () {
    console.log(333);
}
xhr.send();

// 再执行一个输出
console.log(222);
```



### FormData对象

Date() --日期

Data() --数据

FormData()  是H5 中新增的一个内置对象

> FormData()对象用以将数据编译成键值对, 以使用`XMLHttpRequest`来发送数据.其主要用于发送表单数据, 但亦可用于发送带键值对数据(keyd data) 二独立于表单使用
>
> 以前的AJAX操作只能提交字符串,现在可以提交**二级制**的数据

##### 使用方法1(有form表单)

```js
<form id="fm">
    <input type="text" name="user"><br>
    <input type="password" name="pwd"><br>
    <input type="radio" name="sex" value="男" checked>男
    <input type="radio" name="sex" value="女">女<br>
    <input type="file" name="pic"><br/>
    <input type="button" id="btn" value="提交">
</form>

<script>
    // 当点击提交按钮的时候，需要把表单各项的值，提交给fd接口。
        document.getElementById('btn').onclick = function () {
            // 获取各项值
            /* var user = document.getElementsByName('user')[0].value;
            var pwd = document.getElementsByName('pwd')[0].value; */

            // FormData 专门用于收集表单各项值
            // 1. 有表单，找到表单
            var form = document.getElementById('fm');
            // 2. 实例化FormData，将表单的DOM对象传入即可
            var fd = new FormData(form); // fd对象中包含了表单所有的值

            // 将各项值发送给fd接口
            var xhr = new XMLHttpRequest();
            xhr.open('POST', '/fd');
            // xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
            xhr.responseType = 'json';
            xhr.send(fd);
            xhr.onload = function () {
                console.log(this.response);
            }
        }
</script>
```

##### 使用方法2(没有form表单)



```html
	<form id="fm">
        <input type="text" name="user"><br>
        <input type="password" name="pwd"><br>
        <input type="radio" name="sex" value="男" checked>男
        <input type="radio" name="sex" value="女">女<br>
        <input type="file" name="pic"><br />
        <input type="button" id="btn" value="提交">
    </form>

    <script src="/jquery.js"></script>
    <script>

        $('#btn').click(function () {
            var fm = $('#fm');
            var fd = new FormData(fm[0]); // 这里fm必须是DOM对象
            console.log(fd);

            $.ajax({
                type: 'post',
                url: '/fd',

                // 如果data使用的是对象，ajax方法会把对象转成字符串，
                // 即把{name: 'zs', age: 18}转成name=zs&age=18
                // data: {name: 'zs', age: 18}, 
                data: fd,
                // processData: false, 表示不让jQuery把fd对象转成字符串，而是直接发送fd对象
                processData: false,
                // contentType：false，表示不让jQuery去设置content-type，让FormData去处理
                contentType: false,
                success: function (res) {
                    console.log(res);
                }
            });
        });


        // xhr.send('name=zs&age=18');

    </script>
```





### 回调函数是处理异步请求的最佳方案

总结: 

* 回调函数:
  * 回调函数是吧函数当做一个参数传入方法内部
* 异步请求
  * 异步指的在同一个时间执行多次事件
  * 在执行**耗时的操作**的时候会挂起执行,不会影响后面代码的执行

* 解释
  * 如果需要使用到异步请用中的一个变量或者是返回值的时候
  * 就把这个请用封装起来 把另一个函数当做参数传入请求函数当中
  * 当异步请求结束之后会执行传入的回调函数,
  * 但是这个回调函数是有外部使用的  异步请求内部执行,所以可以使用异步请球中的结果和变量,之后这个回调函数return 之后就是处理过异步请求之后的结果.















## 懒加载

###  介绍

* 懒加载就是自动换页  通过检测文档高度来自动按需加载网页内容

> 通过检测文本的卷起高度去知道 网页是否移动到底部
>
> 判断  是否需要加载数据

* 获取三个值==> 通过计算去的到整个页面距离文档底部的距离
  * 1.获取整个浏览器的高度
  * 2.获取整个页面的高度
  * 3.获取页面卷起的高度==> 卷起就是消失在页面顶部的内容高度
* 通过jquery 对象可以使用三个方法去获得这三个高度
  * **浏览器高度** ==>$(window).height();
  * **页面高度**  ==> $(document).height();
  * **卷起的高度**==> $(document).scrollTop();

![](assets\jq01.png)

> 浏览器的可视窗口距离整个页面的底部的距离需要自己设定
> //就是指定当页面距离页面底部多少像素的时候再发生加载这个事情
> //使用if 去判断这个高度是否满足懒加载的条件
>
> 条件== (浏览器的高度+ 卷起的高度 + 设定的高度 >= 浏览器高度)
> //满足这个条件之后就说明整个文档距离底部已经超过或者等于自己设定的一个范围 但是这个条件在使用监听浏览器滚动条的时候会满足多次
> //满足多次则会执行多次事件
> // if(){
>
> }
>
> //

### **出现多次加载问题**?

> 使用开关思想去解决这个bug   在执行这个加载事件的时候给外部声明一个开关为true 在执行整个加载事件时 这个开关为false  在整个加载事件完成之后给这个开关去赋值true  这个开关需要添加到这个条件内部 

### 解决方法:

* **也就是说   加载事件需要满足两个条件**



> 1. **开关为true** 
> 2. **整个页面满足到页面底部的距离 ==> 为自己设定的一个值例如100**



