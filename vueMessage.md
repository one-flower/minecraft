# 自己没事干整理的vue

## vue的3种使用方式
1.	Js引入 <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
2.	快速的运行vue文件，需要用到vue的一个服务，使用方法，先下载一个服务，cnpm install -g @vue/cli-service-global 执行这个命令，全局安装这个插件
3.	使用脚手架工具，安装npm install -g @vue/cli

## vue生命周期
总共分为 8 个阶段创建前/后，载入前/后，更新前/后，销毁前/后。
- beforeCreat() 创建前
- created（）创建    （页面使用常用）  
创建前/后： 在 beforeCreate 阶段，vue 实例的挂载元素 el 还没有。
- beforeMount()挂载前
- mounted（）挂载    （页面使用常用）  
载入前/后：在 beforeMount 阶段，vue 实例的$el 和 data 都初始化了，但还是挂载之前为虚拟的 dom 节点，data.message 还未替换。在 mounted 阶段，vue 实例挂载完成，data.message 成功渲染。
- beforeupdate（）更改前
- updated（）更改  
更新前/后：当 data 变化时，会触发 beforeUpdate 和 updated 方法。
- beforeDestroy()销毁前
- destroyed（）销毁  
销毁前/后：在执行 destroy 方法后，对 data 的改变不会再触发周期函数，说明此时 vue 实例已经解除了事件监听以及和 dom 的绑定，但是 dom 结构依然存在

##小知识
### 一些vue的特性
1. prop 的大小写  
HTML 中的 attribute 名是大小写不敏感的，所以浏览器会把所有大写字符解释为小写字符。这意味着当你使用 DOM 中的模板时，camelCase (驼峰命名法) 的 prop 名需要使用其等价的 kebab-case (短横线分隔命名) 命名：
2. 不推荐同时使用 v-if 和 v-for  
当 v-if 与 v-for 一起使用时，v-for 具有比 v-if 更高的优先级
### 一些操作的简写
1. v-bind  :
2. v-on    @
### vuex
vue 框架中状态管理  
有 5 种属性，分别是 state、getter、mutation、action、module  
常用
```
computed: {
    ...mapGetters([
      'userInfo'
    ])
  },
```

## 路由的3种跳转方式

1. router-link 地址栏会有请求参数
    vue页面<router-link :to="'/edit/'+id"></router-link>  
    vue 路由  
```
{  
    path: '/edit/:id',  
    name: 'fcedit',  
    component: () => import('./views/housing/edit'),  
    meta: {  
        title: '编辑',  
    }  
}
```
接收 this.$route.params

2. path query传参相当于ajax的get 请求，请求参数会写在地址栏
```
this.$router.push({
    path :'./inputinformation',
    query:{ id : val }
})
```
接收 this.$route.query
3. name params传参不会显示在地址栏，但是页面刷新的时候参数会丢失
```
this.$router.push({
    name :'inputinformation',
    params:{ id : val }
})
```
接收 this.$route.params
    
## 父子组件传递
父 p 子 c   建议单项数据流传递，不建议反向传递
1. 父组件直接传值  
传递的值需要父组件预先有
```
父组件：
<templete>
    <div><c :c_val=”pval”></c></div>
</templete>

<script>
import c from xxxx
export default {
    data(){
        returen{
            pval:'hahaha'
        }
    },
    components:{ c:'c'}
}

子组件：
<templete>
    <div>{{pval}</div>
</templete>

<script>
export default {
    data(){
        returen{
            pval:''
        }
    }，
    props:{
        cVal: {
            type: String,
            default: () => {
                return ''
            }
        }
    }
}
</script>

```
2. 父组件调用子组件的方法
```
父组件：
<templete>
<div>
    <c ref="cMethods"></c>
    <button @click="call()">调用子组件</button>
</div>
</templete>

<script>
import c from xxxx
export default {
    components:{ c:'c'},
    methods:{
        call(){
            this.$refs.cMethods.accept('我是父组件')
        }
    }
}

子组件：
<templete>
</templete>

<script>
export default {
    methods:{
        accept(val){
            alert(val)
        }
    }
}
</script>

```
3. 子组件调用父组件的方法
```
子组件：
<templete>
<div>
    <button @click="call()">调用父组件</button>
</div>
</templete>

<script>
import p from xxxx
export default {
    components:{ p:'p'},
    methods:{
        call(){
            this.$emit('accept','我是子组件')
        }
    }
}

父组件：
<templete>
<div>
    <C v-on:accept="accept"/>
</div>
</templete>

<script>
import c from xxxx
export default {
    methods:{
        accept(val){
            alert(val)
        }
    }
}
</script>


#### Gitee Feature

1. You can use Readme\_XXX.md to support different languages, such as Readme\_en.md, Readme\_zh.md
2. Gitee blog [blog.gitee.com](https://blog.gitee.com)
3. Explore open source project [https://gitee.com/explore](https://gitee.com/explore)
4. The most valuable open source project [GVP](https://gitee.com/gvp)
5. The manual of Gitee [https://gitee.com/help](https://gitee.com/help)
6. The most popular members  [https://gitee.com/gitee-stars/](https://gitee.com/gitee-stars/)
