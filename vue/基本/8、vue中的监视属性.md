# vue中的监视属性
## vue3中的监视属性
说明：  
vue3的监视watch只能监视以下四种类型  
1、ref类型响应式数据  
2、reactive 类型响应式数据  
3、函数返回一个值  
4、一个包括上述情况的数组 

### watch监视ref类型数据
#### watch监视ref定义的基本类型
```
<script setup lang="ts">
  import {watch, ref} from 'vue';
  let num = ref(0);
  watch(num, (newVal, oldVal) => {      // 直接写名字，不用写.value，这个watch会自动.value
    //newVal, oldVal不一样
  })
</script>
```

#### watch监视ref定义的对象类型
说明：  
需要开启深度监视，否则监视的是地址，属性的变化不会触发回调
```
<script setup lang="ts">
  import {watch, ref} from 'vue';
  let num = ref({
    age: 18
  });
  watch(num, (newVal, oldVal) => {
    //newVal, oldVal一样
  }, {
    deep: true,
  })
</script>
```

#### watch监视reactive定义的对象类型
说明：  
当监视的对象是reactive创建的时候，会自动开启深度监视，而且这个深度监视是无法通过deep: false关掉的
```
<script setup lang="ts">
  import {watch, reactive} from 'vue';
  let num = reactive({
    age: 18
  });
  watch(num, (newVal, oldVal) => {
    //newVal, oldVal一样
  })
</script>
```

#### watch监视的是ref定义或者reactive定义的对象中的某个属性的时候

## vue2中的监视属性
```
<template>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      name: 'c'
    }
  },
  watch: {
    name: function(newVal, oldVal) {
      // 执行操作
    }
  }
}
</script>

<style>
</style>

```