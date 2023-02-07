# Vue-Router4

**路由核心**，改变URL，但是页面不进行整体刷新

路由理解为指向

**路由表**：是一个映射表，一个路由就是一组**映射关系**，key:value

key:表示路由，value可以为function 或者component(**组件**)

Vue-Router是基于路由和组件的 ，路由是用来设定访问路径，将路径和组件映射起来



## 4和3的区别

- createRouter
- 用来创建router对象
- 4.x用法

```javascript
import { createRouter } from "vue-router"
const router = createRouter({
    // opyions
    .....
})
```

- 3.x用法

```javascript
import VueRouter from "vue-router"'
const router = new VueRouter({
    // options
    ......
})
```

### 路由模式

- createWebHashHistory (hash)
- createWebHashHistory (history)
- 4.x用法

```javascript
import { 
    createRouter,
    createWebHashHistory,
    createWebHashHistory
} from 'vue-router'
const router = createRouter({
    history:createWebHashHistory() / createWebHashHistory()
})
```

- 3.x用法

```javascript
 const router = new VueRouter({
    mode: 'hash' / 'history'
 })
```

### 重定向

- 写法有所改变
- 4.x的写法

```javascrip
{
    path: '/:pathMatch(.*)*', // 需要使用正则去匹配
    redirect: Home,
}
```

- 3.x的写法

```javascript
{
    path: '*',
    redirect: Home
}
```

### 挂载方式

- 因为vue3的composition api，vue-router的挂载方式以插件来挂载
- 4.x的用法

```javascript
    import { createApp } from 'vue'
    import router from './router.js'
    import App from './App.vue'
    createApp(App).use(router).mount('#app');
```

- 3.x的用法，以属性的方式进行挂载

```javascript
 import router from './router.js'
   new Vue({
      router
   })

```

### 组件中的使用

- 因为setup中不能访 **this**,所以提供两个api来获取 **router** 和 **route** ， **useRouter()** 和 **useRoute()**
- 4.x的用法

```javascript
   import { useRouter,useRoute } from "vue-router"
   export default({
      setup(){
        const router = useRouter();
        const route = useRoute();
        const linkToHome = () => {
            router.push({
                path:'/'
            })
        }
        return{
            linkToHome
        }
      }
   })
```

- 3.x的用法

```javascript
    export default({
       methods:{
         linkToHome(){
           this.$router.push({
                   path:'/'
               })
         }
       }
    })
```

## Vue-Router4























































