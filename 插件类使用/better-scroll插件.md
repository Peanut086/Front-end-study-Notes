# 一、具体使用参考插件文档

文档地址：

https://better-scroll.github.io/docs/zh-CN/plugins/

# 二、使用中可能遇到的问题

## 1.contentHeight高度与预计不相符

+ 产生的原因：原因在于插件内部进行初始化content高度计算时，可能某些需要显示的数据还未渲染完毕，因此contentHeight高度有误
+ 解决办法：使用事件总线，监听某一个组件中的资源加载情况，该组件中每一个需要监听加载的子元素加载完成一次就refresh一次contentHeight
    + 原生的监听方式：`img.onload = function(){}`
    + vue实例中：`@load="fn"`

