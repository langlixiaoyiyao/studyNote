# vue3的hook
## hook说明
vue3中hook的实现主要是为了将同一模块的数据方法等集合放到一起。  
## 写法
自定义的hook其实就是一个js，js中导出一个默认函数，函数return一个对象。函数里面可以写任何东西，比如钩子函数，计算属性等。
```
// useDog.js
import { reactive } from 'vue';
export default function() {
    const dog = reactive({
        name: '柯基',
        age: 18,
    });
    function updateAge() {
        dog.age++;
    }
    return {
        dog,
        updateAge
    }
}
// 使用 src/app.vue
<script setup>
import useDog from '@/hooks/useDog';
const { dogData, updateDogAge } = useDog();
</script>
```