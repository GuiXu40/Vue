# --------------------v-bind及class与class与style-----------------------
<p id="title"></p>

## :fish_cake:目录
#### <a href="#p1">:diamonds:v-bind简介</a>
#### <a href="#p2">:diamonds:绑定class的几种方式</a>
#### <a href="#p3">:diamonds:绑定内联样式</a>
<p id="p1"></p>

## :egg:v-bind简介
:spades:<a href="#title">回到目录</a><br>
作用就是: 动态更新HTML元素上的属性
<p id="p2"></p>

## :egg:绑定class的几种方式
:spades:<a href="#title">回到目录</a><br>
#### :hearts:对象语法
给v-bind:class设置一个**对象**,可以动态的切换class
```JavaScript
<body>
    <div id="app">
        <div :class="{'active': isActive}"></div>
    </div>
</body>
<script src="js/vue.min.js"></script>
<script>
    new Vue(
        {
            el: '#app',
            data: {
                isActive: true
            }
        }
    )
</script>
```
对象中可以传入多个属性可以实现**动态切换class**-->而且,:class可以与普通class共存
```JavaScript
<body>
    <div id="app">
        <div :class="{'active': isActive,'error': isError}"></div>
    </div>
</body>
<script src="js/vue.min.js"></script>
<script>
    new Vue(
        {
            el: '#app',
            data: {
                isActive: true,
                isError: false
            }
        }
    )
</script>
```
当:class的表达式过长或逻辑复杂时,还可以绑定一个计算属性
```Javascript
<body>
    <div id="app">
        <div :class="classes"></div>
    </div>
</body>
<script src="js/vue.min.js"></script>
<script>
    new Vue(
        {
            el: '#app',
            data: {
                isActive: true,
                error: null
            },
            computed: {
                classes: function(){
                    return {
                        active: this.isActice && this,error
                    }
                }
            }
        }
    )
</script>
```
#### :hearts:数组语法
当需要多个class时,可以使用数组语法,给class绑定一个数组,应用一个class列表
```JavaScript
<body>
    <div id="app">
        <div :class="[activeCls,errorCls]"></div>
    </div>
</body>
<script src="js/vue.min.js"></script>
<script>
    new Vue(
        {
            el: '#app',
            data: {
                activeCls: 'active',
                errorCls: 'error'
            }
        }
    )
</script>

<div class="active error"></div>
```
也可以使用三元运算符
```JavaScript
<body>
    <div id="app">
        <div :class="[isActive ? activeCls: '',errorCls]"></div>
    </div>
</body>
<script src="js/vue.min.js"></script>
<script>
    new Vue(
        {
            el: '#app',
            data: {
                isActice: true,
                activeCls: 'active',
                errorCls: 'error'
            }
        }
    )
</script>

<div class="active error"></div>
```
也可以使用对象语法替代运算
```JavaScript
<body>
    <div id="app">
        <div :class="[{'active': isActive},errorCls]"></div>
    </div>
</body>
<script src="js/vue.min.js"></script>
<script>
    new Vue(
        {
            el: '#app',
            data: {
                isActive: true,
                errorCls: 'error'
            }
        }
    )
</script>

<div class="active error"></div>
```
当然也可以使用data,computed和method三中方法
#### :hearts:在组件上使用
<p id="p3"></p>

## :egg:绑定内联样式
:spades:<a href="#title">回到目录</a><br>
语法: :style
