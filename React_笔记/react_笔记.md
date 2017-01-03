1. React的基本认识
  * Facebook开源的一个js库
  * 一个用于构建用户界面的js库
  * React的核心思想: 通过构建可复用组件来构建用户界面
  * React的特点
    * Declarative(声明式编码)
    * Component-Based(组件化编码)
    * Learn Once, Write Anywhere(支持客户端与服务器渲染)
    * 高效
    * 单向数据流
  * React高效的原因
    * 虚拟(virtual)DOM, 不总是直接操作DOM
    * 高效的DOM Diff算法, 最小化页面重绘
2. 使用React
	* 导入js库文件(react.js, react-dom.js, babel.js)
	* 在页面中导入
	* 编码:
		```
      <div id="container"></div>
      
      <script type="text/babel">
        var aa = 123
        ReactDOM.render(<h1>{aa}</h2>, containerDOM);
      </script>
		```
3. JSX
	* 全称: JavaScript XML
  * react定义的一种类似于XML的JS扩展语法: XML+JS
  * 作用: 用来创建react虚拟DOM(元素)对象
	* js中直接可以套标签, 但标签要套js需要放在{}中
	* 在解析显示js数组时, 会自动遍历显示
	* 把数据的数组转换为标签的数组: 
		```
      var liArr = dataArr.map(function(item, index){
        return <li key={index}>{item}</li>
      })
		```
	* 注意:
    * 标签必须有结束
    * 标签的class属性必须改为className属性
    * 标签的style属性值必须为: {{}}
4. Component : React是面向组件编程的(组件化编码开发)
	* 基本理解和使用
		* 自定义的标签: 组件类(构建函数/一般函数/类)/标签
		* 创建组件类
      ```
      //方式1: 无状态函数(最简洁, 推荐使用)
      function MyComponent1() {
        return <h1>自定义组件标题11111</h1>;
      }
      //方式2: ES6类语法(复杂组件, 推荐使用)
      class MyComponent3 extends React.Component {
        render () {
          return <h1>自定义组件标题33333</h1>;
        }
      }
      //方式3: ES5老语法(不推荐使用了)
      var MyComponent2 = React.createClass({
        render () {
          return <h1>自定义组件标题22222</h1>;
        }
      });
      ```
		* 渲染组件标签
			```
			ReactDOM.render(<MyComp />,  cotainerEle);
			```
    * ReactDOM.render()渲染组件标签的基本流程
      * React内部会创建组件实例对象
      * 得到虚拟DOM并解析为真实DOM
      * 插入到指定的页面元素内部
	* props
    * 数据结构：对象
    * 内部结构：{组件实例对象的属性名： 属性值}
    * props的数据是只读的，不能修改
		* 所有组件标签的属性的集合对象
		* 给标签指定属性, 保存外部数据(可能是一个function)
		* 在组件内部读取属性: this.props.propertyName
		* 作用: 从目标组件外部向组件内部传递数据
		* 对props中的属性值进行类型限制和必要性限制
      ```
      Person.propTypes = {
        name: React.PropTypes.string.isRequired,
        age: React.PropTypes.number.isRequired
      }
      ```
    * 扩展属性: 将对象的所有属性通过props传递
        ```
        <Person {...person}/>
        ```
  * 组件的组合(组件嵌套)
    * 组件标签中包含子组件标签
    * 拆分组件: 拆分界面, 抽取组件
    * 通过props传递数据
	* refs    --->refs属性读取的是标签的属性值
    * 数据结构：对象
    * 内部结构：{打上ref标记的标签的ref这个属性名的属性值： 打上ref的标签}
		* 组件内包含ref属性的标签元素的集合对象
		* 给操作目标标签指定ref属性, 打一个标识
		* 在组件内部获得标签对象: this.refs.refName(只是得到了标签元素对象)
		* 作用: 操作组件内部的真实标签dom元素对象
  * 事件处理
    * 自定义的事件处理, 通过事件委托的方式实现(委托给组件的根标签)
    * 给标签添加属性: onXxx={this.eventHandler}
    * 在组件中添加事件处理方法
      ```
        eventHandler(event) {
                    
        }
      ```
    * 使自定义方法中的this为组件对象
      * 在constructor()中bind(this)
      * onXxx={this.eventHandler.bind(this)}
      * 使用箭头函数定义方法(ES6模块化编码时才能使用)
	* state
		* 组件被称为"状态机", 页面的显示是根据组件的state属性的数据来显示
		* 初始化指定:
        ```
        constructor() {
          super();
          this.state = {
            stateName1 : stateValue1,
            stateName2 : stateValue2
          };
        }
        ```
		* 读取显示: 
		    this.state.stateName1
		* 更新状态-->更新界面 : 
		    this.setState({stateName1 : newValue})
	* 实现一个双向绑定的组件
		* React是单向数据流
		* 需要通过onChange监听手动实现
	* 组件生命周期
		* 组件的三个生命周期状态:
      * Mount：插入真实 DOM
      * Update：被重新渲染
      * Unmount：被移出真实 DOM
    * 生命周期流程:
      * 第一次初始化显示
        ```
        constructor()
        componentWillMount() : 将要插入回调
        render() : 用于插入虚拟DOM回调
        componentDidMount() : 已经插入回调
        ```
      * 每次更新state
        ```
        componentWillUpdate() : 将要更新回调
        render() : 更新(重新渲染)
        componentDidUpdate() : 已经更新回调
        ```
      * 删除组件
        ```
        ReactDOM.unmountComponentAtNode(document.getElementById('example')) : 移除组件
        componentWillUnmount() : 组件将要被移除回调
        ```
    * 常用的方法
      ```
      render()
      constructor()
      componentDidMount() : 只执行一次, 已经在dom树中, 适合启动/设置一些监听
      ```   
5. ajax
	* React没有ajax模块, 需要使用其它ajax库
	* 一般是在componentDidMount中发送ajax请求, 得到数据后, 更新state
	* 发送ajax请求的库: fetch.js
	  * fetch是新的发送ajax请求的方式(完全区别于XMLHttpRequest及其封装)
	  * fetch的优点:
	    * 语法简洁，更加语义化
	    * 基于标准Promise实现
	  * 基本语法:
	    ```
	    fetch("http://blog.parryqiu.com")
        .then(response => {
           response.json().then(result => {
              //处理result
           })
        })
        .catch(e => {
           //处理异常
        })
	    ```
    * Fetch 替换 XHR 只是时间问题
	* 发送ajax请求的库: axios
	  * Promise based HTTP client for the browser and node.js
	  * 语法:
	    ```
	      //get请求
        axios.get('/user?ID=12345')  
          .then(function (response) {
            console.log(response);
          })
          .catch(function (error) {
            console.log(error);
          });
        //post请求
        axios.post('/user', {
            firstName: 'Fred',
            lastName: 'Flintstone'
          })
          .then(function (response) {
            console.log(response);
          })
          .catch(function (error) {
            console.log(error);
          });
	    ```
    
6. 应用编码:
	* 拆分组件
	* 数据结构的设计
	* props设计
	* state设计
	* 自定义事件处理(消息发布/订阅): pubsub.js
    * PubSub.subscribe("事件名", function(eventName, data){})
    * PubSub.publish("事件名", data) : 发布事件

7. 组件总结
  * 组件的组成
    * html
    * css
    * js
    * 图片
  * 为什么要整组件化开发
    * 应用开发越来越复杂(结构/行为)--> 简化开发--->拆分界面--->多个组件
    * 多个界面有相同的功能(可能有一些变化部分)-->提高复用
      -->抽取成一个组件(使用props技术解决变化部分)-->各个界面只使用组件标签就可以轻松实现效果

8.实现组件间通信方式1: 
* 父组件向子组件传递数据
  * 数据(包含对数据操作的函数)都在父组件里
  * 数据只能是当前组件和子组件使用, 不能给兄弟组件使用
  * 共同的数据放在父组件上, 特有的数据放在自己组件内部
  * 一般数据---> 用于组件页面显示
  * 函数数据--->调用执行
  * 父子组件的通信 
* 实现组件间通信方式2: 
  * 使用消息订阅(subscribe)-发布(publish)机制
  * 工具库: PubSubJS
  * 下载: npm install pubsub-js --save
  * 使用: 
    ```
    import PubSub from 'pubsub-js' //引入
    PubSub.subscribe('delete', function(data){ }); //订阅
    PubSub.publish('delete', data) //发布消息
  
总结：三大属性props,refs,state
* props里面存放的是静态属性，不会变化的值，
  内部结构：{组件实例对象的所有属性名： 属性值}
  作用：能够从组件对象外部获取到数据，包括从其父组件获取数据（对象和函数）
* state里面存放的都是动态属性，就是属性值是会变化的
  作用：当state里面的属性值变化时，就会更新页面。
        在state中可以进行页面数据的初始化,初始化工作写在class中的constructor中,因为在每次挂载组件标签对象时，
        首先会调用constructor()方法，例如
        ```
        this.state= {msg: ''}
        ```
        读取state可以通过this.state.msg
        更新state可以通过this.setState({msg: '小古'})
* refs是用来标记指定的真实dom元素，可以为想获取的元素指定ref='username'属性
      通过this.refs.username获取到绑定ref属性的元素
  内部结构：{打上ref标记的标签的ref这个属性名的属性值： 打上ref的标签}