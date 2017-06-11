# vue

Vue是构建用户界面的渐进框架。与其他整体框架不同，Vue是从根本上设计的，以便逐步采用。
Vue能完美的为先进的单页面应该用程序提供支持。

使用vue就是在vue.js中创建一个ViewModel。ViewModel是Vue.js的核心，是一个Vue实例。
ViewModel中的DOM Listeners工具会检测页面上DOM元素的变化，进而更改数据。

使用Vue的过程分为三个部分。
* 定义View
* 定义Model
* 创建Vue实例将View和Model连接起来。

## 例子
```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>

    <body>
        <div id="app">
            {{ message }}
        </div>
        <!--//view-->
    </body>
    <script src="http://static.runoob.com/assets/vue/1.0.11/vue.min.js"></script>
    <script>
        var exampleData = {
            message: 'Hello World!'
        }//model

        new Vue({
            el: '#app',
            data: exampleData
        })
    </script>
</html>
```
通过这个例子可以看出，在div处是我们的View，然后var exampleData处是创建了一个model，最后
再传附件一个Vue来连接View和Model。运行中{{message}}会被数据对象message属性替换，所以页面上
会输出“Hello World”。
要是想要再输入的同时，立刻就更改文本内容，将div中的代码改成下列代码就可以了：

    <p>{{message}}</p>
    <input type="text" v-model="message"/>

将message绑定到书文本框，就实现同时更改了。

## Vue.js的常用指令

* v-if,v-else
* v-show
* v-for
* v-bind
* v-on

---------------------

### v-if & v-else
v-if后面直接跟表达式，通过判断表达式的真伪来删除和插入元素，基本语法：v-if="expression"
expression返回值是一个bool值。
v-else指令是在v-if后添加一个else块，要跟再v-if后面才能够被识别
```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>
    <body>
        <div id="app">
            <h1>Hello, Vue.js!</h1>
            <h1 v-if="yes">Yes!</h1>
            <h1 v-else>No!</h1>
            <h1 v-if="age >= 21">Age: {{ age }}</h1>
            <h1 v-else>Name: {{ name }}</h1>
        </div>
    </body>
    <script src="http://static.runoob.com/assets/vue/1.0.11/vue.min.js"></script>
    <script>
        var vm = new Vue({
            el: '#app',
            data: {
                yes: true,
                age: 25,
                name: 'keepfool'
            }
        })
    </script>
</html>
```
* 数据yes的属性是true，所以Yes被输出，如果属性为false，就会输出NO
* 因为age >= 21，所以被输出，要是age的值小于21就会输出name。

### v-for

v-for的作用就是根据一组数据的选项列表进行渲染，它的语法就是：

    v-for="item iin items"

items是一个数组，item是数组元素。
#### 示例

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <title></title>
    <link rel="stylesheet" href="styles/demo.css" />
</head>

<body>
    <div id="fruit">
        <table border="1">
            <thead>
                <tr>
                    <th>Fruit</th>
                    <th>Color</th>
                    <th>Sweet or not Sweet</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="fruit in fruits">
                    <td>{{ fruit.name }}</td>
                    <td>{{ fruit.age }}</td>
                    <td>{{ fruit.sex }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</body>
<script src="http://static.runoob.com/assets/vue/1.0.11/vue.min.js"></script>
<script>
    var vm = new Vue({
        el: '#fruit',
        data: {
            fruits: [{
                name: 'Apple',
                age: 1,
                sex: 'sweet'
            }, {
                name: 'Banana',
                age: 2,
                sex: 'sweet'
            }, {
                name: 'Orange',
                age: 3,
                sex: 'not sweet'
            }, {
                name: 'Pear',
                age: 2,
                sex: 'sweet'
            }]
        }
    })
</script>
</html>
```

这一段代码最后的效果就是一个将数组中的数据用一个表格输出。
这段代码中，在选项对象的data属性中定义了一个fruits数组，然后
用v-for便利fruit对象的名字、年份和甜度。
因为v-if将数组中的数据遍历了一边，所以表格就会有四行。


### v-bind
v-bind 指令用于响应地更新 HTML 特性
v-bind指令可以在其名称后带一个参数，用冒号隔开。

#### 示例

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <title></title>
    <link rel="stylesheet" href="styles/demo.css" />
    
</head>

<body>
    <div id="app">

        <ul class="pagination">
            <li v-for="n in pageCount" >
                <a v-bind:class="activeNumber === n + 1 ? 'active' : ''">{{ n + 1 }}></a>
            </li>
        </ul>
    </div>
</body>
<script src="js/vue.js"></script>
<script>
    var vm = new Vue({
        el: '#app',
        data: {
            activeNumber: 10,
            pageCount: 20

        }
    })
</script>

</html>
```
这段代码的效果就是输出一行数据，然后将一个数字的框进行高亮标记。
输出一串数字还是通过v-for对pageCount从0开遍历。而当前的高亮的数字则通过

    v-bind:class="activeNumber === n + 1 ? 'active' : ''"

这段代码实现，activeNumber在data中已经有一个值，然后当v-for遍历到判断语句成立的时候，就会高亮。

### v-on
v-on指令用于给监听DOM事件，后面也是用冒号隔开然后再跟上方法。
有两种形式调用方法：绑定一个方法（让事件指向方法的引用），或者使用内联语句。

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <title></title>
</head>

<body>
    <div id="app">
        <p><input type="text" v-model="message"></p>
        <p>
            <button v-on:click="greet">Greet</button>
            <button v-on:click="say('Hi')">Hi</button>
        </p>
    </div>

</body>
<script src="js/vue.js"></script>
<script>
    var vm = new Vue({
        el: '#app',
        data: {
            message: 'Hello, Vue.js!'
        },
        methods: {
            greet: function() {
                alert(this.message)
            },
            say: function(msg) {
                prompt("hello", "陈尔磊")
            }
        }
    })
</script>
</html>
```
### 综合代码

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <title></title>
    <link rel="stylesheet" href="styles/demo.css" />
    <style type="text/CSS">
        body{margin: 0;padding: 0;} #fieldest{width: 260px;height: 400px;float: left;} #table{width: 350px;height: 400px;}
    </style>
</head>

<body>
    <div id="app">

        <fieldset id="fieldest">
            <legend>
                水果管理系统
            </legend>
            <div class="form-group">
                <label>水果名:</label>
                <input type="text" v-model="newFruit.name" />
            </div>
            <div class="form-group">
                <label>保质期:</label>
                <input type="text" v-model="newFruit.age" />
            </div>

            <div class="form-group">
                <label>颜色:</label>
                <select v-model="newFruit.sex">
                    <option value="深色">深色</option>
                    <option value="浅色">浅色</option>
                </select>
                <!--<label>是否过期:</label>
                <select v-model="newFruit.lx1">
                    <option value="过期">过期</option>
                    <option value="未过期">未过期</option>
                </select>-->
            </div>

            <div class="form-group">
                <label></label>
                <button @click="createFruit">Create</button>
            </div>
        </fieldset>
        <table id="table">
            <thead>
                <tr>
                    <th>水果名</th>
                    <th>保质期</th>
                    <th>颜色</th>
                    <th>是否过期</th>
                    <th>删除</th>

                </tr>
            </thead>
            <tbody>
                <tr v-for="fruit in fruits">
                    <td>{{ fruit.name }}</td>
                    <td>{{ fruit.age }}</td>
                    <td>{{ fruit.sex }}</td>
                    <td v-if="fruit.age >= 30">{{fruit.lx1}}</td>
                    <td v-else>{{fruit.lx2}}</td>
                    <td :class="'text-center'">
                        <button @click="deleteFruit($index)">删除</button></td>
                </tr>
            </tbody>
        </table>
    </div>
</body>
<script src="js/vue.js"></script>
<script>
    var vm = new Vue({
        el: '#app',
        data: {
            newFruit: {
                name: '',
                age: '',
                sex: 'Male',
                lx1: '过期',
                lx2: '未过期'


            },
            fruits: [{
                name: '苹果',
                age: 30,
                sex: '浅色',
                lx1: '过期',
                lx2: '未过期'
            }, {
                name: '梨子',
                age: 26,
                sex: '浅色',
                lx1: '过期',
                lx2: '未过期'

            }, {
                name: '香蕉',
                age: 22,
                sex: '浅色',
                lx1: '过期',
                lx2: '未过期'
            }, {
                name: '樱桃',
                age: 36,
                sex: '深色',
                lx1: '过期',
                lx2: '未过期'

            }]
        },
        methods: {
            createFruit: function() {
                this.fruits.push(this.newFruit);
                this.newFruit = {
                    name: '',
                    age: '',
                    sex: '深色',
                    lx1: '过期',
                    lx2: '未过期'
                }
            },
            deleteFruit: function(index) {
                this.fruits.splice(index, 1);
            }
        }
    })
</script>

</html>
```


