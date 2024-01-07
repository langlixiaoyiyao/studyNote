# vue3中toRefs和toRef的作用
## toRefs的作用
说明：将一个响应式对象转换成一个普通对象，这个普通对象的每个属性都是指向源对象相应属性的ref。每个单独的ref都是使用toRef创建的  
```
<template>
    <div>{{name}}</div>     
</template>
<script lang='ts' setup name='Person'>
    import {reactive, toRefs} from 'vue';
    let person = reactive({
        name: 'huang',
        age: 18,
    })
    let {name, age} = toRefs(person);
    function changeName {
        name = '李四';        // 模板渲染会跟着变（响应式）,而且person.name也会触发改变
        console.log(name);
    };
</script>
```

## toRef的作用
说明：将一个响应式对象里面的某个属性转换成一个响应式  
```
<template>
    <div>{{name}}</div>     
</template>
<script lang='ts' setup name='Person'>
    import {reactive, toRef} from 'vue';
    let person = reactive({
        name: 'huang',
        age: 18,
    })
    let toRef = toRef(person.name);
    function changeName {
        name = '李四';        // 模板渲染会跟着变（响应式）,而且person.name也会触发改变
        console.log(name);
    };
</script>
```