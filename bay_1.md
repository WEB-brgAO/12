## jQeury 介绍

### jQuery的概念

* jQuery 是一个快速的 简洁的javaScript 的库,其设计的宗旨是"write less , Do More", 即倡导写更少的代码,做更多的事情.
* j就是javaScript : Query 是查询:   意思是查询js   吧js中的DOM的操作做了封装,我们可以快速使用查询到的元素,使用其中的功能.
* jQuery封装了javaScript 里常用的功能代码,优化了DOM操作,事件处理,动画设计和Ajax交互
* 学习jQuery就是学习调用这些函数(方法).

### jQuery 的优点

* 轻量级
* 跨浏览器兼容
* 链式编程,隐式迭代
* 对事件,样式,动画支持,大大简化了DOM操作
* 支持插件拓展开发,有着丰富的第三方的插件    
* 免费,开源



### $ 是jQuery 的一个别名



```js
例如：
	$('div').hide()  ===》 jQuery('div').hied()
```

* $ 是jQuery 中的顶级对象.

#### jQuery对象和DOM对象之间的转化

* DOM对象

```js
1.通过原生js获取到的对象就是DOM对象
例如: varmydiv = document.quertSelector("DIV"); mydiv 就是 一个DOM对象
```

* 转化为jQuery对象

```js
因为jQuery 是通过$符号来获取对象,
    所以把需要转化的对象放到$(DOM对象) 返回值就是转化后的jQuery对象

```



* jQuery对象

```js
1.通过jQuery的方式获取的对象就是jQuery对象
例如: var mydiv = $("div") ; mydiv 就是一个jQuery对象
```

* 转化为DOM对象
  * 因为获取到的jQuery对象都是以数组的形式存在的, 包括获取到一个元素还是多个元素,
  * 故,通过索引和下标的方式可以吧DOM对象从jQuery的数组中选择出来

```js
	$('div')[索引]
	$('div').get(索引)
```

* 为什么以数组的方式存在呢?

  * 是因为jQuery封装之后,给DOM节点封装了很多属性和方法,

  * 如果转化为DOM就不能使用jQuery的属性和方法了

    

  **jQuery中的属性和方法  不能和js原生的方法混用, 需要使用的话需要转换**