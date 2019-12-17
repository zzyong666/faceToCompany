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