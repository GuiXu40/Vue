# ---------------------表单和v-model------------------------
<p id="title"></p>

## :fish_cake:目录
#### <a href="#p1">:diamonds:基本用法</a>
#### <a href="#p2">:diamonds:绑定值</a>
#### <a href="#p3">:diamonds:修饰符</a>
<p id="p1"></p>

## :egg:基本用法
:spades:<a href="#title">回到目录</a><br>
可以实现表单数据的双向绑定
#### :hearts: text
```JavaScript
<body>
    <div id="app">
        <input type="text" v-model="message" placeholder="输入..">
        <p>输入的内容是 {{message}}</p>
    </div>
</body>
<script src="js/vue.min.js"></script>
<script>
    var app=new Vue({
        el: '#app',
        data: {
            message: ''
        }
    });
</script>
```
#### :hearts:textarea
```JavaScript
<body>
    <div id="app">
        <textarea name="" id="" cols="30" rows="10" v-model="text" placeholder="输入.."></textarea>
        <p>输入的内容是 {{text}}</p>
    </div>
</body>
<script src="js/vue.min.js"></script>
<script>
    var app=new Vue({
        el: '#app',
        data: {
           text: 'guixu'
        }
    });
</script>
```
**使用v-model后,表单控件显示的值只依赖所绑定的数据,不在关心初始化的value属性**

可以用@input替代v-model
```JavaScript
<body>
    <div id="app">
        <textarea name="" id="" cols="30" rows="10" @input="handle" placeholder="输入.."></textarea>
        <p>输入的内容是 {{text}}</p>
    </div>
</body>
<script src="js/vue.min.js"></script>
<script>
    var app=new Vue({
        el: '#app',
        data: {
           text: 'guixu'
        },
        methods: {
            handle: function(e){
                this.text=e.target.value;
            }
        }
    });
</script>
```
仔细观看渲染结果,有区别
#### :hearts:单选按钮
+ 单独使用时,不需要v-model,直接使用v-bind绑定一个布尔类型的值,为真时选中,为否时不选
```JavaScript
<body>
    <div id="app">
        <input type="radio" :checked="picked">
        <label for="">单选按钮</label>
    </div>
</body>
<script src="js/vue.min.js"></script>
<script>
    var app=new Vue({
        el: '#app',
        data: {
           picked: true
        }
    });
</script>
```
+ 组合使用来实现互斥选择的效果: 需要v-model配合value使用
```Javascript
<body>
    <div id="app">
        <input type="radio" v-model="picked" id="html" value="html">
        <label for="html">html</label>
        <br>
        <input type="radio" v-model="picked" id="javascript" value="javascript">
        <label for="javascript">javascript</label>
        <br>
        <input type="radio" v-model="picked" id="css" value="css">
        <label for="css">css</label>
        <p>选择的项为{{picked}}</p>
    </div>
</body>
<script src="js/vue.min.js"></script>
<script>
    var app=new Vue({
        el: '#app',
        data: {
           picked: 'javascript'
        }
    });
</script>
```
#### :hearts:复选框
+ 单独使用
```JavaScript
<body>
    <div id="app">
        <input type="checkbox" name="" id="checked" v-model="checked">
        <label for="checked">选择状态{{checked}}</label>
        <!-- <p>选择的项为{{picked}}</p> -->
    </div>
</body>
<script src="js/vue.min.js"></script>
<script>
    var app=new Vue({
        el: '#app',
        data: {
           checked: false
        }
    });
</script>
```
+ 组合使用
```JavaScript
<body>
    <div id="app">
        <input type="checkbox" name="" id="html" v-model="checked" value="html">
        <label for="html">html</label>
        <input type="checkbox" name="" id="css" v-model="checked" value="css">
        <label for="css">css</label>
        <input type="checkbox" name="" id="js" v-model="checked" value="js">
        <label for="js">js</label>
        <p>选择的项为{{checked}}</p>
    </div>
</body>
<script src="js/vue.min.js"></script>
<script>
    var app=new Vue({
        el: '#app',
        data: {
           checked: ['html','js']
        }
    });
</script>
```
#### :hearts:选择列表
单选与多选差别不大
```JavaScript
<body>
    <div id="app">
        <select name="" id="" v-model="selected">
            <option value="">html</option>
            <option value="js">javascript</option>
            <option value="">css</option>
        </select>
        <p>选择的项为{{selected}}</p>
    </div>
</body>
<script src="js/vue.min.js"></script>
<script>
    var app=new Vue({
        el: '#app',
        data: {
           selected: 'html'
        }
    });
</script>
```
多选
```JavaScript
<body>
    <div id="app">
        <select name="" id="" v-model="selected">
            <option value="">html</option>
            <option value="js">javascript</option>
            <option value="">css</option>
        </select>
        <p>选择的项为{{selected}}</p>
    </div>
</body>
<script src="js/vue.min.js"></script>
<script>
    var app=new Vue({
        el: '#app',
        data: {
           selected: ['html','js']
        }
    });
</script>
```
<p id="p2"></p>

## :egg:绑定值
:spades:<a href="#title">回到目录</a><br>
绑定一个动态的数据,搭配v-bind来实现

单选按钮
```JavaScript
<body>
    <div id="app">
        <input type="radio" name="" id="" v-model="picked" :value="value">
        <label for="">单选按钮</label>
        <p>{{picked}}</p>
        <p>{{value}}</p>
    </div>
</body>
<script src="js/vue.min.js"></script>
<script>
    var app=new Vue({
        el: '#app',
        data: {
           picked: false,
           value: 123
        }
    });
</script>
```
当选中时,picked==value==123

复选框:
```JavaScript
<body>
    <div id="app">
        <input type="checkbox" name="" id="" v-model="toggle" :true-value="value1" :false-value="value2">
        <label for="">复选框</label>
        <p>{{toggle}}</p>
        <p>{{value1}}</p>
        <p>{{value2}}</p>
    </div>
</body>
<script src="js/vue.min.js"></script>
<script>
    var app=new Vue({
        el: '#app',
        data: {
           toggle: false,
           value1: 'a',
           value2: 'b'
        }
    });
</script>
```
勾选时,toggle==value1,未勾选时toggle==Value2

#### :hearts:选择列表
```JavaScript
<body>
    <div id="app">
        <select name="" id="" v-model="selected">
            <option value="" :value="{number: 123}">123</option>
        </select>
        {{selected.number}}
    </div>
</body>
<script src="js/vue.min.js"></script>
<script>
    var app=new Vue({
        el: '#app',
        data: {
           selected: ''
        }
    });
</script>
```
当选中时,app.selected是一个Object
<p id="p3"></p>

## :egg:修饰符
:spades:<a href="#title">回到目录</a><br>
#### :hearts:.lazy
v-model默认在input事件中同步输入框的数据,使用修饰符.lazy会转变为change事件中同步
```JavaScript
<body>
    <div id="app">
        <input type="text" name="" id="" v-model.lazy="message">
        <p>{{message}}</p>
    </div>
</body>
<script src="js/vue.min.js"></script>
<script>
    var app=new Vue({
        el: '#app',
        data: {
           message: ''
        }
    });
</script>
```
#### :hearts:.number
将输入转换为Number类型
```JavaScript
<body>
    <div id="app">
        <input type="text" name="" id="" v-model.number="message">
        <p>{{typeof message}}</p>
    </div>
</body>
<script src="js/vue.min.js"></script>
<script>
    var app=new Vue({
        el: '#app',
        data: {
           message: 123
        }
    });
</script>
```
#### :hearts:.trim
可以自动过滤输入的首尾空格
```JavaScript
<body>
    <div id="app">
        <input type="text" name="" id="" v-model.trim="message">
        <p>{{message}}</p>
    </div>
</body>
<script src="js/vue.min.js"></script>
<script>
    var app=new Vue({
        el: '#app',
        data: {
           message: ''
        }
    });
</script>
```

总结: 感觉这个vue是真的强,避开所有渲染,方便!!加油学习
