# 一、Vue内置指令

## 什么是指令？

指令就是vue内部提供的一些属性；

这些属性中封装好了Vue内部实现的一些功能，只要使用指令就可以快捷的实现这些功能。

------

## 1.`v-model`：双向数据绑定

+ vue默认是数据的单向绑定，但是使用v-model指令可以实现数据的双向绑定（仅限于input、textarea、select标签中）；

### 1.1 结合文本框使用

+ 单行文本(结合`text类型的input标签`)：

```html
<input type="text" v-model="msg1">
```

+ 多行文本（结合``textarea标签``）:

```html
<textarea cols="30" rows="1" v-model="msg2"></textarea>
```

###	1.2 结合选择按钮使用

####  复选框（`checkbox`）

+ 单个复选框：绑定到布尔值

```html
<input type="checkbox" id="b1" v-model="msg3">
<label for="b1">{{msg3}}</label>
```

+ 多个复选框：绑定到一个数组
    + 注意：多个复选框时，不要忘了给每个checkbox添加value属性，否则选一个全部都会选中

```html
<input type="checkbox" id="m1" v-model="msg4" value="肖战">
<label for="m1">肖战</label>
<input type="checkbox" id="m2" v-model="msg4" value="蔡徐坤">
<label for="m2">蔡徐坤</label>
<input type="checkbox" id="m3" v-model="msg4" value="王宝鸡">
<label for="m3">王宝鸡</label>
<input type="checkbox" id="m4" v-model="msg4" value="陈爽">
<label for="m4">陈爽</label>
<p>大傻逼们：{{msg4}}</p>
```

### 1.3 结合select标签使用

​	单选时绑定一个`值`：

```html
<div id="app">
    <p>选择的选项：{{names}}</p>
    <select name="ido" v-model="names">
      <option disabled value="">请选择</option> <!-- 这里需要给一个value值，刷新时才会有“请选择”的字样-->
      <option>王宝鸡</option>
      <option>肖战</option>
      <option>菜虚昆</option>
    </select>
  </div>
```

```js
new Vue({
      el: '#app',
      data: {
        names: ''
      }
    })
```

​	多选时绑定到`数组`更好：

```html
<div id="app">
    <p>选择的选项：{{names}}</p>
    <select name="ido" v-model="names" multiple>
      <option disabled value="">请选择</option> <!-- 这里需要给一个value值，刷新时才会有“请选择”的字样-->
      <option>王宝鸡</option>
      <option>肖战</option>
      <option>菜虚昆</option>
    </select>
</div>
```

```js
new Vue({
      el: '#app',
      data: {
        names: []
      }
    })
```

### 1.4 结合input的`radio`类型使用

### 1.5 v-model的`修饰符`

+ `.lazy`：默认情况下表单每次在input事件触发后将输入框的值与数据同步，使用.lazy修饰符后可以将input事件修改为change事件（change事件在表单完全输入完成后才触发）；
+ `.number`：使用该修饰符，可以自动将用户输入的内容转化为Number类型；
+ `.trim`：去掉用户输入的内容两端的空格；

------

## 2.插值指令

+  mustache语法：{{val}}

1. `v-once`：只编译渲染一次，之后vue实例中的数据变化时不再动态更新；
2. `v-html`：双大括号默认会将数据输出为文本形式，该指令能将数据以html的形式输出；
3. `v-text`：更新元素的textContent，相当于设置元素的innerText；
4. `v-pre`：跳过元素及其子元素的编译过程，显示原始的mustache；
5. `v-cloak`：隐藏未编译的mustache，直到编译完成，`需要和css规则搭配使用，比如 [v-cloak] {display:none}`；

------

## 3.条件渲染

条件判断指令主要有以下几个，在表达式值为true时才会渲染对应的元素；

1. `v-if`
2. `v-else`
3. `v-else-if`
4. `v-show`

v-if、v-else-if、v-else一起使用时，是否渲染主要看v-if，如果v-if对应的元素不渲染，那么就看v-else-if，如果还是不渲染，那么就渲染v-else；

v-else、v-else-if不能单独使用，并且两个指令所在的元素必须是相邻的兄弟元素；

v-if后面的值既可以从数据中获取，也可以直接在后面使用表达式；

**v-if和v-show的区别：**

- `v-if`：表达式为false时，不会渲染，html页面中也不会存在对应的元素；
- `v-show`：表达式为false时，修改元素的display属性为none，但是对应的元素仍会被渲染；
- 因此，在实际开发中，如果某个元素需要频繁的切换显示隐藏，那么使用v-show更合适，v-show修改的仅仅是元素的display属性，但是不管值如何都会被渲染到html结构中；v-if不适用于这种情况，由于v-if对应的值在true和false之间频繁切换导致的后果就是对应的元素会频繁的创建、移除，比较消耗性能；

------

## 4.循环遍历

`v-for`：根据数据多次渲染元素，相当于原生js中的for in循环；

1. 可以基于一个数组（或其他数据结构）来渲染一个列表；
2. v-for可以遍历的对象主要有以下几类：
    1. 数组
    2. 对象
    3. 数值
    4. 遍历器对象（iterator）
    5. 字符串
3. v-for的key属性：一般定义为数据结构中元素的key值，避免重复；设置key属性的原因主要是为了提高重复渲染时的效率；
4. 写法如下所示：

```html
<div>
  <ul>
    /*  可以遍历出的属性可以是key、value、index  */
    <li v-for="item in movies" key="item">{{item}}</li>
  </ul>
</div>
```

# 二、Vue自定义指令

## 1.自定义全局指令

+ 在需要对DOM元素进行底层操作的时候，就可以使用自定义指令，因为2.0版本之后虽然复用的形式是组件，但是并不能完全满足开发需求；

### 自定义指令的形式

```javascript
// 在全局Vue中注册
// 注意：这里的name就是指令名称，注册时不需要加上“v-”，vue内部会自动加上
Vue.directive('name',{
  // el参数就是使用该指令的元素，会被自动传入到该回调函数中
  钩子函数：function(el){
    // some code
  }
})
```

==注意：==这里的钩子函数需要视情况指定，比如说有些操作使用bind是无效的，需要用其他钩子函数；

## 2.局部自定义指令



## 3.钩子函数

一个指令定义对象可以提供如下几个钩子函数，都是可选的：

1. `bind`：只调用一次，指令第一次绑定到元素时调用，在这里可以进行一次性的初始化设置；
2. `inserted`:被绑定的元素插入到父节点时调用（只能保证父节点存在，不能保证百分百插入到父节点中）；
3. `update`：所有组件的Vnode更新时调用，也可能发生在其子Vnode更新之前；
4. `componentUpdated`：指令所在组件的Vnode及其子Vnode全部更新后调用；
5. `unbind`：只调用一次，指令与组件解绑时调用；

## 4.钩子函数参数

