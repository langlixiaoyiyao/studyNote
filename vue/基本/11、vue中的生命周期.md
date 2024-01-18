# vue 中的生命周期

## 父子组件的挂载顺序
子组件先挂载完毕，父组件后挂载完毕

## vue3中的生命周期钩子
### 创建 setup (不分前后)
```
<script setup>
    // 这里写组件的创建生命周期函数
</script>
```

### 挂载
#### 挂载前
```
<script setup>
    import { onBeforeMount } from 'vue';
    onBeforeMount(() => {
        
    })
</script>
```

#### 挂载后
```
<script setup>
    import { onMounted } from 'vue';
    onMounted(() => {

    })
</script>
```

### 更新
#### 更新前
```
<script setup>
    import { onBeforeUpdate } from 'vue';
    onBeforeUpdate(() => {

    })
</script>
```

#### 更新后
```
<script setup> 
    import { onUpdated } from 'vue';
    onUpdated(() => {

    })
</script>
```

### 卸载
#### 卸载前
```
<script setup>
    import { onBeforeUnMount } from 'vue';
    onBeforeUnMount(() => {

    })
</script>
```

#### 卸载后
```
<script setup>
    import { onBeforeUnMounted } from 'vue';
    onBeforeUnMounted(() => {
        
    })
</script>
```

## vue2中的生命周期钩子函数
### 创建
#### 创建前
```
<script>
    export default {
        name: '',
        data() {
            return {},
        },
        beforeCreate() {

        }
    }
</script>
```

#### 创建后
```
<script>
    export default {
        name: '',
        data() {
            return {},
        },
        created() {
            
        }
    }
</script>
```

### 挂载
#### 挂载前
```
<script>
    export default {
        name: '',
        data() {
            return {},
        },
        beforeMount() {
            
        }
    }
</script>
```

#### 挂载后
```
<script>
    export default {
        name: '',
        data() {
            return {},
        },
        mounted() {
            
        }
    }
</script>
```

### 更新
#### 更新前
```
<script>
    export default {
        name: '',
        data() {
            return {},
        },
        beforeUpdate() {
            
        }
    }
</script>
```

#### 更新后
```
<script>
    export default {
        name: '',
        data() {
            return {},
        },
        updated() {
            
        }
    }
</script>
```

### 销毁
#### 销毁前
```
<script>
    export default {
        name: '',
        data() {
            return {},
        },
        beforeDestory() {
            
        }
    }
</script>
```

#### 销毁后
```
<script>
    export default {
        name: '',
        data() {
            return {},
        },
        destoryed() {
            
        }
    }
</script>
```
