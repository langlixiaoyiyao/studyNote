# vue的响应式
## vue3响应式写法
### ref
要点：  
1、ref(target)，target是基本类型或者对象，返回值是对象带有value属性的对象。
```
<template>
    <div>{{name}}</div>     // 不需要.value，因为模板会自己调用.value
</template>
<script lang='ts' setup name='Person'>
    import {ref} from 'vue';
    let name = ref('张三');
    let person = ref({
        firstName: 'huang',
        age: 18,
    })
    function changeName {
        name.value = '李四';        // 模板渲染会跟着变（响应式），需要.value进行修改
        console.log(name.value);
    };
    function changePerson {
        person.value.firstName = 'xiao';    // 响应式
        person.value = {                    // 响应式
            firstName: 'hong',
            age: 19,
        }
    }
</script>
```

### reactive
要点：  
1、只能用来创建对象（包括数组）类型的响应式数据。  
```
<template>
    <div>{{person.name}}</div>     
</template>
<script lang='ts' setup name='Person'>
    import {reactive} from 'vue';
    let person = reactive({
        name: 'huang',
        age: 18,
    })
    function changeName {
        person.name = '李四';        // 模板渲染会跟着变（响应式）
        console.log(person.name);
    };
    function changePerson {
        person.name = 'xiao';    // 响应式
        person = Object.assign(person, {    // 只有这样写才有响应式，直接赋值新的对象给person是不会有响应式的
            name: 'xiao',
            age: 19,
        })
    }
</script>
```

### ref和reactive用来创建响应式数据的区别
1、ref可以用来创建基本类型的响应式数据和对象类型的响应式数据
2、reactive只能用来创建对象类型的响应式数据
3、其实ref内部对于创建对象类型的响应式数据其实是调用了reactive
4、用ref创建的响应式数据需要调用.value来进行读取或者修改  

### ref和reactive的应用规则
1、对于创建基本类型的响应式数据只能用ref  
2、对于创建对象类型但层次不深的对象数据可以用ref或者reactive  
3、对于层级结构比较深的对象数据的响应式建议用reactive  


## vue2的响应式写法
vue2中只要把数据写到data配置项就是响应式的。但是vue不能检测数组和对象的变化。（数组的长度的增加，对象属性的增加）。  
### 对于对象属性的增加
```
var vm = new Vue({
    data: {
        person: {
            a: 1,
        }
    }
    methods: {
        changePerson: function() {
            this.person.a = 2;     // 响应式
            // this.person.b = 3; 非响应式
            this.$set(this.person, 'b', 3); // 响应式 增加一个属性
            this.person = Object.assign({}, this.person, {b: 3, c: 5});     // 响应式 增加多个属性
        }
    }
})
```

### 对于数组
说明：  
1、vue不能响应通过index增加数组数据  
2、vue不能响应通过.length修改数组长度  
3、Array的push(),shift()...等方法可以触发vue的响应式，具体详细方法可查看vue2官网
解决：  
1、可以用this.$set(原数组, 索引, 新增加的item);  
2、可以通过Array.splice()方法