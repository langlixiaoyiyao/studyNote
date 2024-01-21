# vue中的ref属性

## vue3中的ref属性
### 加在html标签上
```
<template>
    <div ref="title"></div>
</template>
<script setup>
    import {ref} from 'vue';
    const title = ref();  // title.value存储的就是这个标签的dom元素
    console.log(title.value);
</script>
```
### 加在自定义组件上
```
<template>
    <Person ref="title"></Person>
</template>
<script setup>
    import {ref} from 'vue';
    import Person from '@/components/Person'
    const title = ref();  // title.value存储的就是这个组件的实例对象（但如果Person组件内部没有使用defineExpose导出东西，你这样是查看不了什么的）
    console.log(title.value);
</script>

// Person.vue
<script setup>
    import {ref} from 'vue';
    const num = ref(0);
    defineExpose({
        num
    })
</script>
```

## vue2中的ref属性
### 加在html标签上
```
<template>
    <div ref="input"></div>
</template>
<script>
    export default {
        name: 'Person',
        data() {
            return {
                a: 'a'
            }
        },
        mounted() {
            console.log(this.$refs.input); // 获取得到的就是dom元素
        }
    }
</script>
```

### 加在自定义组件上
```
// Person
<script>
export default {
    name: 'Person',
    data() {
        return {
            a: 'a'
        }
    }
}
</script>

// App.vue
<template>
    <Person ref="input"></Person>
</template>
<script>
    import Person from '@/components/Person.vue';
    export default {
        name: 'Person',
        component: {
            Person,
        }
        data() {
            return {
                a: 'a'
            }
        },
        mounted() {
            console.log(this.$refs.input.a); 
        }
    }
</script>

```