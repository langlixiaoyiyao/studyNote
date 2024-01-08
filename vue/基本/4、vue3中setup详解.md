# vue3中setup详解
## setup基础写法
```
<template>
    <div>{{name}}</div>
    <div @click="changeName">改变name</div>
</template>
<script>
    export default {
        name: "Person",
        setup() {
            let name = 'H';
            function changeName() {
                name = "V"              // 没有响应式
            }
            return {
                name,
                changeName
            }
        }
    }
</script>
```

## setup语法糖
要点如下：  
1、每个组件模板文件中要有两个script标签，两个script标签的lang属性要一致。  
2、第一个script标签内部使用export defalut 导出组件的name。  
3、第二个script属性加上setup属性，内部写变量或者函数，无需导出，template模板内部可使用该script定义的变量或者函数。  
  
说明：如果不写导出组件name的那个script标签，那么vue会默认文件名为组件的名字
```
<template>
    <div>{{name}}</div>
    <div @click="changeName">改变name</div>
</template>
<script lang='ts'>
    export default {
        name: "Person",
    }
</script>
<script lang='ts' setup>
    let name = 'H';
    function changeName() {
        name = "V"              // 没有响应式
    }
</script>
```

## setup高级写法
要点如下：  
1、可以只写那个拥有setup属性的script。  
2、安装vite-plugin-vue-setup-extend组件。  
3、在vite.config.ts导入vite-plugin-vue-setup-extend，并配置。  
4、在那个拥有setup属性的script上面加上name属性，值就是该组件的名字。 

```
// 安装vite-plugin-vue-setup-extend插件
npm i -D vite-plugin-vue-setup-extend
```
```
// vite.config.ts 配置代码如下
import { fileURLToPath, URL } from 'node:url'

import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import vueSetupExtend from 'vite-plugin-vue-setup-extend'

export default defineConfig({
    plugins: [
        vue(),
        vueSetupExtend(),
    ],
    resolve: {
        alias: {
        '@': fileURLToPath(new URL('./src', import.meta.url))
        }
    }
})
``` 
```
// 模板文件
<template>
    <div>{{name}}</div>
    <div @click="changeName">改变name</div>
</template>
<script lang='ts' setup name='Person'>
    let name = 'H';
    function changeName() {
        name = "V"              // 没有响应式
    }
</script>
```
