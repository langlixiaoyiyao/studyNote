# vue3中的组合式api写法
## setup解析
setup是一个配置项，值是一个函数，返回值是模板中要用到的变量和方法。  
setup里面没有this指向  
setup函数的运行要比vue生命周期中的beforeCreate要早  
```
<template>
    <div>{{myName}}</div>
    <div @click="handleClick">点击</div>
</template>
<script lang='ts'>
    export default {
        name: 'App',
        setup() {
            let myName='H';
            function handleClick() {
                myName='X';        // 这样写是没有响应式的
            };
            return {
                myName,
                handleClick
            }
        }
    }
</script>
<style></style>
```




# vue2中配置项写法
```
<template>
    <div>{{myName}}</div>
    <div @click="handleClick">点击</div>
</template>
<script lang='ts'>
    export default {
        name: 'App',
        data() {
            return {
                myName: 'H',
            }
        },
        methods: {
            handleClick() {
                this.myName='X';
            }
        }
    }
</script>
<style></style>
```

# setup和配置项写法的比较
1、data，methods配置项可以同setup配置项共存。  
2、data，methods配置项里面可以通过this获取得到setup中return出去的属性和方法。（反向不行）  
