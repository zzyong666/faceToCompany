## vue
##### 1.vue的双向数据绑定原理？
- 实现mvvm的双向绑定，是采用数据劫持结合发布者-订阅者模式的方式，通过Object.defineProperty()来劫持各个属性的setter，getter，在数据变动时发布消息给订阅者，触发相应的监听回调。
#####  2.vue组件通信?
①父组件向子组件传值 --Props传递数据
在父组件中使用儿子组件

```
<template>
　　<div>
　　　　父组件：{{money}}
　　　　<Son1 :money="money"><Son1>
　　</div>
</template>
<script>
　　import Son1 from ''./Son1";
　　export default{
　　　　components:{
　　　　　　Son1
　　　　},
　　　　data(){
　　　　　　return { money: 100};
　　　　}
　　};
</script>
```

子组件接受数据

```
props:{
　　value:{
　　　　type:Number,
　　　　default:1
　　}
}
```

如果是数组

```
props:{
　　value:{
　　　　type:Array,
　　　　default: ()=>[]
　　}
}
```

②子组件通信父组件 $emit使用
子组件触发父组件方法，通过回调的方式将修改的内容传递给父组件
父组件

```
<template>
　　<div>
　　　　父组件：{{money}}
　　　　<Son1 :money="money" @input="change"><Son1>
　　</div>
</template>
<script>
　　import Son1 from ''./Son1";
　　export default{
　　　　methods:{
　　　　　change(data){
　　　　　　 this.money = data
　　　　　 }　
　　　　},
　　　　components:{
　　　　　　Son1
　　　　},
　　　　data(){
　　　　　　return { money: 100};
　　　　}
　　};
</script>
```

子组件触发绑定自己身上的方法

```
<template>
　　<div>
　　　　子组件1：{{money}}
　　　　<button @click="$emit('input',200)">修改父组件的值<Son1>
　　</div>
</template>
<script>
　　export default{
　　　　props:{
　　　　　money:{
　　　　　　 type:Number
　　　　　}
　　　　}
　　};
</script>
```

③ $parent、$children（多层级传递）

```
<Grandson1 :value="value"></Grandson1>
<template>
　　<div>
　　　　孙子1：{{value}}
　　　　<---调用父组件的input事件-->
　　　　<button @click="$parent.$emit('input',200)">更改<Son1>
　　</div>
</template>
<script>
　　export default{
　　　　props:{
　　　　　value:{
　　　　　　 type:Number
　　　　　}
　　　　}
　　};
</script>
```

④$attrs、 $listeners：
$attrs批量向下传入属性

```
<Son2 name="小明" age="18"></Son2>
<--可以在son2组件中使用$attrs,可以将属性继续向下传递-->
<div>
　　儿子2：{{  $attrs.name }}
　　<Grandson2  v-bind="$attrs"></Grandson2>
</div>
<tempalte>
　　<div>孙子：{{$attrs}}</div>
</template>
```

$listeners批量向下传入方法

```
<Son2 name="小明" age="18" @click=“()=>{this.money  =500}”></Son2>
<--可以在son2组件中使用$attrs,可以将属性继续向下传递-->
<Grandson2  v-bind="$attrs" v-on="$listeners"></Grandson2>
<button @click="$listeners.click()">更改<Son1>
```

⑤Provide&Inject

```
Provide 在父级中注入数据
provide(){
　　return {parentMsg:'父亲'}；
}
Inject
在任意子组件中可以注入父级数据
inject：['parentMsg']//会将数据挂载在当前实例上
```

⑥ref使用
获取组件实例

```
<Grandson2  name="花花" ref="grand2"></Grandson2>
mounted(){
　　console.log(this.$refs.grand2.name);
}
```

⑦EventBus：用于跨组件通知

```
Vue.prototype.$bus = new Vue();
Son2组件和Grandson1互相通信
mounted() {
　　//父亲组件注册
　　this.$bus.$on('my',data=>{
　　　　console.log(data)
　　})
}
mounted(){
　　//侄子组件调用
　　this.$nextTick(()=>{
　　　　this.$bus.$emit('my',"我是小红”);
　　})
}
```

##### 3.vue中method，computed和watch三者的区别？
- computed--适用于重新计算比较费时不用重复数据计算的环境。所有 getter 和 setter 的 this 上下文自动地绑定为 Vue 实例。如果一个数据依赖于其他数据，那么把这个数据设计为computed
- watch--像是一个 data 的数据监听回调，当依赖的 data 的数据变化，执行回调，在方法中会传入 newVal 和 oldVal。可以提供输入值无效，提供中间值 特场景。Vue 实例将会在实例化时调用 $watch()，遍历 watch 对象的每一个属性。如果你需要在某个数据变化时做一些事情，使用watch。
- method-- 跟前面的都不一样，我们通常在这里面写入方法，只要调用就会重新执行一次
##### 4.vue-route是怎么实现的？
- vue-router通过hash与History interface两种方式实现前端路由，更新视图但不重新请求页面”是前端路由原理的核心之一
- hash模式：在浏览器中符号“#”，#以及#后面的字符称之为hash，用window.location.hash读取；特点：hash虽然在URL中，但不被包括在HTTP请求中；用来指导浏览器动作，对服务端安全无用，hash不会重加载页面。
- history模式：history采用HTML5的新特性；且提供了两个新方法：pushState（），replaceState（）可以对浏览器历史记录栈进行修改，以及popState事件的监听到状态变更。
##### 5.vue中$nexTrick有什么用？
在Vue生命周期的created()钩子函数进行的DOM操作一定要放在Vue.nextTick()的回调函数中。原因是什么呢，原因是在created()钩子函数执行的时候DOM 其实并未进行任何渲染，而此时进行DOM操作无异于徒劳，所以此处一定要将DOM操作的js代码放进Vue.nextTick()的回调函数中
##### 6.vue中$set有什么用？
在我们使用vue进行开发的过程中，可能会遇到一种情况：当生成vue实例后，当再次给数据赋值时，有时候并不会自动更新到视图上去,因此可以使用$set。

```
initTableData() {
  this.tableData.forEach(element => {
      this.$set(element, 'edit', false)
  })
}
```

##### 7.vue生命周期的理解？
- Vue 实例从创建到销毁的过程，就是生命周期。从开始创建、初始化数据、编译模板、挂载Dom→渲染、更新→渲染、销毁等一系列过程，称之为 Vue 的生命周期。
生命周期中有多个事件钩子，如下：
	- beforeCreate（创建前） 在数据观测和初始化事件还未开始
	- created（创建后） 完成数据观测，属性和方法的运算，初始化事件，$el属性还没有显示出来
	- beforeMount（载入前） 在挂载开始之前被调用，相关的render函数首次被调用。实例已完成以下的配置：编译模板，把data里面的数据和模板生成html。注意此时还没有挂载html到页面上。
	- mounted（载入后） 在el 被新创建的 vm.$el 替换，并挂载到实例上去之后调用。实例已完成以下的配置：用上面编译好的html内容替换el属性指向的DOM对象。完成模板中的html渲染到html页面中。此过程中进行ajax交互。
	- beforeUpdate（更新前） 在数据更新之前调用，发生在虚拟DOM重新渲染和打补丁之前。可以在该钩子中进一步地更改状态，不会触发附加的重渲染过程。
	- updated（更新后） 在由于数据更改导致的虚拟DOM重新渲染和打补丁之后调用。调用时，组件DOM已经更新，所以可以执行依赖于DOM的操作。然而在大多数情况下，应该避免在此期间更改状态，因为这可能会导致更新无限循环。该钩子在服务器端渲染期间不被调用。
	- beforeDestroy（销毁前） 在实例销毁之前调用。实例仍然完全可用。
	- destroyed（销毁后） 在实例销毁之后调用。调用后，所有的事件监听器会被移除，所有的子实例也会被销毁。该钩子在服务器端渲染期间不被调用。
##### 8.v-if和v-show的区别？
- v-if是通过控制dom节点的存在与否来控制元素的显隐；
- v-show是通过设置DOM元素的display样式，block为显示，none为隐藏；
基于以上区别，因此，如果需要非常频繁地切换，则使用 v-show 较好；如果在运行时条件很少改变，则使用 v-if 较好。
##### 9.$route和$router的区别？
- `$router`是VueRouter的一个对象，通过`Vue.use(VueRouter)`和VueRouter构造函数得到一个router的实例对象，这个对象中是一个全局的对象，他包含了所有的路由包含了许多关键的对象和属性。
- `$route`对象表示当前的路由信息，包含了当前 URL 解析得到的信息
	- **1.$route.path** 字符串，对应当前路由的路径，总是解析为绝对路径，如 "/foo/bar"。 
	- **2.$route.params** 一个 key/value 对象，包含了 动态片段 和 全匹配片段， 如果没有路由参数，就是一个空对象。
	- **3.$route.query** 一个 key/value 对象，表示 URL 查询参数。例如，对于路径 /foo?user=1，则有 $route.query.user == 1， 如果没有查询参数，则是个空对象。
	- **4.$route.hash** 当前路由的 hash 值 (不带 #) ，如果没有 hash 值，则为空字符串。锚点 
	- **5.$route.fullPath** 完成解析后的 URL，包含查询参数和 hash 的完整路径。
	- **6.$route.matched** 数组，包含当前匹配的路径中所包含的所有片段所对应的配置参数对象。
	- **7.$route.name 当前路径名字** 。
	- **8.$route.meta** 路由元信息。
##### 10.vue组件data为什么必须是函数？
- 如果data是一个函数的话，这样每复用一次组件，就会返回一份新的data，类似于给每个组件实例创建一个私有的数据空间，让各个组件实例维护各自的数据。而单纯的写成对象形式，就使得所有组件实例共用了一份data，就会造成一个变了全都会变的结果。
##### 11.vue中怎么自定义指令？
① 定义全局的自定义变量

```
main.js
Vue.directive('color',{
  inserted(el){
//  各单位注意，这里的el获取的是标签元素，说白了就是可以直接操作DOM    console.log(el)
    el.style.color = "red"
  }
})

<div >前端伪大叔</div>
<div v-color>前端伪大叔</div>
```

② 组件内指令-只有自己组件可以使用

```
//  template
<div >前端伪大叔</div>
<div v-color>前端伪大叔</div>

//  script
directives:{
    color:{  
     inserted(el){
       el.style.color = 'cyan'
     }
   }
}
```

##### 12.对keep-aerlive的了解？
- 通过设置了keep-alive，可以简单理解为从页面1跳转到页面2后，然后后退到页面1，只会加载缓存中之前已经渲染好的页面1，而不会再次重新加载页面1，及不会再触发页面一种的created等类似的钩子函数，除非自己重新刷新该页面1。
##### 13.vue中key的作用？
强制替换元素，从而可以触发组件的生命周期钩子或者触发过渡。因为当key改变时，Vue认为一个新的元素产生了，从而会新插入一个元素来替换掉原有的元素。

```
<transition> <span :key="text">{{text}}</span> </transition>、
```

- 这里如果text发生改变，整个<span>元素会发生更新，因为当text改变时，这个元素的key属性就发生了改变，在渲染更新时，Vue会认为这里新产生了一个元素，而老的元素由于key不存在了，所以会被删除，从而触发了过渡。
同理，key属性被用在组件上时，当key改变时会引起新组件的创建和原有组件的删除，此时组件的生命周期钩子就会被触发。
##### 14.vue中常用的路由钩子函数有哪一些？
- 全局守卫：
	- router.beforeEach 全局前置守卫 进入路由之前
	- router.beforeResolve 全局解析守卫(2.5.0+) 在beforeRouteEnter调用之后调用
	- router.afterEach 全局后置钩子 进入路由之后
- 路由组件内的守卫：
	- beforeRouteEnter 进入路由前
	- beforeRouteUpdate (2.2) 路由复用同一个组件时
	- beforeRouteLeave 离开当前路由时
##### 15.vue中常用的修饰符？
- .stop              //组织单击事件冒泡
- .prevent        //提交事件不再重新加载页面
- .capture        //添加事件侦听器时使用事件捕获模式
- .self              //只当事件在该元素本身时触发回调（在其子元素上不触发）
- .once             //只触发一次事件
##### 16.vuex中的成员？对应的作用？
- state => 基本数据 
- getters => 从基本数据派生的数据 
- mutations => 提交更改数据的方法，同步！
- actions => 像一个装饰器，包裹mutations，使之可以异步。
- modules => 模块化Vuex
#####  16.谈一谈vue的虚拟DOM是什么回事？
- Vue.js通过编译将模版转换成渲染函数(render)，执行渲染函数就可以得到一个虚拟DOM
简单点讲，在Vue的实现上，Vue讲模版编译成虚拟DOM渲染函数。结合Vue自带的响应系统，在状态改变时，Vue能够智能地计算出重新渲染组件的最小代价并应用到DOM操作上。