# 一、计算属性
+ 复杂逻辑处理尽量使用计算属性

```JavaScript
let test = new Vue({
  el : '#app',
  // 计算属性，类似于方法的定义，区别在于methods没有缓存   并且计算属性的方法会自定绑定到getter上，本质上是一个取值器
  // 计算属性有缓存，也就是意味着只有当实例中的数据改变时才会再次调用方法更新依赖，不同于methods的每次都要执行对应的方法
  computed : {
    fullName : function(){
      return this.firstName + ' ' + this.lastName; // 拼接姓名的例子
    }
  },
  methods : {
    getFullName : function(){
      return this.firstName + ' ' + this.lastName; // 会反复调用
    }
  }
})
```

+ 计算属性有缓存，只需要执行一次对应的回调，除非对应的响应式依赖的数据需要重新计算，否则只需要从缓存中获取数据；

# 二、侦听器

1. 除了使用watch属性之外，还可以使用vm.$watch API侦听数据的变化；

2. 作用：侦听某个变量，当变量对应的的值改变时执行相应地函数；

3. 语法：watch: {监听的变量名(){ 执行某些操作 }}

    ```html
    <div class="app">{{message}} {{name}}</div>
    
    <script src="../vue.js"></script>
    <script>
      const test = new Vue({
        el: '.app',
        data: {
    			message: '王宝鸡',
    	    name: '王兴强'
        },
    	  watch: {
        	// 监听message值是否改变
        	message(newVal,oldVal){
        		this.message = newVal
    	    },
    		  name(newVal,oldVal){
        		this.name = newVal
    		  }
    	  }
      })
    </script>
    ```