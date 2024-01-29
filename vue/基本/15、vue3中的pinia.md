# vue3中的pinia
这是vue3中的集中式状态（数据）管理

## 安装
npm i pinia

## 使用
### 配置pinia，使其能在vue3中使用
```
// src/main.js
import {createApp} from 'vue';
import { createPinia } from 'pinia';
import App from './App.vue';

const pinia = createPinia();
const app = createApp(App);
app.use(pinia);
app.mount('#app');
```

### 编写store文件
#### store文件的配置项写法
```
// src/store/count.js
import {defineStore} from 'pinia';
export const useCountStore = defineStore('count', {
    state() {   // 配置数据
        return {
            num: 6,
        }
    },
    actions: {  // 配置action函数
        increment(value) {
            this.sum += value;
            this.$state.sum += value;
        }
    },
    getters: {  // 相当于计算属性
        bigSum(state) {
            const a = this.num * 10;
            const b = state.num * 10
            const c = this.state.num * 10;
            return a;
        }
    }
})
```

#### store的组合式写法
```
// src/store/count.js
import {rective} from 'vue';
import {defineStore} from 'pinia'
const useCountStore = defineStore('count', () => {
    // 数据
    const obj = reactive({
        sum: 6
    });

    // 方法
    function increment(value) {
        obj.sum += 3;
    };

    return {obj, increment};
})
```

### store文件的使用
```
import useCountStore from '@/store/count.js';
const countStore = useCountStore();
countStore.sum;  // 获取变量
countStore.sum += 2;  // 直接修改
countStore.increment(3);    // 调用action修改
countStore.$patch({
    sum: '888',     // 批量修改
})
```

### store数据的解构
不能使用toRefs，因为toRefs会将被包裹的所有项都会变成ref响应式对象（包括方法等）。可以使用pinia内部提供的storeToRefs。这个函数只会把数据变成响应式对象。
```
import useCountStore from '@/store/count';
const obj = useCountStore();
const {sum} = storeToRefs(obj);
```

### store数据的监听
每个store对象里面都会有一个$subscribe函数（当store里面的数据发生变化的时候，这个函数就会触发）
```
const countStore = useCountStore();
countStore.$subscribe((mutate, state) => {
    //mutate记录了本次修改的信息
    // state 记录的是本次修改的数据项的数据
})
```


# 题外话
1、如何多次解构某个对象
```
const {obj: {name:username}} = {
    obj: {
        name: ''
    }
}
// username是将name重命名为username
```
2、ref对象
如果这个ref对象是由我们自己定义的，那么我们在使用的时候需要.value。  
如果是vue自己定义的，那么我们可以直接写，不需要.value。