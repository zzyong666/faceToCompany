## JavaScript
##### 1.MVVM和MVC的区别？
 MVC：MVC模式可以这样理解，将html看成view;js看成controller，处理用户与应用的交互，响应对view的操作（对事件的监听），调用Model对数据进行操作，完成model与view的同步（根据model的改变，通过选择器对view进行操作）;将js的ajax当做Model，从服务器获取数据，MVC是单向的。
MVVM：它实现了View和Model的自动同步，也就是当Model的属性改变时，我们不用再自己手动操作Dom元素，来改变View的显示，而是改变属性后该属性对应View层显示会自动改变，MVVM是双向的。
##### 2.写一个简单的函数判断类型？

```
Object.prototype.toString.call() //进行判断
```

##### 3.实现简单的数组求和？

```
eval([1,2,3].join("+"))
// 或
arr.reduce((total,item)=>total+=item,0);
```

##### 4.实现简单的数组去重？
基础数据结构数组：

```
[...new Set([...])]或Array.from(new Set(array))(set返回的结构不是数组类型)
```

对象数组类型数组：
```
// 方法一：
      //定义常量 res,值为一个Map对象实例
      const res = new Map();
      //返回arr数组过滤后的结果，结果为一个数组
      //过滤条件是，如果res中没有某个键，就设置这个键的值为1
      return arr.filter((a) => !res.has(a) && res.set(a, 1))
// 方法二：
     //  方法2：利用reduce方法遍历数组,reduce第一个参数是遍历需要执行的函数，第二个            参数是item的初始值
     var obj = {};
     arr = arr.reduce(function(item, next) {
     obj[next.key] ? '' : obj[next.key] = true && item.push(next);
         return item;
     }, []);
```
##### 5.请写出你所知道的元素水平垂直居中？最少两种，三种良好，四种优秀
- ①绝对定位水平垂直居中
```
<div style="
	 position: absolute;
     width: 500px;
     height: 300px;
     margin: auto;
     top: 0;
     left: 0;
     bottom: 0;
     right: 0;
     background-color: green;
     ">水平垂直居中</div>
```
- ② 相对位置50%+margin控制
```
<div style="position: relative;
     width:400px;
     height:200px;
     top: 50%;
     left: 50%;
     margin: -100px 0 0 -200px;
     background-color: red;">水平垂直居中</div>
```
- ③ 相对位置50%+translate位移
```
<div style="position: absolute;
     width:300px;
     height:200px;
     top: 50%;
     left: 50%;
     transform: translate(-50%, -50%);
     background-color: blue;">水平垂直居中</div>
```
- ④ flex 布局居中
```
<div style="display: flex;align-items: center;justify-content: center;">
    <div style="width: 100px;height: 100px;background-color: gray;">flex 布局</div>
  </div>
```
##### 6.Map和Set的区别？
Set 对象类似于数组，且成员的值都是唯一的。
Map 对象是键值对集合，和 JSON 对象类似，但是 key 不仅可以是字符串还可以是对象
##### 7.跨域是什么原因引起？怎么解决？
跨域是指一个域下的文档或脚本试图去请求另一个域下的资源，这里跨域是广义的。
- ① jsonp函数
在HTML DOM中,script标签本身就可以访问其它域的资源，不受浏览器同源策略的限制，可以通过在页面动态创建script标签。
```
var script = document.createElement('script');  
script.src = "http://aa.xx.com/js/*.js";  
document.body.appendChild(script);  
```
- ② iframe实现跨域
基于iframe实现的跨域要求两个域具有aa.xx.com,bb.xx.com这种特点，也就是两个页面必须属于同一个顶级基础域（例如都是xxx.com，或是xxx.com.cn），使用同一协议（例如都是 http）和同一端口（例如都是80），这样在两个页面中同时添加document.domain，就可以实现父页面调用子页面的函数
- ③ 跨域资源共享（CORS）
服务器端对于CORS的支持，主要就是通过设置Access-Control-Allow-Origin来进行的。如果浏览器检测到相应的设置，就可以允许Ajax进行跨域的访问。
- ④ 使用HTML5的window.postMessage方法跨域
window对象新增了一个window.postMessage方法，允许跨窗口通信，不论这两个窗口是否同源。目前IE8+、FireFox、Chrome、Opera等浏览器都已经支持window.postMessage方法。
- ⑤nginx反向代理
##### 8.谈一谈CSS重绘与回流/重排？
会触发重绘或回流/重排的操作
①添加、删除元素(回流+重绘)
②隐藏元素，display:none(回流+重绘)，visibility:hidden(只重绘，不回流)
③移动元素，如改变top、left或移动元素到另外1个父元素中(重绘+回流)
④改变浏览器大小(回流+重绘)
⑤改变浏览器的字体大小(回流+重绘)
⑥改变元素的padding、border、margin(回流+重绘)
⑦改变浏览器的字体颜色（只重绘，不回流）
⑧改变元素的背景颜色（只重绘，不回流）
##### 9.let,var和const有什么区别？
- const定义的变量不可以修改，而且必须初始化
- var定义的变量可以修改，如果不初始化会输出undefined，不会报错。
- let是块级作用域，函数内部使用let定义后，对函数外部无影响。
##### 10.箭头函数和普通函数有什么区别？
主要区别在this指向问题
- ①普通函数的this 指向调用它的那个对象，例如 obj.func ,那么func中的this就是obj
- ②箭头函数不能作为构造函数，不能使用new，没有this，arguments箭头函数，箭头函数的this永远指向其上下文的 this ，任何方法都改变不了其指向，如 call() , bind() , apply()（或者说箭头函数中的this指向的是定义时的this，而不是执行时的this）

```
var name = "The Window";
var object = {
　　　　name : "My Object",
　　　　getNameFunc : function(){
            console.log(this.name); // My Object
    　　　　　return function(){
    　　　　　　　return this.name; // The Window
    　　　　  };
　　　　},
　　　　b: () => {
           return this.name; // the window
       },
       c: function() {
           return () => {
              return this.name; //My Object
          }
       }
}
```

##### 11.谈谈你对闭包的理解？
- 函数声明的时候，会生成一个独立的作用域，同一作用域的对象可以互相访问，作用域呈层级包含状态，形成作用域链，子作用域的对象可以访问父作用域的对象，反之不能；另外子作用域会使用最近的父作用域的对象。
##### 12.谈谈原型链继承的理解？
- 什么是原型链：只要是对象就有原型, 并且原型也是对象, 因此只要定义了一个对象, 那么就可以找到他的原型, 如此反复, 就可以构成一个对象的序列, 这个结构就被称为原型链
所有的实例有一个内部指针(prototype)，指向它的原型对象，并且可以访问原型对象上的所有属性和方法。
##### 13.求数组交集？并集？
① 使用 filter、concat 来计算

```
var a = [1,2,3,4,5]
var b = [2,4,6,8,10]
//交集
// var c = a.filter(function(v){ return b.indexOf(v) > -1 })
var c = a.filter(item=>b.includes(item));
//差集
// var d = a.filter(function(v){ return b.indexOf(v) == -1 });
var d = a.filter(item=>!b.includes(item));
//补集
var e = a.filter(function(v){ return !(b.indexOf(v) > -1) })
.concat(b.filter(function(v){ return !(a.indexOf(v) > -1)}))
//并集
var f = a.concat(b.filter(function(v){ return !(a.indexOf(v) > -1)}));
console.log("数组a：", a);
console.log("数组b：", b);
console.log("a与b的交集：", c);
console.log("a与b的差集：", d);
console.log("a与b的补集：", e);
console.log("a与b的并集：", f);
```

② 借助扩展运算符（...）以及 Set 的特性实现相关计算，代码也会更加简单些

```
var a = [1,2,3,4,5]
var b = [2,4,6,8,10]
console.log("数组a：", a);
console.log("数组b：", b);
var sa = new Set(a);
var sb = new Set(b);
// 交集
let intersect = a.filter(x => sb.has(x));
// 差集
let minus = a.filter(x => !sb.has(x));
// 补集
let complement = [...a.filter(x => !sb.has(x)), ...b.filter(x => !sa.has(x))];
// 并集
let unionSet = Array.from(new Set([...a, ...b]));
console.log("a与b的交集：", intersect);
console.log("a与b的差集：", minus);
console.log("a与b的补集：", complement);
console.log("a与b的并集：", unionSet);
```
#####  14.谈谈localStorage，sessionStorage和cookies的区别？
- ① sessionStorage用于本地存储一个会话（session）中的数据，这些数据只有在同一个会话中的页面才能访问并且当会话结束后数据也随之销毁。因此sessionStorage不是一种持久化的本地存储，仅仅是会话级别的存储。
- ② localStorage用于持久化的本地存储，除非主动删除数据，否则数据是永远不会过期的。
- ③ cookie 数据始终在同源的http请求中携带，即cookie在浏览器和服务器之间来回传递。
#####  15.介绍一下重绘和回流？需要怎么优化？
- ①用transform 代替 top，left ，margin-top， margin-left... 这些位移属性。
- ② opacity 加上 transform: translateZ/3d  这个属性之后便不会发生回流和重绘了。
- ③不要使用 js 代码对dom 元素设置多条样式，选择用一个 className 代替之。
- ④如果确实需要用 js 对 dom 设置多条样式那么可以将这个dom 先隐藏，然后再对其设置。
- ⑤不要使用table 布局，因为table 的每一个行甚至每一个单元格的样式更新都会导致整个table 重新布局。
- ⑥对于频繁变化的元素应该为其加一个 transform 属性，对于视频使用video 标签。


#####  16.谈谈深拷贝和浅拷贝？
浅拷贝：浅拷贝就是对内存地址的复制，让目标对象指针和源对象指向同一片内存空间，当内存销毁的时候，指向这片内存的几个指针需要重新定义才可以使用，要不然会成为野指针。
深拷贝：深拷贝是指拷贝对象的具体内容，而内存地址是自主分配的，拷贝结束之后，两个对象虽然存的值是相同的，但是内存地址不一样，两个对象也互不影响，互不干涉。

#####  17.css有哪些选择器？权重？
选择器类型：
1、ID　　#id
2、class　　.class
3、标签　　p
4、通用　　*
5、属性　　[type="text"]
6、伪类　　：hover
7、伪元素　　::first-line
8、子选择器、相邻选择器
权重计算规则：
1、第一等：代表内联样式，如: style=””，权值为1000。
2、第二等：代表ID选择器，如：#content，权值为0100。
3、第三等：代表类，伪类和属性选择器，如.content，权值为0010。
4、第四等：代表类型选择器和伪元素选择器，如div p，权值为0001。
5、通配符、子选择器、相邻选择器等的。如*、>、+,权值为0000。
6、继承的样式没有权值。
#####  18.说说flex布局？
Flex（Flexible Box），也就是”弹性布局”，它可以很灵活地实现垂直居中、多列布局等自适应问题。而任何一个容器都可以指定为Flex布局。设为Flex布局以后，子元素的float、clear和vertical-align属性将失效。
##### 19.介绍一下盒模型？
①盒模型：内容(content)、填充(padding)、边界(margin)、 边框(border)
②类型： IE 盒子模型、标准 W3C 盒子模型；
③两种盒模型的主要区别是:标准盒模型的宽高是值内容宽高(content) 
④而IE盒模型的宽高是指content+padding+border。
 ⑤设置盒模型的方式是：设置box-sizing box-sizing:content-box  标准盒模型， box-sizing:border-box IE盒模型
#####  20.解释一下变量提升？
在进入一个执行上下文后，先把 var 和 function 声明的变量前置，再去顺序执行代码。
PS：作用域分为全局作用域和函数作用域，用var声明的变量，只在自己所在的所用域有效。
我们举例来看看下面的代码。
示例一

```
console.log(fn); var fn = 1; function fn() { } console.log(fn);
```

相当于

```
var fn = undefined; function fn() { } console.log(fn); fn = 1; console.log(fn);
```

示例二

```
console.log(i); for (var i = 0; i < 3; i++) { console.log(i) }
```

相当于

```
var i = undefined; console.log(i); for (i = 0; i < 3; i++) { console.log(i); }
```

#####  21.如何理解事件委托？
也可以称之为事件代理，给父元素绑定事件，用来监听子元素的冒泡事件，并找到是哪个子元素的事件。将事件委托给另外的元素，利用事件冒泡的特性，将里层的事件委托给外层事件，将事件绑定到目标元素的父节点，根据event对象的属性进行事件委托，改善性能。事件监听器会分析从子元素冒泡上来的事件，找到是哪个子元素的事件。

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>事件委托</title>
</head>
<body>
    <ul id="list">
        <li>我是第一个li</li>
        <li>我是第二个li</li>
        <li>我是第三个li</li>
        <li>我是第四个li</li>
        <li>我是第五个li</li>
    </ul>
</body>
<script>
    window.onload = function(){
        var list = document.getElementById("list");
        var li = document.getElementsByTagName("li");
        list.onmouseover = function(env){
            //  兼容获取event对象
           var env = env || window.event;
          //  兼容获取目标对象   env.target为标准  env.srcElement为IE
           var target = env.target || env.srcElement;
           // 判断目标对象是否是li
           // target.nodeName 可以获取节点名称，通过toLowerCase()可以将节点名称的大小转换为小写
           if(target.nodeName.toLowerCase()=== "li"){
               target.style.background = "red";
           }
        }
    }
</script>
</html>
```



##### 40.谈谈前端性能优化？
- ①减少HTTP请求：合并文件、CSS精灵、inline Image
- ②减少DNS查询：DNS查询完成之前浏览器不能从这个主机下载任何任何文件。方法：DNS缓存、将资源分布到恰当数量的主机名，平衡并行下载和DNS查询
- ③避免重定向：多余的中间访问
- ④使Ajax可缓存
- ⑤非必须组件延迟加载⑦未来所需组件预加载
- ⑥减少DOM元素数量
- ⑦将资源放到不同的域下：浏览器同时从一个域下载资源的数目有限，增加域可以提高并行下载量
- ⑧减少iframe数量
##### 41.谈谈toString和String的区别？
- toString()方法；数值、字符串、对象、布尔；都有toString方法；这个方法唯一能做的就是返回相应的字符串；其中null和undefined没有toString()方法；
- String()属于强制转换， null转换的结果为null；undefined转换的结果为undefined；其余的如果有toString()方法，即调用该方法，返回相应的结果；


