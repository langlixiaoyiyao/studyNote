# vue中的路由
## 准备工作
`
npm i vue-router
`
## vue中路由的使用方式
### vue3中的使用方式
#### 基本使用
```
// src/router/index.ts
import { createRouter, createWebHistory } from 'vue-router';
import Index from '@/views/Index.vue';

const router = createRouter({
    history: createWebHistory(),
    routes: [
        {
            name: 'index',
            path: '/index',
            component: Index,
        }
    ]
});

export default router;
```
```
// src/main.ts
import './assets/main.css';
import Router from '@/router';

import { createApp } from 'vue'
import App from './App.vue'

const app = createApp(App);
app.use(Router);
app.mount('#app')
```
```
// src/App.vue
<template>
  <div>
    <RouterLink to="/index" active-class="active" />
    <div class="body">
      <RouterView />
    </div>
  </div>
</template>

<script setup lang="ts">
  import {RouterView, RouterLink} from 'vue-router';
</script>

<style scoped>
</style>
```

#### createRouter(config) config.history
1、config.history 代表路由的模式，值为 createWebHistory() 或者 createWebHash()  

#### createRouter(config) config.routes
说明：  
1、config.routes 是配置路由的，是个数组，数组中应该包含对象。  

##### 二级路由写法
```
// 二级路由
const router = createRouter({
    history: createWebHistory(),
    routes: [
        {
            name: 'index',  // 路由的名字
            path: '/index', // 路由匹配的路径
            component: Index, // 路由组件
            children: [            // 二级路由
                {
                    name: 'detail', // 路由的名字
                    path: 'detail', // 路由匹配的路径,不需要写/
                    component: Detail,  // 路由组件
                }
            ]
        }
    ]
});

// 应用
<RouterLink to="/index/detail"></RouterLink>
// or
<RouterLink :to="{name: 'detail'}"></RouterLink>
```

##### 路由参数写法
###### query写法
```
// 路由参数的几种写法
const router = createRouter({
    history: createWebHistory(),
    routes: [
        {
            // query参数
            name: 'index',  // 路由的名字
            path: '/index', // 路由匹配的路径
            component: Index, // 路由组件
        },
    ]
});

// 应用
<RouterLink to="/index?id=1"></RouterLink>
<RouterLink :to="{name: 'index', query: {id: '1'}}"></RouterLink>

// 得到路由参数
import {useRoute} from 'vue-router';

const route = useRoute();  // route是个响应式对象
console.log(route.query);

```

###### params写法
```
// 路由参数的几种写法
const router = createRouter({
    history: createWebHistory(),
    routes: [
        {
            // params参数
            name: 'detail',
            path: '/detail/:id/:content?',  // 加个问号表示其必要性
            component: Detail,
        }
    ]
});

// 应用
<RouterLink to="/detail/1"></RouterLink>
<RouterLink :to="{name: 'detail', params: {id: '1'}}"></RouterLink>  // 当使用params模式，而且to属性值是个对象，只能通过name跳转，不能用path跳转，而且params中的参数不能是对象或者数组类型

// 得到路由参数
import {useRoute} from 'vue-router';

const route = useRoute();  // route是个响应式对象
console.log(route.params);
```

##### 路由的props写法
###### 只能用于params参数的写法
```
// 路由的props配置：简单来说就是当使用这个配置，可以将路由参数当组件参数一样使用
const router = createRouter({
    history: createWebHistory(),
    routes: [
        {
            // params参数
            name: 'detail',
            path: '/detail/:id/:content?',  // 加个问号表示其必要性
            component: Detail,
            // 第一种写法(只能用于params模式)
            props: true,
            
        }
    ]
});

// 使用
defineProps(['id']);   
```

###### query和params参数都可用
```
// 路由的props配置：简单来说就是当使用这个配置，可以将路由参数当组件参数一样使用
const router = createRouter({
    history: createWebHistory(),
    routes: [
        {
            // query参数
            name: 'index',  // 路由的名字
            path: '/index', // 路由匹配的路径
            component: Index, // 路由组件
            // props的第二种写法（query和params两种模式都可以用）
            props(route) {
                return route.query;  // 是哪种模式就return哪种模式的字段, 也可以自己决定返回哪种参数
            }
        }
    ]
});

// 使用
defineProps(['id']);   
```

###### 写死的写法
```
// 路由的props配置：简单来说就是当使用这个配置，可以将路由参数当组件参数一样使用
const router = createRouter({
    history: createWebHistory(),
    routes: [
        {
            name: 'a',  // 路由的名字
            path: '/a', // 路由匹配的路径
            component: A, // 路由组件
            // props的第三种写法（写死）
            props: {
                a: 100
            }
        }
    ]
});

// 使用
defineProps(['id']);   
```

#### RouterLink的replace属性
说明：直接替换当前路由  

#### 编程式导航
```
import {useRouter} from 'vue-router';
const router = useRouter();
router.push('/index');
router.replace('/detail')
```
说明，push方法和replace方法里面的参数，RouterLink的to属性可以怎么写，它就可以怎么写

#### 路由重定向
```
// 当匹配到/hh路径的时候就会重定向到/home
const router = createRouter({
    history: createWebHistory(),
    routes: [
        {
            path: '/hh', // 路由匹配的路径
            rediect: '/home'
        }
    ]
});
```

### vue2中的使用方式
#### 基本使用
```
// src/router/index.js
import VueRouter from 'vue-router';
import Home from '@/views/Home.vue';
const router = VueRouter({
    mode: 'history',    // mode默认是hash模式
    routes: [
        {
            path: '/home',
            component: Home,
        }
    ]

})
export default router;
```
```
// src/main.js
import Vue from 'vue'
import App from './App.vue'
import VueRouter from 'vue-router'
import router from '@/router'

Vue.config.productionTip = false
Vue.use(VueRouter);
new Vue({
  render: h => h(App),
  router
}).$mount('#app');
```
```
// src/app.vue
<template>
    <div>
        <router-view></router-view>
    </div>
</template>
<script>
export default {
    name: 'App',
}
</script>
```

#### 路由跳转
路由组件配置  
```
// src/router/index.js
import VueRouter from 'vue-router';
import Home from '@/views/Home.vue';
const router = new VueRouter({
    mode: 'history',
    routes: [
        {
            path: '/home',
            name: 'home',
            component: Home
        }
    ]
});
export default router;
```
##### 使用router-link跳转
###### 使用路径跳转
```
// src/app.vue
<template>
    <div>
        <router-link to='/home'>首页</router-link>
    </div>
</template>
```
###### 命名式路由跳转
```
// src/app.vue
<template>
    <div>
        <router-link :to='{name: "home"}'>首页</router-link>
    </div>
</template>
```
##### 编程式路由跳转
```
// src/App.vue
<script>
export default {
    name: 'App',
    data() {
        return {};
    },
    methods: {
        goHome() {
            this.$router.push('/home');
            this.$router.push({name: 'home'});
        }
    }
}
</script>
```

#### 路由参数
与vue3一致，这里不做说明

#### 嵌套路由
与vue3一致，这里不做说明

#### 重定向
与vue3一致，这里不做说明

