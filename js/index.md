# js




### JS1 js的数据类型有哪些（以及转换）

```js
答: 简单数据类型: number string boolean undefined   null
	复杂数据类型: object  function  array



数据类型转换： 
    转数字类型： parseInt(整数)  parseFloat（小数）  Number（不明确类型转换） +
    转字符串类型： xx+''   toString() null和undefined没有这个方法
    转布尔类型： Boolean() 
     除了 0,''（空引号）,null, undefined,NAN ，不成立的表达式 是false,
     其他均为true,一般用于if(条件判断)
    隐式转换：
    a.当加号的左边没有数字，后面有数字，加号被解析成正号，+号后面一定是数字类型
    b.任何数据和字符串相加都是字符串，除了NAN
    c.只要跟NAN沾边，一定是NAN
    字符串和NAN相加是字符串的NAN，typeOf类型是字符串
    d.精度丢失：
    0.1+0.2 = 0.30000000000000004
    计算机会把它转成二进制计算
    解决精度丢失问题：扩大到整数去运算
    ((0.1*100+0.2*100))/100 =0.3

+号的上下文：
a.当加号左边没有数字，只有右边有数字，加号被解析成正号，正号后面一定是数字类型
b.加号两边都是数字，加号就是运算符
c.+号的左右如果有一个数据是字符串数据类型的话  那么这个+号会被解析成连接符
   字符串的拼接：'+变量+'    模板字符串 `${变量}`
```

### JS2 typeof返回的数据类型

```js
答: number string boolean undefined  object  function 
   特殊情况：
   typeof null -->object
   typeof array -->object
   typeof function --> function
   typeof typeof 任何类型  -->string
   isNaN() 判断是否为NAN，返回布尔值true false


复杂数据类型判断
p instanceof Array

返回布尔值 看这个实例是不是有构造函数创建出来的
```

### JS3 运算符及优先级

```js
答: 
1.赋值运算符
   =  将符号右边的内容赋值到左边去，左边必须是个容器
   累加 a+ = 10  =>  a=a+10
2.自增自减运算符
变量++   先使用，再自增
++变量   先自增，再使用
共同点都在原来及基础上加1， 类似 a=a+1
面试题： （1+2模板）
 let a = 1; let b = ++a + ++a; console.log(b);   5
 let a = 1; let b = a++ + ++a; console.log(b);   4
 let a = 1; let b = a++ + a++; console.log(b);   3
 let a = 1; let b = ++a + a++; console.log(b);   4
 console.log(5++) 报错（存储容器）                console.log(++5)  报错（存储容器）

3.逻辑运算符（用于多个组合条件判断）
与 或 非
&& ||  ！
表达式1 && 表达式2    1、2均为true就为true
表达式1 || 表达式2    1、2一个为true就为true
! 取反

4.比较运算符
  >、 <、 >=、 <=、 ==、 ===、 !=、 !==
  多一个=,就是既比较类型也比较值，优先比较类型
  特殊说明（了解）
  如果是"数字"和"其他值"的比较 则其他值会自动转换成数  字去比较
涉及到"NAN"都是false （NaN）
如果是"字符串"和"字符串"比较 则会每一个字符的ASCII码去进行比较,同时是按位进行比较
'azzz'<'b' true
如果是布尔值参与比较 布尔值会转换成数字0和1
  

一元运算符： 运算符的左右只有一个数据的时候 ++ --
二元运算符： 运算符的左右有两个个数据的时候 + - * / %
三元运算符：  ？ 表达式1：表达式2

 const num1 = 10
      const num2 = 20
      const num3 = 30
console.log((num1 > num2 ? num1 : num2) > num3 ? (num1 > num2 ? num1 : num2) : num3)
...

优先级：（从高到低）
1.（）优先级最高
2.一元运算符 ++ -- ！
3.算数运算符 先* / % 再 + -
4.关系运算符 > >= < <=
5.相等运算符 == !=  ===  !==
6.逻辑运算符 先&& 后||
7.赋值运算符
表达式长以优先级最低的分


```

### JS4 什么是深拷贝什么是浅拷贝

```js
答: 浅拷贝: 拷贝对象的一层属性,如果对象里面还有对象,拷贝的是地址, 两者之间修改会有影响,适用于对象里面属性的值是简单数据类型的.
    深拷贝: 拷贝对象的多层属性,如果对象里面还有对象,会继续拷贝,使用递归去实现.
```

### JS5 如何实现深拷贝和浅拷贝

```js
答:
浅拷贝:  // 1.Object.assign() 浅拷贝(好多博客写错了!!) => React中常用!
        // 2. ES6 spread....操作符
    var obj = {
      class: 'UI',
      age: 20,
      love: 'eat'
    }
    function getObj(obj) {
      var newObj = {}
      for (var k in obj) {
        newObj[k] = obj[k]
      }
      return newObj
    }
    var obj2 = getObj(obj)
    console.log(obj2)

深拷贝: 二深拷贝 JSON.parse(JSON.stringify(对象))
		var obj = {
      class: '前端',
      age: 26,
      love: {
      friuts : 'apple',
      meat: 'beef'
      }
    }
		function getObj(obj) {
      var newObj = {}
      for (var k in obj) {
        /* if (typeof obj[k] == 'object') {
          newObj[k] = getObj(obj[k])
        } else {
          newObj[k] = obj[k]
        } */
        newObj[k] = typeof obj[k] == 'object' ? getObj(obj[k]) : obj[k]
      }
      return newObj
    }
    var obj2 = getObj(obj)
    console.log(obj2)
```

### JS6 对闭包的理解？并能举出闭包的例子（实现数据私有化）

```js
答: 闭包 函数和声明该函数的词法环境的组合(两个嵌套关系的函数,内部函数可以访问外部函数定义的变量)
    闭包的优点：1、形成私有空间，避免全局变量的污染
               2、持久化内存，保存数据
    闭包的缺点：1、持久化内存，导致内存泄露
    解决：1、尽快避免函数的嵌套，以及变量的引用
         2、执行完的变量，可以赋值null，让垃圾回收机制，进行回收释放内存（当不在引用的变量、对象，垃圾回收机制就会回收）
 （函数执行时，会为函数内部的局部变量，开辟内存空间，并在函数执行完成后，释放这块存储空间）

     垃圾回收机制：常见的浏览器垃圾回收算法: 引用计数 和 标记清除法
     1）引用计数：如果没有任何变量指向它了，说明该对象已经不再需要了。
         缺点：循环引用
     2）标记清除法：在JS中就是全局出发定时扫描内存中的对象，
         无法触及的对象，就会背回收。
         
例: 点击li获取当前下标
    <ul>
      <li>111</li>
      <li>222</li>
      <li>333</li>
      <li>444</li>
      <li>555</li>
    </ul>
      var lis = document.querySelectorAll('li')
      for (var i = 0; i < lis.length; i++) {
        (function (j) {
          lis[j].onclick = function () {
            console.log(j)
          }
        })(i)
      }
```

```js
    function addCount()
     {
          let count =0;
          function add() {
                count++;
                console.log('调用了'+count + '次')
          }
          return add
      }  //在闭包中，返回一个引用类型时，这块闭包的空间就不会释放
      let addFn = addCount()
      addFn()//1
      addFn()//2
      addFn = null //解决内存泄漏
```

### JS7 什么是原型和原型链

```js
答: 原型: 函数都有prototype属性,这个属性的值是个对象,称之为原型
   原型链: 对象都有__proto__属性,这个属性指向它的原型对象,原型对象也是对象,也有__proto__属性,指向原型对象的原型对象,这样一层一层形成的链式结构称为原型链.
   
   实例对象.`__proto__`  === 构造函数.prototype (相等)

   面试题： function Person() {}
		   let p = new Person()
          console.log(p.__proto__ === Person.prototype)   // true
          console.log(p.__proto__.constructor === Person) // true
       console.log(Person.prototype.constructor === Person) //true

```

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/33a2f195c0ff4837800326ffad34ea41.jpeg#pic_center)

### JS8 call、apply和bind的区别

```js
答: 1. call和apply方法都可以调用函数,方法内的第一个参数可以修改this的指向
	2. call方法可以有多个参数,除了第一个参数,其他参数作为实参传递给函数
		 apply方法最多有2个参数,第二个参数是个数组或伪数组,数组里面的每一项作为实参传递给函数
	3. bind方法不能调用函数,返回值是一个函数，它会创建一个副本函数,并且绑定新函数的this指向bind返回的新的函数
```

### JS9 等于的区别

```js
答：== 表示是相等，只比较内容
   === 表示是全等，不仅比较内容，也比较类型
```

### JS10 es6-es10新增常用方法

```js
答: 
es6:
1、let、const
2、解构赋值  let { a, b } = { a: 1, b: 2 }
3、箭头函数
4、字符串模板
5、扩展运算符
6、数组方法：map、filter等等
7、类：class关键字
8、promise
9、函数参数默认值 fn(a = 1) {}
10、对象属性简写 let a = 1; let obj = {a}
11、模块化：import--引入、exprot default--导出

es7:
1、includes()方法，用来判断一个数组是否包含一个指定的值，根据情况，如果包含则返回true，否则返回false。

es8:
1、async/await

es9：
1、Promise.finally() 允许你指定最终的逻辑

es10:
1、数组Array的flat()和flatmap()
   flat:方法最基本的作用就是数组降维
      var arr1 = [1, 2, [3, 4]];
            arr1.flat(); 
            // [1, 2, 3, 4]

        var arr3 = [1, 2, [3, 4, [5, 6]]];
        arr3.flat(2); //提取深度为2
        // [1, 2, 3, 4, 5, 6]

        //使用 Infinity 作为深度，展开任意深度的嵌套数组
        arr3.flat(Infinity); 
        // [1, 2, 3, 4, 5, 6]
   flatmap:方法首先使用映射函数映射(遍历)每个元素，然后将结果压缩成一个新数组
```

### JS11 怎么理解函数的防抖和节流

```js
答:
1、定义：
防抖: 就是指触发事件后在n秒内函数只能执行一次，如果在n秒内又触发了事件，则会重新计算函数执行时间。
     例如：设定1000毫秒执行，当你触发事件了，他会1000毫秒后执行，但是在还剩500毫秒的时候你又触发了事件，那就会重新开始1000毫秒之后再执行
	 经典应用场景 ： 输入框输入事件
	 
节流: 就是指连续触发事件但是在设定的一段时间内中只执行一次函数。
     例如：设定1000毫秒执行，那你在1000毫秒触发在多次，也只在1000毫秒后执行一次
      防止用户短时间内重复点击按钮提交（获取短信验证码）
	  
2、防抖和节流的实现：
    <body>
    <input type="text" class="ipt" />
    <script>
      var timerId = null
      document.querySelector('.ipt').onkeyup = function () {
        // 防抖
        if (timerId !== null) {
          clearTimeout(timerId)
        }
        timerId = setTimeout(() => {
          console.log('我是防抖')
        }, 1000)
      }

      document.querySelector('.ipt').onkeyup = function () {
        // 节流
        console.log(2)
        if (timerId !== null) {
          return
        }

        timerId = setTimeout(() => {
          console.log('我是节流')
          timerId = null
        }, 1000)
      }

    </script>
  </body>
```

### JS12 什么是事件流

```js
答: 事件流是指事件传播的顺序,由事件捕获 => 目标事件 => 事件冒泡
```

### JS13 如何阻止冒泡和默认行为？ 原生事件操作集合

```js
答: 阻止冒泡和捕获  e.stopPropagation()
    阻止默认行为   e.preventDefault()   return false
    注意：addEventListener注册的事件，在高浏览器版本中，return false将没有效果，必须要用事件对象


 节点操作: 对对应的节点实现 增删改查

      查: 通过当前节点找目标节点 => 明确的亲戚关系
        1. 父级: parentNode
        2. 子集: children[]  children 获取的是动态集合，数组会更新，下标错乱
        querySelector 静态集合，数组不会更新
        3. 兄弟: 
            perviousElementSibling 上一个
            nextElementSibling 下一个
   增删元素：
     1. 创建元素 => document.createElement('标签')
      返回值: 这个标签对应的DOM对象 都是在内存里面的
      
      btn.onclick = function() {
        let li = '<li></li>'
        ul.innerHTML = li
      }  考虑内容的安全性 批量会有性能问题  引发浏览器重排和重绘
    2. 添加元素
      parent.appendChild(需要添加的元素) => 把对应的元素添加到parent内容的最后面
      parent.insertBefore(需要添加的元素, 参照物节点) => 当对应的元素添加到参照物的前面去
      大多数情况下: 参照物节点就是 => parent.children[0];
      注意点:
        1. 追加的节点有新节点和页面上已经存在的节点两种情况
        2. 如果insertBefore里面的参照物找不到的情况下, 类似于appendChild的操作
    3. 删除元素
      parent.removeChild(需要删除的节点)
      删所有（可给空）: parent.innerHTML = '';
    4. 克隆节点
      模板节点.cloneNode(布尔值)
      返回值: 克隆出来的新节点
      使用场景: 如果对应的节点模块是比较复杂的html结构的时候,就可以事先准备好一个HTML结构,直接通过cloneNode得到一个新的模板

        

```

```javascript
    常用事件：
      点击事件: 
         click: 单击
         dblclick： 双击
       // 针对表单
         onfocus：获得焦点
         onblur：失去焦点
         onsubmit： 表单提交
         onchange：内容发生改变(失去焦点时)
         oninput: 当value值被修改的时候触发 
         
      键盘事件:
        keydown: 键盘按下 (如果获取了表单的内容获取的上一次的表单的结果)
        keyup: 键盘抬起 (获取的表单内容是当前这一次的表单内容)
        keypress: 键盘按下时触发   
    
      鼠标事件:
      mouseenter: 鼠标进入
      mousemove: 鼠标移动
      mouseleave: 鼠标离开
      ——————————————————————————————————————————————————————————————————————————————————————————————
      事件对象中的常用属性
      事件对象的获取: 直接在事件处理函数中接受一个形参即可
      鼠标落点:
          e.pageX, e.pageY => 以整个页面为参照物
          e.clientX, e.clientY => 以整个可视区域为参照物
          e.screenX, e.screenY => 以整个屏幕区域为参照物
      键盘事件的事件对象:
        e.keyCode => 键盘的键盘码
```

```javascript
    操作元素的样式
    元素style.left 
    操作类名
    classList.add('active')
    classList.remove('active')
```

![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/f9b680d00115cc27a2ddf677f9f6567e.png#pic_center)
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/e6332c8f5940f22366b496c29be852a4.png#pic_center)



### JS14 原生注册事件的方式有哪些？区别是什么

```js
答: 注册方式
事件三要素：事件源 事件名  事件处理函数 
		  1. on + 事件名称 click   
		  2. addEventListener
		区别: 
			1. 使用on注册事件,同一个元素只能注册一个同类型事件,否则会覆盖。
			2. addEventListener可以注册同一事件多次,不会被覆盖。
              元素.on+'事件名'=null 移除事件
              元素.removeEventListener(''事件名',事件处理函数，false)  移除事件
```

### JS15 get 和post的区别

```js
答: get
			1. 在url后面拼接参数,只能以文本的形式传递数据
			2. 传递的数据量小,4KB左右
			3. 安全性低, 会将数据显示在地址栏
			4. 速度快,通常用于安全性要求不高的请求
			5. 会缓存数据
			6. get没有请求头和请求体
	post
		    1. 安全性比较高
			2. 传递数据量大,请求对数据长度没有要求
			3. 请求不会被缓存,也不会保留在浏览器历史记录里
```

### JS16 null和undefined的区别

```js
答：null 表示空值 没有获取到。typeof null 返回"object"
   undefined 表示未定义，声明没有值。typeof undefined 返回"undefined"
```

### JS17 Json字符串和json对象怎么相互转换

```js
答: JSON对象转JSON字符串: JSON.stringify(对象)
    JSON字符串转JSON对象: JSON.parse(字符串)
```

### JS18 怎么理解同步和异步

```js
	1、javascript是单线程。单线程就意味着，所有任务需要排队，前一个任务结束，才会执行后一个任务。如果前一个任务耗时很长，后一个任务就不得不一直等着。于是就有一个概念——任务队列。
	2、同步任务，顾名思义，就是立即执行的任务，同步任务一般会直接进入到主线程中执行；而异步任务，就是异步执行的任务，比如ajax网络请求，setTimeout 定时函数等都属于异步任务，异步任务会通过任务队列( Event Queue )的机制来进行协调。
```

### JS19 js的运行机制是什么

```js
答：js是单线程执行的，页面加载时，会自上而下执行主线程上的同步任务，当主线程代码执行完毕时，才开始执行在任务队列中的异步任务。具体如下  
    1.所有同步任务都在主线程上执行，形成一个执行栈。
    2.主线程之外，还存在一个"任务队列(eventloop队列或者消息队列)"。只要异步任务有了运行结果，就在"任务队列"之中放置一个事件。
    3.一旦"执行栈"中的所有同步任务执行完毕，系统就会读取"任务队列"，看看里面有哪些事件。哪些对应的异步任务，于是结束等待状态，进入执行栈，开始执行。
    4.主线程不断重复上面的第三步。
   
   自己理解：
        1. JS是单线程的,也就是说同一时间只能做一件事情,这个是JS本身的特性决定的.
        2. Js的有些任务是需要耗费时间的或者等待的,所以纯粹的单线程会等待导致阻塞代码,用户体验很差
        3. JS会将耗费时间或者等待的操作(异步任务)交给浏览器(浏览器是多线程的),浏览器负责调度
        4. 等JS的同步任务执行完毕之后,再去执行异步任务
```

### JS20 怎么理解面向对象

```js
答：1、面向对象是一种软件开发的思想和面向过程是相对应的，就是把程序看作一个对象，将属性和方法封装其中，以提高代码的灵活性、复用性、可扩展性。
  2、面向对象有三大特性：封装、继承、多态。
       封装：把相关的信息（无论数据或方法）存储在对象中的能力
       继承：由另一个类（或多个类）得来类的属性和方法的能力
       多态：编写能以多种方法运行的函数或方法的能力
   3、js中对象是一个无序的数据集合或者也可以说是属性和方法的集合，可以动态的添加属性可方法。
   4、js是基于对象，但是也使用了嵌入了面向对象的思想，可以实现继承和封装，这样也可以提供代码的灵活性和复用性。
```

### JS21 原生ajax

```js
答：1.创建异步对象 var xhr = new HTMLHttpRequest()
    2.设置请求行  xhr.open()
    3.设置请求头  xhr.setRequestHeader()   get请求没有请求头
    4.设置请求体  xhr.send      get请求没有请求体,参数为null
    5.监视异步对象的状态变化   xhr.onreadystatechange(){}
```

### ajax axios fetch区别

```js
ajax
    1.创建异步对象 var xhr = new HTMLHttpRequest()
    2.设置请求行  xhr.open()
    3.设置请求头  xhr.setRequestHeader()   get请求没有请求头
    4.设置请求体  xhr.send      get请求没有请求体,参数为null
    5.监视异步对象的状态变化   xhr.onreadystatechange(){}
一、Ajax
Ajax（Asynchronous JavaScript and XML）是一种在无需重新加载整个页面的情况下，能够更新部分网页的技术。它基于XMLHttpRequest对象实现，可以在不中断用户与页面的交互的情况下，向后端发送请求并获取数据。Ajax的优点包括：
异步性：Ajax可以在不阻塞页面的情况下发送请求，提高了用户体验。
可跨域：Ajax请求可以跨越不同的域名，方便前后端分离开发。
灵活性高：可以自定义请求头、请求体、响应格式等。
然而，Ajax也存在一些缺点：
编程复杂：需要手动处理请求和响应，编写回调函数等，代码量较大。
兼容性差：在老版本的浏览器中，可能存在兼容性问题。

二、Fetch
Fetch是ES6中引入的一个新的网络请求API，它返回一个Promise对象，使得异步操作更加方便。Fetch的优点包括：
基于Promise：Fetch使用Promise对象处理异步操作，代码更加简洁易懂。
自带超时处理：Fetch可以在请求超时后自动中断请求，避免了长时间等待。
跨域方便：Fetch请求可以自动处理CORS（跨源资源共享）问题，降低了跨域设置的难度。
然而，Fetch也存在一些缺点：
无法取消请求：一旦发送请求，无法中途取消。
请求数据默认不会作为JSON解析：需要手动处理响应数据的解析。

三、Axios
Axios是一个基于Promise的HTTP客户端，它提供了许多实用的功能，如拦截请求和响应、转换请求和响应数据、自动转换JSON数据等。Axios的优点包括：
功能丰富：Axios提供了许多实用的功能，方便开发者处理各种复杂的请求场景。
浏览器和node.js兼容性好：Axios可以在浏览器和node.js环境中运行，兼容性较好。
支持取消请求：Axios提供了取消请求的功能，方便开发者在需要时中断请求。
然而，Axios也存在一些缺点：
体积较大：由于功能丰富，Axios的体积相对较大，可能会影响页面加载速度。
依赖Promise：Axios基于Promise实现，对于不熟悉Promise的开发者来说，可能会有一定的学习成本。
综上所述，Ajax、Fetch和Axios各有优缺点，开发者可以根据实际需求和场景选择合适的技术。对于简单的数据获取需求，可以使用Fetch；对于需要处理复杂请求和响应的场景，可以使用Axios；对于老版本的浏览器兼容性需求，可以考虑使用Ajax。
```





### JS22 伪数组和真数组的区别

```js
伪数组：
1、拥有length属性
2、不具有数组的方法
3、伪数组是一个Object，真数组是Array
4、伪数组的长度不可变，真数组的长度是可变的
```

### JS23 那些情况会得到伪数组

```js
1、参数 arguments，
2、DOM 对象列表（比如通过 document.getElementsByTags 得到的列表）、childNodes也是伪数组
3、jQuery 对象（比如 $("div")）
```

### JS23  伪数组怎么转换为真数组

```js
1、let newArr = Array.prototype.slice.call(伪数组)
2、let newArr = Array.from(伪数组),ES6的新语法
3、let newArr = [...伪数组]，使用扩展运算符,也是ES6的语法
```

### JS23 let、const、var的区别

```js
1、var声明变量存在提升（提升当前作用域最顶端），let和const是不存在变量提升的情况,需要先声明再使用
2、var没有块级作用，let和const存在块级作用域 {}
3、var允许重复声明，let和const在同一作用域不允许重复声明
4、var和let声明变量可以修改，const是常量不能改变
const 定义对象能改变，引用类型（地址） 值类型不能改变
5.全局的let不会挂载到window;
全局的var会挂载到window,造成window属性污染
```

### JS24 异步函数有哪些

```js
JavaScript 中常见的异步函数有：定时器，事件和 ajax 等
```

### JS25 什么是promise，特点是什么

```js
	首先，它是一个对象，也就是说与其他JavaScript对象的用法，没有什么两样；它使得异步操作具备同步操作的效果，使得程序具备正常的同步运行的流程，回调函数不必再一层层嵌套。
	简单说，它的思想是，每一个异步任务立刻返回一个Promise对象，由于是立刻返回，所以可以采用同步操作的流程。这个Promises对象有一个then方法，允许指定回调函数，在异步任务完成后调用。
    
 特点：
    1、Promise对象只有三种状态。
        异步操作“未完成”（pending）
        异步操作“已完成”（resolved，又称fulfilled）
        异步操作“失败”（rejected）
        异步操作成功，Promise对象传回一个值，状态变为resolved。
        异步操作失败，Promise对象抛出一个错误，状态变为rejected。
    2、promise的回调是同步的，then是异步的
    3、可以链式调用
```

### JS26 promise的方法有哪些，能说明其作用

```js
原型上的方法：
1、Promise.prototype.then()
	1）作用是为 Promise 实例添加状态改变时的回调函数。接受两个回调函数作为参数。第一个回调函数是Promise对象的状态变为resolved时调用，第二个回调函数是Promise对象的状态变为rejected时调用。其中，第二个函数是可选的，不一定要提供。
    2）返回的是另一个Promise对象，后面还可以接着调用then方法。
2、Promise.prototype.catch()
	1）用于指定发生错误时的回调函数。
    2）返回的也是一个 Promise 对象，因此还可以接着调用then方法
3、Promise.prototype.finally()
	1）finally方法用于指定不管 Promise 对象最后状态如何，都会执行的回调函数。
    2）finally方法的回调函数不接受任何参数，这意味着没有办法知道，前面的 Promise 状态到底是fulfilled还是rejected。

自身API:
1、Promise.resolve()
	1）不带参数传递 — 返回一个新的状态为resolve的promise对象
    2）参数是一个 Promise 实例— 返回 当前的promise实例
2、Promise.reject()
	1)返回的是一个值
    2）返回的值会传递到下一个then的resolve方法参数中
3、Promise.all() 
	1）并行执行异步操作的能力
    2）所有异步操作执行完后才执行回调
4、Promise.race()
	1）那个结果返回来的快就是，那个结果，不管结果是成功还是失败
```



### JS27 async和await是干什么的

```js
1、async 用于申明一个 function 是异步的，而 await 用于等待一个异步方法执行完成。
2、await 只能出现在 async 函数中。
3、async 函数返回的是一个 Promise 对象，后面可以用then方法。
```

### JS28 async和await 原理是什么

```js
async函数就是generator函数的语法糖。
async函数，就是将generator函数的*换成async，将yield替换成await。
async函数对generator改进了

```

### JS28  数组如何进行降维（扁平化）

```js
1、利用Array.some方法判断数组中是否还存在数组，es6展开运算符连接数组
       let arr = [1,2,[3,4]]
        while (arr.some(item => Array.isArray(item))) {
            arr = [].concat(...arr);
        }
2、使用数组的concat方法
　   let arr = [1,2,[3,4]]
     let result = []
     result = Array.prototype.concat.apply([], arr)

3、 使用数组的concat方法和扩展运算符
    var arr = [1,2,[3,4]]
    var result = []
    result = [].concat(...arr)
        
4、es6中的flat函数也可以实现数组的扁平化
    let arr = [1,2,['a','b',['中','文',[1,2,3,[11,21,31]]]],3];
    let result = arr.flat( Infinity )
    注意：flat方法的infinity属性，可以实现多层数组的降维
```

### JS29 怎么理解事件循环机制

```js
	1、JavaScript 是一门单线程语言.单线程可能会出现阻塞的情况，所js分了同步任务和异步任务。
    2、同步和异步任务分别进入不同的执行环境，同步的进入主线程，即主执行栈，异步的进入 Event Queue（事件队列） 。主线程内的任务执行完毕为空，会去 Event Queue 读取对应的任务，推入主线程执行。 上述过程的不断重复就是我们说的 Event Loop (事件循环)。
```

### JS30 什么是作用域链

```js
	1、作用域：分全局作用域和局部作用域
    2、在访问一个变量时，首先在当前作用域中找，如果找不到再到外层作用域中找，这样一层一层的查找，就形成了作用域链。
    3、如果没有找到会返回undefined
```

### JS31 for in 和 for of 的区别

```js
1、for…in是遍历数组、对象的key
2、for…of是遍历数组的value
例如：
let arr = ["a","b"];
1）for (let key in arr) {
console.log(key);  //0 1
}
2）for (let value of arr) {
console.log(value);  //a b
}
```

### JS32 数组去重的方式

```js
1、第一种方式：利用indexof方法
  let arr = [2, 8, 5, 0, 5, 2, 6, 7, 2]
  let newArr = []
  for (let i = 0; i < arr.length; i++) {
     if (newArr.indexOf(arr[i]) === -1) {
       newArr.push(arr[i])
     }
  }

2、第二种方式：sort()方法
   let arr = [2, 8, 5, 0, 5, 2, 6, 7, 2]
   arr.sort()
   let newArr = [arr[0]]
   for (let i = 1; i < arr.length; i++) {
     if (arr[i] !== newArr[newArr.length - 1]) {
       newArr.push(arr[i])
     }
   }
3、第三种方式：两层for循环
    let arr = [2, 8, 5, 0, 5, 2, 6, 7, 2, 8]
    let newArr = []
    for (let i = 0; i < arr.length; i++) {
      for (let j = i + 1; j < arr.length; j++) {
        if (arr[i] === arr[j]) {
          i++
          j = i
        }
      }
     newArr.push(arr[i])
  }
4、第四种方式：利用ES6 Set去重
 let arr = [2, 8, 5, 0, 5, 2, 6, 7, 2, 8]
 let newArr = Array.from(new Set(arr))
```

### JS33 数字处理，三位隔开

```javascript
如何格式化数字，使整数部分每三位加一个逗号，这时不妨：（不推荐）

const num = 2333333;
num.toLocaleString();   // 2,333,333

const num = 103293456.90
num.toLocaleString();  // 103,293,456.9

let string = "12345678123456789";
const reg = /(?!\b)(?=(\d{3})+\b)/g;

let result = string.replace(reg, ',')
console.log(result); 
// => "12,345,678,123,456,789"


```

### JS34 解释下什么是变量声明提升

```javascript
 解释下什么是变量声明提升？
变量提升（hoisting），是负责解析执⾏代码的 JavaScript 引擎的⼯作⽅式产⽣的⼀个特性。
JS引擎在运⾏⼀份代码的时候，会按照下⾯的步骤进⾏⼯作：
1. ⾸先，对代码进⾏预解析，并获取声明的所有变量
2. 然后，将这些变量的声明语句统⼀放到代码的最前⾯
3. 最后，开始⼀⾏⼀⾏运⾏代码
我们通过⼀段代码来解释这个运⾏过程：
上⾯这段代码的实际执⾏顺序为:
1. JS引擎将 var a = 1 分解为两个部分：变量声明语句 var a = undefined 和变量赋值语句
a = 1
2. JS引擎将 var a = undefined 放到代码的最前⾯，⽽ a = 1 保留在原地
也就是说经过了转换，代码就变成了:
console.log(a)
var a = 1
function b() {
 console.log(a) }
 b() // 1
变量的这⼀转换过程，就被称为变量的声明提升。
⽽这是不规范, 不合理的, 我们⽤的 let 就没有这个变量提升的问题
```

### JS35 JS 的参数是以什么⽅式进⾏传递的？

```javascript
基本数据类型和复杂数据类型的数据在传递时，会有不同的表现。
基本类型：是值传递！
基本类型的传递⽅式⽐较简单，是按照 值传递 进⾏的。
复杂类型: 传递的是地址! (变量中存的就是地址)
var a = undefined
console.log(a) // undefined
a = 1
function b() {
 console.log(a) }b() // 1
let a = 1
function test(x) {
 x = 10 // 并不会改变实参的值
 console.log(x) }
test(a) // 10
console.log(a) // 1
```

### JS36 宏任务微任务

```javascript
JavaScript 把异步任务又做了进一步的划分，异步任务又分为两类，分别是：

① 宏任务：
整个script标签
异步 Ajax 请求、
setTimeout、setInterval、
文件操作
其它宏任务

② 微任务：
Promise.then、.catch 和 .finally
process.nextTick
await
其它微任务


```

![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/3a1dc4af353fbf903ff1bdb4b8496479.webp?x-image-process=image/format,png#pic_center)
![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/b762de66ff9797f701fd56130dd0a796.webp?x-image-process=image/format,png#pic_center)
每一个宏任务执行完之后，都会检查是否存在待执行的微任务。
如果有，则执行完所有微任务之后，再继续执行下一个宏任务。
async内部遇到await的时候，只有当await右边跟随的代码执行完毕的时候，才会执行后面的代码，
此时后面的代码也可以算作内部的微任务
当我们需要不阻塞主线程异步执行，但又要有顺序的执行相关代码的时候，await/async就可以排上用场，就理解为 await修饰那句话当作同步任务
宏任务最后执行
promise内部遇到resolve（）和reject（）调用的时候，会继续执行后面的代码，Promise 是用来管理异步编程的，它本身不是异步的** **，promise是同步代码**promise里面是同步，promise.then()是微任务，setTimeout是宏任务。

面试题：

```javascript
																																							console.log(1)

setTimeout(function() {
  console.log(2)
}, 0)

const p = new Promise((resolve, reject) => {
  resolve(1000)
})
p.then(data => {
  console.log(data)
})

console.log(3)    //1 3 1000  undefined 2


```

```javascript
console.log(1)
setTimeout(function() {
  console.log(2)
  new Promise(function(resolve) {
    console.log(3)
    resolve()
  }).then(function() {
    console.log(4)
  })
})

new Promise(function(resolve) {
  console.log(5)
  resolve()
}).then(function() {
  console.log(6)
})
setTimeout(function() {
  console.log(7)
  new Promise(function(resolve) {
    console.log(8)
    resolve()
  }).then(function() {
    console.log(9)
  })
})
console.log(10)  
```

```javascript
console.log(1)

  setTimeout(function() {
    console.log(2)
  }, 0)

  const p = new Promise((resolve, reject) => {
    console.log(3)
    resolve(1000) // 标记为成功
    console.log(4)
  })

  p.then(data => {
    console.log(data)
  })

  console.log(5)
```

```javascript
  new Promise((resolve, reject) => {
    resolve(1)

    new Promise((resolve, reject) => {
      resolve(2)
    }).then(data => {
      console.log(data)
    })

  }).then(data => {
    console.log(data)
  })

  console.log(3)
```

```javascript
setTimeout(() => {
  console.log(1)
}, 0)
new Promise((resolve, reject) => {
  console.log(2)
  resolve('p1')

  new Promise((resolve, reject) => {
    console.log(3)
    setTimeout(() => {
      resolve('setTimeout2')
      console.log(4)
    }, 0)
    resolve('p2')
  }).then(data => {
    console.log(data)
  })

  setTimeout(() => {
    resolve('setTimeout1')
    console.log(5)
  }, 0)
}).then(data => {
  console.log(data)
})
console.log(6)



async function async1() {
    console.log('async1 start');
    await async2();
    console.log('async1 end');
}
async function async2() {
    console.log('async2');
}
console.log('script start');
setTimeout(function() {
    console.log('setTimeout');
}, 0)
async1();
new Promise(function(resolve) {
    console.log('promise1');
    resolve();
}).then(function() {
    console.log('promise2');
});
console.log('script end');  //script start async1 start async2 promise1 script end  async1 end  promise2  setTimeout
```

### JS37 箭头函数

```javascript
         1.箭头函数没有自己的this,获取外部作用域的this
         2.箭头函数,不能作为构造函数(会报错),不能配合new一起使用,没有this
         3.箭头函数中,没有arguments(形参列表,是个伪数组)(会报错),它有...rest剩余形参

        //简化
        //1.如果形参只写1个,可以省略小括号(0,2,2以上都不能省)
        //2.如果函数体只有一句话,花括号可以省
        //当函数体省略时,会自动将后面的式子return出去
```

### JS38 this指向理解

```javascript
       // 总结:
        (非箭头函数)函数的this指向-> 其实函数内部的this指向是 函数在 调用位置的作用域中的this指向
        // => 需要会找到函数在哪里调用 debugger CallStack 第二个位置
        // ps: 函数调用位置不确定->fn()
        //   fn()
        //   obj.fn()
        //   setTimeout(() => {
        //     fn()
        //   });
        // 1. 默认window
        // 2. 隐式 对象
        // 3. 显示cba
        // 4. new绑定

        箭头函数的this指向-> 是 函数在 声明的位置的作用域中的this指向
        // => 需要找到声明的位置在哪里
        //没有自己的this,在肩头函数中访问this,会访问到外部作用域的this
        //事件函数中,要用到this,就不要写成箭头函数
        //不想要自己的this可以改成箭头函数写法
        // let btn = doucument.querySelector('#btn')
        // btn.onclick = function() {
        //         console.log(this)  //btn
        //             //实际工作中,setTimeout和setInterval 中的this,默认指向window(没有意义的)
        //             //这个指向window的this,我们是不需要的
        //         setTimeout(() => {
        //             console.log(this)//btn
        //             this.style.backgroundColor = 'pink'
        //         }, 1000)
        //     }

        // btn.onclick = function() {
        //         let that = this
        //         setTimeout(() => {
        //             that.style.backgroundColor = 'pink'
        //         }, 1000)
        //     }
        //常见情况分析理解:
        //单独的定时器 延迟器 箭头函数写法里面的this指向是默认绑定,指向window,
        //定时器 延时器 在其他函数里面箭头函数写 this指向父级函数的this指向
        //事件处理函数, this指向调用者,隐式绑定,指向事件源
        //注册事件委托,里面this指向.del
        // $('#btn').on('click', '.del', () => {

        //     })

        //箭头函数没有自己的this,找外部作用域on函数的this,这里是on帮我们处理的this指向
        // ps: 函数调用位置不确定->fn()

        面试 QA
        1. 非箭头 调用位置 (不一定在哪里, 所以变来变去)
        2. 箭头 声明的位置
```

### JS39 new修饰符

```javascript
  //new做了四件事
        //1.创建了一个新对象
        //2.让构造函数里面的this指向这个新对象
        //3.执行构造函数,可以给构造函数创建的实例新建方法和属性
        //4.将对象返回
        // function Vue(el, data) {
        //     console.log('-----')
        //         // console.log(this)
        //     this.el = el
        //     this.data = data
        // }
        // const vue = new Vue()
        // new加函数名就可以直接调用
        //new可以执行函数,()可以省,这里面是为了传实参
```

### JS40 递归函数

```javascript
//递归函数:
        //在函数内部,自己掉自己,就是递归
        //1.必须在内部,自己掉自己
        //2.必须要有出口,必须要有结束条件,否则会死递归
```

### JS41 数组方法（基本操作）

```javascript
数组： 
长度：arr.length
下标范围 0-arr.length-1
查： arr[index] 若无此项为undefined
改： arr[index] = 新值
增： arr[arr.length] = 新值 

增： 尾部增  push(要追加的内容，一个或多个)      返回值：新的数组长度 
    头部增  unshift(要追加的内容，一个或多个)   返回值：新的数组长度
    
删： 尾部删  pop（）       无参                 返回值：被删除的元素
    尾部增  shift()       无参                 返回值：被删除的元素
 //把数组的最后一个元素变成数组的第一个元素
      // arr.unshift(arr.pop())；
 //把数组的第一个元素变成数组的最后一个元素
      //arr.push(arr.shift());

实现数组任意位置的增删改截取： arr.splice(起始的下标，删除的个数，替换的内容)   返回值：由被删除的元素组成的数组
                      注： 增，第二项参数写0，替换内容不改时可以不传。 for循环里不能使用，因为改变了原数组，改变了下标
数组提取：                 arr.slice()                         返回值：新数组
                       不传参数，复制一个新数组
                       传一个参数（起始的下标）=》 从这个下标一直提取到结束 
                       传两个参数（起始下标，结束下标）    =》  从起始下标一直提取到结束下标
                       倒数第四位开始一直到最后一位（包含最后一位）  slice将字符串长度与对应的负参数相加结果入参
数组排序，翻转，拼接
排序 arr.sort() 数默认排序为从小到大  不传参，默认使用字符串方式排序  传一个函数 return a-b 小到大   返回：翻转后的数组
翻转 arr.reverse()                    返回:颠倒的原数组
拼接 arr.concat(数组1，...)            返回值： 拼接好的新数组  

数组拼接成字符串 join('分隔符')
查找数组中元素
indexOf(查找的内容，起始下标（默认为0）)
从左往右   
用来查找数组中某个元素出现的位置，找到返回该元素对应的下标，找不到返回-1
lastIndexOf(查找的内容，从哪个下标开始)  找到返回该元素对应的下标，找不到返回-1
从右往左（从后面开始）
arr.includes（查找的那项） 包含 true false


改变原数组： push（）unshift（）pop（）shift() sort（） reverse() splice()
不会改变原数组： concat（） join（）slice（）

```

### JS41 数组方法（高阶）

```javascript
 数组的方法 es5/es6
       forEach 遍历 无返回值
       map 遍历,给数组的每个元素做特殊的处理  收集返回的值到一个**新数组**中
       filter 过滤, 保留需要的项(return true的项), 存到一个**新数组**中
       reduce 求和
       some 遍历,  用于数组判断  当数组中只要有一个符合条件就返回 **true** 
       every 遍历, 必须每一个都满足条件, 结果才是**true**
       Array.from(伪数组) 将伪数组转换成真数组

       find 找, 找第一个满足条件的项, 如果没找到 undefined
       findIndex 找, 找第一个满足条件的项的下标, 如果没找到 -1
       includes()方法返回一个布尔值


```

### JS42 reduce

```javascript
数组中的 reduce 犹如一只魔法棒，通过它可以做一些黑科技一样的事情。语法如下：
reduce(callback(accumulator, currentValue[, index, array])[,initialValue])
reduce 接受两个参数，回调函数和初识值，初始值是可选的。回调函数接受4个参数：积累值、当前值、当前下标、当前数组。
如果 reduce的参数只有一个，那么积累值一开始是数组中第一个值，如果reduce的参数有两个，那么积累值一开始是出入的 initialValue 初始值。然后在每一次迭代时，返回的值作为下一次迭代的 accumulator 积累值。
今天的这些例子的大多数可能不是问题的理想解决方案，主要的目的是想说介绍如何使用reduce来解决问题。
求和和乘法

// 求和
[3, 5, 4, 3, 6, 2, 3, 4].reduce((a, i) => a + i);
// 30

// 有初始化值
[3, 5, 4, 3, 6, 2, 3, 4].reduce((a, i) => a + i, 5 );
// 35

// 如果看不懂第一个的代码，那么下面的代码与它等价
[3, 5, 4, 3, 6, 2, 3, 4].reduce(function(a, i){return (a + i)}, 0 );

// 乘法
[3, 5, 4, 3, 6, 2, 3, 4].reduce((a, i) => a * i);
查找数组中的最大值

如果要使用 reduce 查找数组中的最大值，可以这么做：
[3, 5, 4, 3, 6, 2, 3, 4].reduce((a, i) => Math.max(a, i), -Infinity);
上面，在每一次迭代中，我们返回累加器和当前项之间的最大值，最后我们得到整个数组的最大值。
如果你真想在数组中找到最大值，不要有上面这个，用下面这个更简洁：
Math.max(...[3, 5, 4, 3, 6, 2, 3, 4]);
连接不均匀数组

let data = [
  ["The","red", "horse"],
  ["Plane","over","the","ocean"],
  ["Chocolate","ice","cream","is","awesome"], 
  ["this","is","a","long","sentence"]
]
let dataConcat = data.map(item=>item.reduce((a,i)=>`${a} ${i}`))

// 结果
['The red horse', 
'Plane over the ocean', 
'Chocolate ice cream is awesome', 
'this is a long sentence']
在这里我们使用 map 来遍历数组中的每一项，我们对所有的数组进行还原，并将数组还原成一个字符串。
移除数组中的重复项

let dupes = [1,2,3,'a','a','f',3,4,2,'d','d']
let withOutDupes = dupes.reduce((noDupes, curVal) => {
  if (noDupes.indexOf(curVal) === -1) { noDupes.push(curVal) }
  return noDupes
}, [])
检查当前值是否在累加器数组上存在，如果没有则返回-1，然后添加它。
当然可以用 Set  的方式来快速删除重复值，有兴趣的可以自己去谷歌一下。
验证括号

[..."(())()(()())"].reduce((a,i)=> i==='('?a+1:a-1,0);
// 0

[..."((())()(()())"].reduce((a,i)=> i==='('?a+1:a-1,0);
// 1

[..."(())()(()()))"].reduce((a,i)=> i==='('?a+1:a-1,0);
// -1
这是一个很酷的项目，之前在力扣中有刷到。
按属性分组

let obj = [
  {name: 'Alice', job: 'Data Analyst', country: 'AU'},
  {name: 'Bob', job: 'Pilot', country: 'US'},
  {name: 'Lewis', job: 'Pilot', country: 'US'},
  {name: 'Karen', job: 'Software Eng', country: 'CA'},
  {name: 'Jona', job: 'Painter', country: 'CA'},
  {name: 'Jeremy', job: 'Artist', country: 'SP'},
]
let ppl = obj.reduce((group, curP) => {
  let newkey = curP['country']
  if(!group[newkey]){
    group[newkey]=[]
  }
  group[newkey].push(curP)
  return group
}, [])
这里，我们根据 country 对第一个对象数组进行分组，在每次迭代中，我们检查键是否存在，如果不存在，我们创建一个数组，然后将当前的对象添加到该数组中，并返回组数组。
你可以用它做一个函数，用一个指定的键来分组对象。
扁平数组

let flattened = [[3, 4, 5], [2, 5, 3], [4, 5, 6]].reduce(
  (singleArr, nextArray) => singleArr.concat(nextArray), [])

// 结果：[3, 4, 5, 2, 5, 3, 4, 5, 6]
这只是一层，如果有多层，可以用递归函数来解决，但我不太喜欢在 JS 上做递归的东西😂。
一个预定的方法是使用.flat方法，它将做同样的事情
[ [3, 4, 5],
  [2, 5, 3],
  [4, 5, 6]
].flat();
只有幂的正数

[-3, 4, 7, 2, 4].reduce((acc, cur) => {
  if (cur> 0) {
    let R = cur**2;
    acc.push(R);
  }
  return acc;
}, []);

// 结果
[16, 49, 4, 144]
反转字符串

const reverseStr = str=>[...str].reduce((a,v)=>v+a)
这个方法适用于任何对象，不仅适用于字符串。调用reverseStr("Hola")，输出的结果是aloH。
二进制转十进制

const bin2dec = str=>[...String(str)].reduce((acc,cur)=>+cur+acc*2,0)

// 等价于

const bin2dec = (str) => {
  return [...String(str)].reduce((acc,cur)=>{
    return +cur+acc*2
  },0)
}
为了说明这一点，让我们看一个例子:(10111)->1+(1+(1+(0+(1+0*2)*2)*2)*2)*2。
```

### JS42 字符串操作方法

```javascript
长度 str.length
indexOf() lastIndexOf() 从前往后/从后往前找第一次出现的位置，如果没有返回-1
trim()  去字符串左右空格 str=str.trim()
toUpperCase() 转换大写
toLowerCase() 转换小写
slice(start，end) 截取 [start,end)

split('切割符') 切割成数组
[].toString() 转化成字符串
arr.toString().replace(/,/g, '')
arr.join('')
+ 拼接
replace（需要替换的值，用来替换的值）

正则全局替换
 let str = "abcoefoxyozzopp"
 str = str.replace(/o/g,'!')
```

### JS43innerHTML innerText

```javascript
获取文本时：
innerText: 只识别文本，不识别标签
innerHTML： 连同内部的标签一起获取到
设置文本时：
都可以设置文本的内容
innerText: 原样输出
innerHTML： 会解析标签
推荐使用 innerText，避免安全隐患，用户输入隐患
```


### JS44 递归斐波那契

```javascript
//题1:利用递归:求1-100的和(化归思想:将复杂问题简单化)
        //求1-n的和
        // getSum(100)=getSum(99)+100
        // getSum(99)=getSum(98)+99
        //....
        //getSum(2)=getSum(1)+2
        //getSum(1)=1结束条件
        // getSum(n) = getSum(n - 1) + n

        // function getSum(n) {
        //     if (n === 1) {
        //         return 1
        //     }

        //     return getSum(n - 1) + n
        // }
        // let result = getSum(100)
        // console.log(result)
        //题2:斐波那契数列,用递归实现.......................................................
        // ：1、1、2、3、5、8、13、21、34......在数学上，斐波纳契数列以如下被以递归的方法定义：
        // F(1)=1，F(2)=1,
        //n>=2
        //F(3)=F(1)+F(2)=F(3-1)+F(3-2)=2
        //F(4)=F(3)+F(2)=F(4-1)+F(4-2)=3

        //  F(n)=F(n-1)+F(n-2)（n>=2，n∈N*）;
        function num(n) {
            if (n <= 2) {
                return 1;
            } else {
                return num(n - 1) + num(n - 2)
            }
        }
        console.log(num(4))
        console.log(num(5))
        console.log(num(9))
        console.log(num(null)) //1
        console.log(num(undefined)) //报错
        console.log(null <= 2) //true



        // 看一下性能怎么样？
        let count = 0 // 计数 ： 统计fib函数递归了多少次
        function fib(n) {
            count++
            if (n === 1 || n === 2) return 1
            return fib(n - 1) + fib(n - 2)
        }
        console.log(fib(40)); // 102334155
        console.log(count); // 204668309


        //性能优化 缓存:存储数据的容器 数组或对象
        let cache = {}
            // 使用递归去计算兔子第10个月的数量
        let count = 0 // 计数 ： 统计fib函数递归了多少次
        function fib(n) {
            count++
            // 求出第n个月的兔子数量
            // 2. 结束
            if (n === 1 || n === 2) return 1
            if (cache[n]) {
                // 说明了： 缓存中有该月份的数量值，直接取出缓存中的数据
                return cache[n]
            } else {
                // 说明缓存中没有该月份的数量
                let ret = fib(n - 1) + fib(n - 2) // 计算的结果
                    // 把结果存储到缓存中
                cache[n] = ret
                    // 把结果给返回出去
                return ret
            }
        }
        console.log(fib(40));
        console.log(count);

        //全局变量污染问题.............................................
        // 使用闭包来保护cache数据的安全
        function outer() {
            // 在这个案例中，如何去使用缓存
            // 缓存里面的数据是计算得出的，我们应该充分信赖缓存里面的数据
            // 缓存里面的数据应该是绝对正确而且是不能被随意修改的
            let cache = {
                // 把月份作为键，把月份对应的数量作为值
                // 1: 1,
                // 2: 1,
                // 3: 2, 
                // 4: 3
            };

            // 使用递归去计算兔子第10个月的数量
            function fib(n) {
                // 求出第n个月的兔子数量
                // 2. 结束
                if (n === 1 || n === 2) return 1
                if (cache[n]) {
                    // 说明了： 缓存中有该月份的数量值，直接取出缓存中的数据
                    return cache[n]
                }
                return cache[n] = fib(n - 1) + fib(n - 2)
            }
            return fib
        }
        let ret = outer()
        console.log(ret(40))
```

### JS45 正则

```javascript
一、创建正则

构造函数创建

const reg = new RegExp(/a/); // 匹配含有字母a


正则字面量

const reg2 = /abc/; // 匹配字母abc
const reg3 = /[abc]/; // 匹配字母a,或者b,或者c

二、正则的组成

正则的组成： 普通字符 + 元字符
普通字符： 大小写字母， 数字
元字符：   在正则里面有特殊含义的

元字符
匹配区间正则表达式含义除了换行的任意的字符.句号,除了句子结束符数字[0-9]\ddigit非数字 除了[0-9]\Dnot digit字符（大小写字母 数字  _）\wword非字符\Wnot word不可见字符（空格 换行 制表符（tab））\sspace可见字符\Snot space但是如果我想要匹配'.'这个符号就要使用 '\' 进行转译
/ 匹配小数点
// 需要对 . 进行转义，  \.
console.log(/\./.test("100.5"));  // true
console.log(/\./.test("1005"));   // false

转译字符还有一个作用，就是这个字符不是特殊字符，使用转译符号后就让他拥有了特殊的含义。比如说元字符，还有一些特殊字符
特殊字符正则表达式含义换行符\nnew line回车符\rreturn空白符\sspace制表符\ttab我们来做一些题目
var reg1 = /abc/
console.log(reg1.test("a")); // false
console.log(reg1.test("aabca")); // true
匹配abc

var reg2 = /\d/
console.log(reg2.test('abc123')) // true
reg2 = /\D/
console.log(reg2.test('abc123')) // true
匹配数字和非数字

var reg3 = /\./
console.log(reg3.test('100.5')) // true
console.log(reg3.test('1005')) // false

如果我要匹配两个怎么办呢？
console.log(/(f|b)oot/.test("f"));      // false
console.log(/(f|b)oot/.test("foot"));   // true
console.log(/(f|b)oot/.test("boot"));   // true
console.log(/(f|b)oot/.test("fboot"));  // true

由题目的最后一题我们引出[]
如果我要匹配a或者b或者c该怎么办？
let reg = /a|b|c/
let reg1 = [abc]

[]的解释说明

[] ===> 在正则里面一个字符的位置，在[]里面可以出现的字符，可以使用“-”表示范围
[^] ===> ^在[]里面，表示非的意思
[^abc] ===> 表示不能是a，或者不能是b，或者不能是c，除了abc都行

// /[abc]/   ==> a 或者 b 或者 c
// /[a-z]/   ==> 是一个字符， 字符可以是 a-z 的其中一个
// /[A-Z]/   ==> 是一个字符， 字符可以是 A-Z 的其中一个
// /[0-9]/   ==> 是一个字符， 字符可以是 0-9 的其中一个
// /[a-zA-Z0-9]/   ==> 是一个字符， 字符可以是 a-z 或者 A-Z 或者  0-9 的其中一个

console.log(/[abc]/.test("a")); // true
console.log(/[abc]/.test("b")); // true
console.log(/[abc]/.test("c")); // true
console.log(/[a-z]/.test("a123")); // true
console.log(/[a-z]/.test("123")); // false
console.log(/[^abc]/.test("abc")); // false
console.log(/[^abc]/.test("ade")); // true,   只要满足了正则的规律，就返回true
console.log(/[^0]/.test("0123")); // true
console.log(/[^0]/.test("0")); // false

三、循环与重复
正则表达式含义解释*出现 0次到多次 {0,}>= 0+出现 1次到多次{1,}>= 1?出现 0次到1次{0,1}0 || 1{m,n}出现 m次到n次{m,}出现 m次以上{m}出现m次{0,m}出现最多m次
我觉得先做一个面试题，根据面试题我们在进行讲解效果会好很多
const target = '111,222,333,aa,  ,!@?'
// 1.1 匹配target中的数字
// 1.2 将特殊符号(除了','号)替换为\*

target.match(/\d+/g)
target.replace(/[^,\w]/g,'*')
// 讲解：
// 1. 字符串的match()方法:
//    会返回数组，数组里面就是字符串中符合正则的每一项, 匹配不到返回null
// 2. 元字符 + 适用于要匹配同个字符出现1次或多次的情况 >=1
      元字符 ? 0 | 1
      元字符 * >= 0
      特定次数:
      {x}: x次
      {min, max}： 介于min次到max次之间
      {min, }: 至少min次
      {0, max}： 至多max次

题目里提到了g这就引出了
四、字符串边界
接下来我们还需要位置边界的匹配。在长文本字符串查找过程中，我们常常需要限制查询的位置。比如我想要全局匹配，我想要不区分大小写
边界和标志正则表达式含义单词边界\bboundary非单词边界\Bnot boundary字符串开头箭头就是开头字符串结尾$做事的结果都会有钱$多行模式mmultiple of lines忽略大小写iignore case, case-insensitive全局模式gglobal

\b和\B

\b是单词边界，具体就是\w和\W之间的位置，也包括\w和^之间的位置，也包括\w和$之间的位置。
const reg1 = "[JS] Lesson_01.mp4".replace(/\b/g, '#');
console.log(reg1); // "[#JS#] #Lesson_01#.#mp4#"
const reg2 = "[JS] Lesson_01.mp4".replace(/\B/g, '#');
console.log(reg2); // "#[J#S]# L#e#s#s#o#n#_#0#1.m#p#4"


^和$

// 把字符串的开头和结尾加上|
const reg1 = "hello".replace(/^|$/g,'|')
console.log(reg1) // "|hello|"

g和m

const result = "I\nlove\njavascript".replace(/^|$/gm, '#');
console.log(result);

 // 给一个连字符串例如：get-element-by-id转化成驼峰形式。
 let str = 'get-element-by-id'
 let reg = /-\w/g
 str.replace(reg,v => v.slice(1).toUpperCase())
 
// 验证座机电话
// 规律：021-29109210 0557-10928380
// 区号：3-4位数字 首位是0 次位不能为0的数字 1-2位数字
// 座机：7-8位数字 首位2-8的数字 6-7位数字

let reg = /^0\[1-9]\d{1,2}-[2-8]\d{6,7}$/
// 验证手机号码
// 规律：13900000000
// 十一位数字 首位1 次位3-9 9位数字

let reg = /^1[3-9]\d{9}$/
// 验证邮箱
// 规律：数字 字母 _ . - @ 数字 字母 _ .字母

let reg = /^[\w\.-]+@\w+(\.[a-z]+)+$/
// 验证姓名
// 规律：汉字 2-6位
let reg = /^[\u4e00-\u9fa5]{2,6}$/

当我以为正则学的差不多的时候，有一个题目难住了我
// 数字的千位分隔符表示法
把"12345678"，变成"12,345,678"


(?=p)和(?!p)

(?=p)，其中p是一个子模式，即p前面的位置
比如(?=l)，表示'l'字符前面的位置，例如：
var result = "hello".replace(/(?=l)/g, '#');
console.log(result); 
// => "he#l#lo"

而(?!p)就是(?=p)的反面意思，比如：
var result = "hello".replace(/(?!l)/g, '#');
console.log(result); 
// => "#h#ell#o#"

经过上面的总结现在给出字符串的千分位分隔符表示法
let string = "12345678123456789";
const reg = /(?!\b)(?=(\d{3})+\b)/g;

let result = string.replace(reg, ',')
console.log(result); 
// => "12,345,678,123,456,789"

另一种数字的千分位分隔符表示法(不推荐)
let num = 10329203.23
console.log(num.toLocaleString())



       
 匹配标签结构： 
  str.replace(/<[^>]+>/g/，'')
```

### JS46 继承原理及最终实现

原理：

```javascript
//代码层面： 继承一些属性和方法
// 继承 可以让多个构造函数之间建立关联，便于管理和复用
（1）原型继承:
利用原型链进行方法继承（进行原型链的修改）
一个实力对象如果访问方法，回往原型上找，原型上找不到就会往原型的原型上找
也就是说在原型链上找
student.prototype = new Person()
student 自己的方法要在下面写，否则在之前原型上，现在访问不到了
（2）组合继承：原型链和借用构造函数call技术组合一块实现
1.使用原型链实现对原型属性和方法的继承（主要是方法）
2.通过借用构造函数来实现对实例属性的继承

function Preson(name,age){
  this.name = name
  this.age = age
}
Person.prototype.sayHi = function() {
  console.log('hi')
}
function Student(code){
  // 借用构造函数，扩展实例属性 调用Person函数，指定this
  Person.call(this,name, age)
  this.code = code
}
// 原型链继承
student.prototype = new Person()
student.prototype.read = function() {
  console.log('小朋友')
}
（3）寄生组合式继承
 Object.create(参数对象)创建新对象
 新对象的_proto_会直接指向传入的参数对象


function Preson(name,age){
  this.name = name
  this.age = age
}
Person.prototype.sayHi = function() {
  console.log('hi')
}
function Student(code){
  // 借用构造函数，扩展实例属性 调用Person函数，指定this
  Person.call(this,name, age)
  this.code = code
}
// 原型链继承
// 不执行函数 
student.prototype = Object.create(Person.prototype)
student.prototype.read = function() {
  console.log('小朋友')
}


```

寄生组合式继承

属性继承原理, 使用 call() 来借调父类的构造函数方法继承原理 

使用 prototype原型, 继承到父类的方法

只要是extends继承的情况，子类构造函数中，必须supe关键字r借调父类构造函数

```javascript
extend关键字继承
// 继承关键字 => extends
class Person {
  constructor (name, age) {
    this.name = name
    this.age = age
  }
  jump () {
    console.log('会跳')
  }
}
class Teacher extends Person {
  constructor (name, age, lesson) {
    super(name, age) // extends 中, 必须调用 super(), 会触发执行父类的构造函数
    super.jump()
    this.lesson = lesson
    console.log('构造函数执行了')
  }
  sayHello () {
    console.log('会打招呼')
  }
}
let teacher1 = new Teacher('zs', 18, '体育')
console.log(teacher1)
```



### JS47 class类

```javascript
1.class本质也是function，class是function的语法糖,将对于构造函数的内容进行封装处理，
2.ES6 中的关键字Class，本质上还是通过原型链和函数做的,创建实例也是用的new,构造函数中this是new绑定
3.类可以不显式定义constructor方法，
  js引擎会默认为类添加一个空的constructor方法：constructor(){}。
  添加到类中的方法会自动添加到原型上，将来所有的实例都能访问到  
4.
  **实例成员：由构造函数创建出来的对象能直接访问的属性和方法，包括：对象本身 以及原型中的所有的属性和方法。**
  实例对象.xxx 实例对象.xxx()
   **静态成员：由构造函数直接访问到的属性和方法。** 构造函数.xxx  构造函数.xxx(ß)
    // 只要被static修饰的属性或者方法, 就是静态成员
    // 使用场景: 如果某个方法, 你觉得不需要实例对象来调用, 
    // 就可以修饰成static, 用类直接调用 (比如: 一些工具方法 => 产生一个随机数)
class Person {}
console.log(typeof Person) // function
静态属性和静态方法，使用static定义的属性和方法只能class自己用，实例用不了


class Person {
  constructor(name) {
    this.name = name
  }

  static age = 22

  static fn() {
    console.log('哈哈')
  }
}
console.log(Person.age) // 22
Person.fn() // 哈哈

const sunshine_lin = new Person('林三心')
console.log(sunshine_lin.age) // undefined
sunshine_lin.fn() // fn is not a function
```

### JS48 类型判断

```javascript
简单数据类型 typeof
null 的判断： 
（1）通过===进行判断值是否是null，===如果类型不同，其结果就是不等。类型相同，结果才相同。
（2）Object.prototype.toString.call(null) //[Object null]
复杂数据类型判断：
instanceof 返回布尔值
// 语法: 实例 instanceof 构造函数(看这个实例是不是由构造函数创建出来的)
//构造函数的原型在不在实例的原型链上

Object.prototype.toString.call(arr) //[Object Array]
```

### JS49 循环语句

```javascript
// 循环语句: 都是根据条件去循环对应的 代码块  可以达到重复去做一件事情
// while循环
// 语法:
// while(条件) {
//   循环体
// }

// 语法:
// do{循环体} while (条件)
// do while循环是在循环之前先执行一次循环体

// for循环: 当如果明确了循环的次数的时候推荐使用for循环
// 因为四要素集成到了for循环的语法里面 (使用的最多)

// while循环: 当不明确循环的次数的时候推荐使用while循环
break 跳出整个循环
continue 跳出当前循环 继续下一次的循环

while(true){
xxx
}
```

### JS50 swiper插件使用

```javascript
1. 查看在线演示 明确自己想要的案例 ( https://www.swiper.com.cn/demo/index.html )
2. 查看swiper的基本使用 ( https://www.swiper.com.cn/usage/index.html )
3. 也可以直接看swiper插件里面的demos,作为参考
4. 配置swiper插件 ( https://www.swiper.com.cn/api/index.html )

基本使用： 中文教程
1.获取方式 （1）下载（js+css） 
（2）安装npm install swiper
2.复制 看官网就行
```


# 

