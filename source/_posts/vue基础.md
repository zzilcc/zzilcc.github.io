---
title: vue基础
date: 2018-07-16 11:28:25
tags: Vue.js
categories: vue
---
## Vue.js是什么
Vue是一个前端框架，官方的解释是一套用于构建用户界面的渐进式框架。相对于React,AngularJS框架来说是比较轻量级的，然后比较容易上手，所以一开始选择学哪个框架的时候就选择了Vue,正好入职的第一家公司也是使用这个框架。
<!--more-->

## 下载
Vue有两个版本，一个开发版本，包含完整的警告和调试模式；一个是生产版本，删除了警告，进行了压缩。

GitHub地址传送门：[github](https://github.com/vuejs/vue)

## Vue实例
我们一般通过Vue函数创建一个新的Vue实例。

    var vue = new Vue({
        //选项
    });


## 声明式渲染

Vue是声明式渲染，这是Vue的核心，我看过比较好的解释就是“我们只需要告诉程序我们想要什么效果，其他交给程序去做”。

官网的例子就很好理解：

    <div id="app">
        {{message}} //Hi
    </div>
    
    var vue = new Vue ({
        el: "#app",
        data: {
            message: 'Hi!'
        }
    }) 
    
  通过这样我们已经把数据渲染进DOM，而且是响应式的。主要data里的message值发生变化，在页面上也会跟着变化。
    
## 选项
   
当创建一个实例后，我们可以传入一个选项对象，下面列出一些常用选项：

 * el
 * data
 * methods
 * computed
 
### el
 选择挂载目标，可以是css选择器，也可以是html元素，在实例挂载后，元素可以通过vue.$el访问。
 
 如果是在实例化时存在这个选项，实例将立即进入编译过程，否则需要显式调用vue.$mount()手动开始编译。
 
 ### data 
 Vue实例的数据对象。Vue是响应式的数据变化的，因为Vue会递归的将data的属性转换为getter/setter。data对象必须是纯粹的对象，也就是含有零个或多个的键值对。
 
 实例创建后，可以通过vue.$data访问，并且Vue实例，也就是vue实际上也代理了data对象上的不是以“_”或者“$”开头的属性。也就是vue.$data.a等价于 vue.a.
 
    <div id="app">
        {{message}}  //Hello,world
    </div>
 
    var vue = new Vue({
        el: "#app",
        data: {
            message: "Hello world!"
        }
    });
    
    vue.$data.message === vue.message //true
     
 ### methods
 用来定义一些方法，用这些方法是实现你想要的一些功能，比如点击事件，或者发送ajax请求等等。这些方法可以通过实例来访问，或者在指令表达式中使用，方法中的this会自动绑定为Vue实例。
    
    <div id="app">
         {{message}}  //Hello
         <button v-on:click="show">展示完整信息</button>//点击按钮后会出现Hello,world!
    </div>
    
    
    
    var vue = new Vue({
        el: "#app",
        data: {
            message: "Hello"
        },
        methods: {
            show: function() {
                return message = + ",world!"
            }
        }
    })
    
 在这个例子我们使用v-on命令，用来监听事件，这个命令下节会解释。我们在button标签里绑定了点击事件，所以一点击的时候，就会触发了show函数，该函数就会执行，所以message的值为“Hello,world！”。
 ### computed
 计算属性，它是基于依赖进行缓存的，只有相关的依赖的值发生了改变，才会重新执行函数，否则只会返回之前的结果。
  
 类型：{[key: string]: Function|{get: Function,set: Function}}
 

    var vue = new Vue({
        el: "#app",
        data: {
            a: 1
        },
        computed: {
            add: function() {
                 return this.a + 1
            }
        }
    })
   
 or
    
    var vue = new Vue({
        el: "#app",
        data: {
            a: 1
        },
        computed: {
            add: {
                get: function() {
                    return this.a + 1
                },
                set: function(data) {
                    this.a = data -1
                }
            }
        }
    })