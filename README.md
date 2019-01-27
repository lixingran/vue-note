# vue-note
vue面试笔记


 <!-- 计算属性 -->
         计算属性是基于它们的依赖进行缓存的。
         计算属性只有在它的相关依赖发生改变时才会重新求值。
         多次访问 reverseM 计算属性会立即返回之前的计算结果，而不必再次执行函数
         ，message改变才会重新求职
         <!-- 例子 -->
         computed: { 
             reverseM:function(){
                  return this.message.split("").reverse().join("") 
                } 
            }


            <!-- setter  getter -->
            <label for="">
                桌腿的数量：
                <input type="range" v-model="legsCount">
            </label>
            <label for="">
                桌子的数量：
                <input type="text" :value="tab">
            </label>
            {{legsCount}}
            data () { 
                return { legsCount:0 } 
            }, 
            computed: { 
                tab:{ 
                    get(){
                        return this.legsCount/4 
                    },
                    <!-- 没用 -->
                    set(newValue){
                        this.legsCount =newValue*4 } 
                    } 
                }
   <!-- class style绑定 -->
<div v-bind:class="[activeClass, errorClass]"></div>
data: { activeClass: 'active', errorClass: 'text-danger' }

    <!-- 三元         -->
    <div v-bind:class="[isActive ? activeClass : '', errorClass]"></div>
            
    <!-- v-if   v-show v-for -->
      相同点： 都控制dom的元素显示隐藏
      不同点：v-if是将显示隐藏的dom整个添加或者删除，
             v-show隐藏是为css添加  display：none；元素还在

       文档：v-if 渲染条件为假什么也不做为真才会开始渲染，更高的切换开销 运行条件很少较好
             v-show 不管什么条件都会渲染只是简单的css 切换，更高的初始渲染开销 频繁的切换
         
             v-for 比v-if 优先级高


    <!-- props  父 ->子        -->
    <!-- 父组件中 -->
    <!-- 定义数据 -->
  
     newList:[ {title:'lalaal'}, {title:'gegege'}, {title:'heheh'} ]
     <!-- 引入组件 -->
     import zi from './index1'
    <!-- 监听 -->
    <zi v-bind:newList="newList"></zi>  
    <!-- 子组件中 -->
     props:{ newList:{ type:Array, required:true } }

    <li v-for="item in newList" :key="item.title">
        {{item.title}}
    </li>
    <!-- emit -->
    <!-- 定义数据 -->
    <!-- 子组件中 -->
     childValue: '我是子组件的数据'

     <!-- 按钮传值 -->
    <button @click="onClickMe">传值</button>
       <!-- 定义方法 -->
     <!-- childValue  父组件中 监听 -->
     onClickMe:function(){ this.$emit('childValue',this.childValue) }
      <!-- 父组件中 -->
    <zi v-on:childValue="childByValue"></zi>
    <!-- 定义方法 -->
     methods:{ childByValue: function (childValue) { // childValue就是子组件传过来的值 this.name = childValue } }
  
  
     <!-- slot  插槽 -->

 <!-- 单个插槽 -->
 <!-- 父组件 -->
<template>
    <div class="father">
        <h3>这里是父组件</h3>
        <child>
            <div class="tmpl">
                <span>菜单1</span>
                <span>菜单2</span>
                <span>菜单3</span>
                <span>菜单4</span>
                <span>菜单5</span>
                <span>菜单6</span>
            </div>
        </child>
    </div>
</template>
<!-- 子组件中 -->
<template>
    <div class="child">
        <h3>这里是子组件</h3>
        <slot></slot>
    </div>
</template>
 <!-- 具名插槽 -->
       
     <!-- 父组件中 -->
        <div slot="one">
            <span>one</span>
        </div>
        <div slot="two">
            <span>2222</span>
        </div>
       <!-- 子组件中 -->
        <slot name="one"></slot>
        <slot name="two"></slot>


 <!-- 作用域插槽 -->
 <!-- 子组件中 -->
<template>
    <div>
        子组件
        <slot :data="data"></slot>

    </div>
</template>
<!-- 定义数据 -->
 data() {
    return {
        data: ['zhangsan', 'lisi', 'wanwu', 'zhaoliu', 'tianqi', 'xiaoba']
    };
},
    <!-- 父组件中     -->

    <baseCheckbox>
        <template slot-scope="user">
            <div>
                <span v-for="item in user.data">
                    {{item}}
                </span>
            </div>
        </template>
    </baseCheckbox>

    <baseCheckbox>
        <template slot-scope="user">
            <div>
                <span v-for="item in user.data">
                    {{item}}
                </span>
            </div>
        </template>
    </baseCheckbox>

    <!-- 生命周期 -->
     beforeCreate vue实例挂在元素el和数据对象data为undefined

     created   vue的数据有了  dom还没有
     beforeMount vue 数据 dom初始化了  dom是虚拟dom；
     数据还未替换
      mounted 实例挂在完成  渲染成功

    computed、watch、methods

 区别： 
    computed：关联元素变化就调用 
    watch：键发生变化就调用 
    methods：满足条件时调用


        query会拼接到url后面，params不会，
        query要用path来引入，params要用name来引入
      
 <!-- 传参: 路径不能使用path 只能使用name,不然获取不到传的数据==------  params 传参 -->
this.$router.push({name: 'dispatch', params: {paicheNo: obj.paicheNo}})
获取：
     取数据：this.$route.params.paicheNo


 动态路由
    {
       path："/list/list/:id'
    }
 接收参数: this.$route.params.id

 <!-- query传参 -->
 this.$router.push({path: '/transport/dispatch', query: {paicheNo: obj.paicheNo}})
 取数据：this.$route.query.paicheNo

  <router-link :to="{path:'/List/list/child',query:{name:'child'}}"></router-link>>  
接收参数: this.$route.query.name


<!-- $parent -->
<!-- 父组件 -->
<component></component>
export default {
     name:'app',
      data:{
           return {
                str:'123456', 
                arr:[1,2,3] 
            }
         } 
        }
        <!-- 子组件 -->
 mounted(){ 
     this.$parent.str='8899';
     }

 <!-- 父子组件事件数据交互（$children获取所有子组件数组） -->


 <!-- $nextTick -->
 created、mounted操作渲染后的Dom，视图更新后对新的视图进行操作。


 <!-- vue 路由 -->
 path：路径 
 name:命名路由 
 aligns：路由别名   /a 的别名是 /b，意味着，当用户访问 /b 时，URL 会保持为 /b，但是路由匹配则为 /a，就像用户访问 /a 一样
 redirect:路由重定向 
 meat：传递自定义数据
children：组件嵌套 
component：组件 
components:多个视图组件
<!-- 全局钩子 前置守卫 -->
router.beforeEach((to,from,next)=>{
 
 // next() 会在任意路由跳转前执行，next一定要记着执行，不然路由不能跳转了
})
<!-- 后置守卫 -->
router.afterEach((to, from) => { // ... })
<!-- 全局解析守卫 -->
beforeResolve

<!-- 路由 钩子 -->
beforeEnter
const router=new Vuerouter({
     routes:[ 
     { path:'/', 
     name:'index',
      component:index,
       beforEnter:(to,from,next)=>{
            // next() 
        },
     beforLeave:(to,from,next)=>{
          // next() 
        } 
    } 
    ] 
})
<!-- 组件内的钩子 -->
 beforeRouteEnter (to, from, next) {
      // 在渲染该组件的对应路由被 confirm 前调用 // 不！能！获取组件实例 `this` // 因为当守卫执行前，组件实例还没被创建 
    },
 beforeRouteUpdate(to, from, next) { 
     // 在当前路由改变，但是该组件被复用时调用 // 举例来说，
     对于一个带有动态参数的路径 /foo/:id，在 /foo/1 和 /foo/2 之间跳转的时候， 
     // 由于会渲染同样的 Foo 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
    // 可以访问组件实例 `this` 
},
 beforeRouteLeave (to, from, next) 
 { // 导航离开该组件的对应路由时调用 // 可以访问组件实例 `this` 
}

运用: 
(1)清除定时器 beforeRouterLeave内清除组件内部定时器，避免占据缓存。 
(2)跳转拦截 beforeRouterLeave页面内有未完成的操作，阻止页面跳转。 
(3)页面遮罩 beforeEach通过改变提交vuex遮罩状态，控制遮罩的显示。
(4)登录拦截 beforeEach判断用户登录状态，未登录跳转登录页


<!-- keep-alive： -->
包裹在router-view组件外面，第一次触发生命钩子created、mounted、activated，退出时触发deactivated,再次进入（浏览器前进后退）只触发activated，不用发起初始化请求。 启用：路由meta中配置keepAlive:true
<!-- 例子 -->
假设这里有 3 个路由： 
A、B、C。
 需求： 
 默认显示 A 
 B 跳到 A，A 不刷新 
 C 跳到 A，A 刷新

<!-- 在 A 路由里面设置 meta 属性： -->
{ path: '/', name: 'A', component: A, meta: { keepAlive: true // 需要被缓存 } }
<!-- 在 B 组件里面设置 beforeRouteLeave： -->
export default {
     data() {
          return {};
         }, 
         methods: {},
          beforeRouteLeave(to, from, next) { 
              // 设置下一个路由的 meta 
              to.meta.keepAlive= true; 
              // 让 A 缓存，即不刷新 
              next(); 
} 
};
<!-- 在 C 组件里面设置 beforeRouteLeave： -->
export default {
     data() {
          return {}; 
        }, methods: {},
         beforeRouteLeave(to, from, next) {
              // 设置下一个路由的  meta
               to.meta.keepAlive= false; 
              // 让 A 不缓存，即刷新
                next();
 }
 };


<!-- vue key -->
当相同的标签名的元素切换时，需要通过key特效设置唯一的值来标记以让vue区分他们
否则vue为了效率只会替换相同标签内部的内容


<!-- vue data  为何data是一个方法-->
当一个组件被定义， data 必须声明为返回一个初始数据对象的函数
，因为组件可能被用来创建多个实例。如果 data 仍然是一个纯粹的对象，
则所有的实例将共享引用同一个数据对象！通过提供 data 函数，每次创建一个新实例后，我们能够调用 data
函数，从而返回初始数据的一个全新副本数据对象

<!-- keep-alive生命周期钩子函数：activated、deactivated -->
包裹在router-view组件外面，第一次触发生命钩子created，mounted，actived，退出时触发deactiveed
，（浏览器前景或后退）只触发actived 不用发起初始化请求
启用：路由meta 中配置keepAlive：true

<!-- vuex  和存本地那个 好 --><!-- vuex刷新数据消失 -->
     感觉你对vuex的理解有误，vuex主页解决的是vue中组件通信的问题，
     具体的体现是当你进行路由切换和组件访问时都能够去操作store中的数据。
    
     如果要解决刷新页面时store中数据不能访问的问题，要么将数据存在localstorage中，要么重新发起请求



     <!-- 过滤器 -->
        <h1>
            {{message | Upper}}
        </h1>

        data () { return { message:'Hellow Vue' } }, 
        filters:{ 
            Upper:function(val){ 
                return val.toUpperCase() 
            },
            Lower:function(val){
                return val.toLowerCase() 
            } 
    },
    <!-- vue自定义指令 -->
<input v-focus>
 //注册一个全局自定义指令v-focus 
 Vue.directive('focus', { 
     // 当绑定元素插入到DOM中 
     inserted: function (el) { 
         // 聚焦元素
          el.focus() 
        } }
        );

        <!-- 跨域 -->
 同源策略跨域（document.domain）
 1.com下的1.com/1.html
 2.com域下的2.com/2.html   来通讯
 1.com/1.html加入一个iframe，src="2.com/2.html"
 这样1.com/1.html就可以获取到iframe src上的hash值
 但是浏览器是不允许跨域修改iframe内的跨域域名通过
 parent.location.hash的值
 在2.com/2.html里面再加一个iframe src="1.com/2.html"，
 然后让src="1.com/2.html"通过parent.parent.location.hash来
 修改1.com/1.html那个iframe的hash。
1.com/1.html想知道hash是不是有变化还要加个定时检测，

<!-- vue 动画 -->
v-enter v-enter-active v-enter-to
v-leave v-leave-active v-leave-to;

<!-- vue 首次加载慢 -->
路由懒加载
使用异步组件，按需加载
'my-component':()=>import('./my-async-component')
图片量多的时候可以进行分批的加载
如果引用了插件不要再vue中引用
vue项目的webpack.base.conf.js  
手动引入到打包好的index.html
