# jqLite

## jqLite 是什么
> jqLite 是angular使用的一个裁剪版本的jquery，所以jqLite具有jquery的一些基本的操作方法

## 创建元素
    angular.element('<div>')

## jqLite的一些特别的、不同于jquery的方法
    1、children() 获取某个元素下面的亲代子元素，返回是一个数组，数组中的每一项代表着dom元素，每一项.eq(索引)可以获取对应的jqLite对象。该函数不支持jquery所提供的选择器特性
    2、find(tag) 获取某个元素下面的标签名为tag的后代元素，该函数不支持jquery所提供的选择器特性
    3、parent() 返回父元素，该函数不支持jquery所提供的选择器特性

## jqLite 访问angularjs特性
> jqLite 还实现了下列这些方法,用来访问angular的特性
    1、controller() 或者 controller(name) 返回当前与当前元素或其父元素相关联的控制器
    2、injector() 返回当前与当前元素或其父元素相关联的注入器
    3、isolatedScope() 如果当前元素有相关联的独立的作用域，则返回该作用域
    4、scope() 返回当前与当前元素或其父元素相关联的作用域
    5、inheritedDate(key) 这个方法和jquery的data方法执行相同的功能，但是会沿着元素层次结构向上查找与指定key相匹配的值。

## 使用jquery代替jqLite
    在使用jqLite之前引入jquery.js 这样angular在安装jqLite之前会先检查jquery是否被加载，如果是则使用jquery，否则使用jqLite

## 注意
> 你可以利用jqLite提供的方法操作指令外部的dom元素，但不建议这么操作.
