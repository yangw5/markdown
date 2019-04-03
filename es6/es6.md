## es6

### 新增数据结构

### 块级作用域 let const

  * 内层作用域不会影响外层作用域

  * let 暂时性死区（TDZ）

  * const 声明常量，地址不可变，但是可以新增属性值。

###  字符串拼接

        ` `

### 三点扩展运算符
扩展运算符将一个数组转为用逗号分隔的参数序列
* 将一个数组，变为参数序列

        let add = (x, y) => x + y;
        let numbers = [3, 45];
        console.log(add(...numbers))//48

* 合并数组

        [...arr1, ...arr2, ...arr3] 

* 使用push将一个数组添加到另一个数组的尾部
        
        a.push(...b)

* 将字符串转换为数组

        [...'hello']  
        // [ "h", "e", "l", "l", "o" ] 

* 转换伪数组为真数组

        var array = [...nodeList]; 

* map结构

        let map = new Map([  
        [1, 'one'],
        [2, 'two'],
        [3, 'three'], 
        ]);
        let arr = [...map.keys()]; // [1, 2, 3]



----
### Set 
* 定于：Set本身也是一种构造函数，用于生成Set数据结构，它类似于数组，但是成员中的值是唯一的，没有重复的。

        let a=[1,2,3,4,5,3,2,1];
        let b=new Set([...a]);//Set(5) {1,2,3,4,5}
        let c[...b];//c=[1,2,3,4,5] Set和Array互转
        let d=[...new Set(a)]//d=[1,2,3,4,5]

  * Set 可用于数组去重，或者检查对象中是否存在某属性值

* Set 拥有 add deleted has clear等方法进行数据的增加 删除 某元素是否存在 清除所有元素。

* 还可以通过 Set实例对象的keys()，values()，entries()方法进行遍历
----
### Map

* Map结构提供了“值—值”的对应，是一种更完善的Hash结构实现。如果你需要“键值对”的数据结构，Map比Object更合适。它类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。

* 实例属性和方法：size、set、get、has、delete、clear

* 遍历方法：keys（）、values（）、entries（）、forEach（）

----
### 迭代器 for ... in   for ...of

* Symbol.iterator

    1. 遍历器（Iterator）是一种接口，为各种不同的数据结构提供统一的访问机制。任何数据结构只要部署Iterator接口，就可以完成遍历操作（即依次处理该数据结构的所有成员）。
    
    2. Iterator的作用有三个：一是为各种数据结构，提供一个统一的、简便的访问接口；二是使得数据结构的成员能够按某种次序排列；三是ES6创造了一种新的遍历命令for...of循环，Iterator接口主要供for...of消费。

    3. 在ES6中，有些数据结构原生具备Iterator接口（比如数组），即不用任何处理，就可以被for...of循环遍历，有些就不行（比如对象）。原因在于，这些数据结构原生部署了Symbol.iterator属性（详见下文），另外一些数据结构没有。凡是部署了Symbol.iterator属性的数据结构，就称为部署了遍历器接口。调用这个接口，就会返回一个遍历器对象。

    4. 在ES6中，有三类数据结构原生具备Iterator接口：数组、某些类似数组的对象、Set和Map结构。

    5. 解构赋值，扩展运算符(...)，yield*_yield*后面跟的是一个可遍历的结构，它会调用该结构的遍历器接口，由于数组的遍历会调用遍历器接口，所以任何接受数组作为参数的场合，其实都调用

    6. 字符串是一个类似数组的对象，也原生具有Iterator接口。

    7. 遍历器对象除了具有next方法，还可以具有return方法和throw方法。如果你自己写遍历器对象生成函数，那么next方法是必须部署的，return方法和throw方法是否部署是可选的。

* for..of适用遍历数/数组对象/字符串/map/set等拥有迭代器对象的集合.但是不能遍历对象,因为没有迭代器对象.与forEach()不同的是，它可以正确响应break、continue和return语句

* for-of循环不支持普通对象，但如果你想迭代一个对象的属性，你可以用for-in循环（这也是它的本职工作）或内建的Object.keys()方法：
----
### Generator 生成器

  1. let f1=function *()
  2. yield

      逻辑划分，复杂的逻辑可以通过yield来暂停，

  3. next()

      返回一个对象，有done（表示这个Generator对象的逻辑块是否执行完成）和value属性（yield语句后的表达式的结果）
      还可以传递参数，赋值给yield关键字前面的变量声明。

    
----
### promise

  1. promise对象是一个构造函数

  1. 异步编程的解决方法，解决的回调地狱问题，

  1. 有三中状态：pending（进行中）、fulfilled（已成功）、rejected（已失败）

  1. Promise对象提供统一的接口

  1. Promise构造函数接收一个函数作为参数，该函数的两个参数分别是resolve和reject，他们是两个函数，由Javascript引擎提供，不用自己部署。
  
  1. promise实例生成以后，可以用then方法分别指定resolved状态和rejected状态的回调函数，then可以接受2个函数作为参数，第一个回调函数是promise对象的状态变为resolved时调用，第二个回调函数是promise对象的状态变为rejected时调用，其中，第二个函数是可选的，不一定要提供，这两个函数都接受promise对象传出的值作为参数；

  1. then方法返回的是一个新的Promise实例，then方法是定义在原型对象Promise.prototype上的。它的作用是为 Promise 实例添加状态改变时的回调函数，then内函数的参数可以接收resolve或者rejected函数的返回值。

          var getJSON = function (url) {
          var promise = new Promise( function(resolve,reject ) 
          {
            var XHR = new XMLHttpRequest();
            XHR.open("GET",url);
            XHR.onreadystatechange = function () 
            {
              if (this.readyState !==4) {return;}
              if(this.status == 200) {
               resolve(this.response);
              } else{
               reject(new Error(this.statusText) );
              }
            };
            XHR.responseType = "json";
            XHR.setRequestHeader("Accept","application/json");
            XHR.send();
          });
          return promise;
          };

          getJSON("posts.json").then(function(json){
          console.log("Contents : "+json );
          }, function(error) {
          console.log("出错了", error);
          }) ;

          //或者

          getJSON("posts/1.json").then(function(post){
          return getJSON(post.commentURL);
          }).then(function  funA(comments) {
          console.log("resolved:" ,comments);
          }, function funB(err){
          console.log("rejected：", err);
          });

          //或者

          getJSON("/post/1.json").then(
          post => getJSON(psot.commentURL)
          ).then(
          comments => console.log("resolved:",comments),
          err => console.log("rejected:" ,err)
          );

----
### async/await
  原理

  >如果async 函数中有返回一个值 ,当调用该函数时，内部会调用Promise.solve() 方法把它转化成一个promise 对象作为返回，但如果timeout 函数内部抛出错误呢？ 那么就会调用Promise.reject() 返回一个promise 对象,如果函数内部抛出错误， promise 对象有一个catch 方法进行捕获。

  作为一个关键字放到函数前面，用于表示函数是一个异步函数

  async 函数返回的是一个promise 对象

  await 关键字只能放到async 函数里面,会拿到promise resolve 的值并进行返回，然后继续向下执行。类似于promise .then()替换为await

  错误处理 通过 try...catch进行异常的抛出

    // 2s 之后返回双倍的值
    function doubleAfter2seconds(num) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve(2 * num)
        }, 2000);
    } )
    }
    async function testResult() {
    let result = await doubleAfter2seconds(30);
    console.log(result);
    }



---
### class
  *  constructor
  * class不存在变量提升