# vue表单课程

* v-model

     &ensp;&ensp;vue通过v-model 实现数据表单元素的数据双向绑定。v-model通过自动判断相应元素类型选择正确的方式实现元素的更新，从而监听用户的输入事件和更新数据。


    v-model 会忽略所有表单元素的 value、checked、selected 特性的初始值而总是将 Vue 实例的数据作为数据来源。你应该通过 JavaScript 在组件的 data 选项中声明初始值。

  > v-model 在内部使用不同的属性为不同的输入元素并抛出不同的事件：<br>
    &ensp;&ensp;text 和 textarea 元素使用 value 属性和 input 事件；<br>
    &ensp;&ensp;checkbox 和 radio 使用 checked 属性和 change 事件；<br>
    &ensp;&ensp;select 字段将 value 作为 prop 并将 change 作为事件。

关于v-model的详细概念见前章 [v-model](http://v-model.com)


* 基本元素

  1. 文本
    ----
          <div>
            <p>文本框 input元素</p>
            <input v-model='message'  placeholder="编辑我……">
            <p>消息是: {{ message }}</p>
          </div>
          <script>
            new Vue({
            el: '#app',
            data: {
            message : '初始值'
            }
            })
          </script>
    ----

  2. 多行文本
    ----
        <div>
          <p>文本框 textare元素</p>
          <textarea v-model='message'  placeholder="编辑我……">
          </textare>
          <p>消息是: {{ message }}</p>
        </div>
        <script>
          new Vue({
          el: '#app',
          data: {
            message : '初始值'
          }
          })
        </script>
    ----

  3. 复选框
<br>单个复选框，数据绑定到布尔值。
<br>多个复选框，数据绑定到同一个数组中去。
  ----
        <div id="app">
        <p>单个复选框：</p>
        <input type="checkbox" id="checkbox" v-model="checked">
        <label for="checkbox">{{ checked }}</label>
        <p>多个复选框：</p>
        <input type="checkbox" id="ck1"  v-model="checkedNames">
        <label for="ck1">复选项1</label>
        <input type="checkbox" id="ck2"  v-model="checkedNames">
        <label for="ck2">复选项2</label>
        <input type="checkbox" id="ck3"  v-model="checkedNames">
        <label for="ck3">复选项3</label>
        <br>
        <span>选择的值为: {{ checkedNames }}</span>
        </div>
        <script>
        new Vue({
        el: '#app',
        data: {
          checked : false,
          checkedNames: []
        }
        })
        </script>
  ----
  
  4. 单选按钮
  ----
        <div id="app">
          <input type="radio" id="se1" v-model="selected">
          <label for="se1">选项1</label>
          <br>
          <input type="radio" id="se2" v-model="selected">
          <label for="se2">选项2</label>
          <br>
          <span>选中值为: {{ selected }}</span>
        </div>
        <script>
          new Vue({
          el: '#app',
          data: {
            selected : 'Runoob'
          }
          })
        </script>
  ----

  5. select 列表
  ----
        <div id="app">
          <select v-model="selected">
            <option value="列表1">列表1</option>
            <option value="列表2">列表2</option>
            <option value="列表3">列表3</option>
          </select>
          <div>
            选择的选项为: {{selected}}
          </div>
        </div>
        <script>
          new Vue({
          el: '#app',
          data: {
            selected: ''
          }
          })
        </script>
  ----
  
* 数据绑定

  &nbsp;&nbsp;&nbsp;&nbsp;通过v-model实现表单元素数据的双向绑定，v-model不过是语法糖，通过自动判断相应元素类型，从而响应用户输入事件和完成数据的更新。

* 修饰符
  1. .lazy

  在默认情况下，v-model 是在input输入时实时同步输入框的数据，而lazy修饰符，可以使其在失去焦点或者敲回车之后在更新。

        <input v-model.lazy="msg" >

  2. .number

  将输入的值转化为数值类型

        <input v-model.number="msg" type="number">

  3. .trim

  自动去除输入值的首尾空白字符

        <input v-model.trim="msg">