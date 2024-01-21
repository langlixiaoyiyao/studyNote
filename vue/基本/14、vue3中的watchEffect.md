# vue3中的watchEffect
说明：  
1、这个函数会接收一个函数，会自动根据参数函数里面的内容自动监视要用到的数据，并在这些数据发生改变的时候执行参数函数。  
```
import {watchEffect, ref} from 'vue';
const num = ref(0);
watchEffect(() => {  // 会一开始就先执行一次
    console.log(num)
})
```
