# vue中的props属性
父组件给子组件传递参数，子组件通过props属性接收参数

## vue3中的props
1、vue3中可以通过宏函数defineProps接受参数，define开头的函数是宏函数，不需要导入就可以使用。  

```
// 父组件给子组件传递参数
<Person a='1' />

// 子组件person
<script setup>
    defineProps(['a']); // 这样接受的参数可以在模板中使用，但无法在script标签中使用
    const allProps = defineProps(['a']); // allProps是个对象，保存了所有你接收的参数

    // typescrip 写法，有默认值
    const allProps = withDefault(defineProps<{a?: number[]}>(['a']), {
        list: () => []
    })
</script>
```

## vue2中的props
```
<script>
    export default {
        name: 'Person',
        props: ['a'],       // script中可以使用this.a访问，模板可以直接使用a
    }
</script>
```