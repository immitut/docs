### JS之父 Brendan Eich 布兰登 艾克

## 押题类型

### 原型链
	每个且只有函数(匿名函数也是函数，但箭头函数没有)都有 prototype 属性
	函数的 prototype 属性指向了一个对象，这个对象是调用该构造函数创造的实例的原型
	原型则是每一个js对象（null?）在创建的时候所用到的模板，每一个js对象都会从原型那去继承属性

	__proto__
	这是每一个js对象(null ???)都具有的一个属性（？），这个属性会指向该对象的实例
	绝大多数浏览器都支持这个非标准的方法去访问原型，但是它并不存在于Person.prototype中，而是Object.prototype中，
	与其说它是一个属性，不如说是一个getter/setter, 当使用obj.__proto__,也就相当于返回了Object.getPrototypeOf(obj)

	constructor
	每个原型都有 constructor 属性指向关联的构造函数、

	``` javascript
	function Person() {
	}

	var kidd = new Person();

	console.log(kidd.__proto__ === Person.prototype) // true
	console.log(Person === Person.prototype.constructor) // true
	console.log(Object.getPrototypeOf(kidd) === Person.prototype) // true
	
	// *实例本身是没有 constructor 的，但是会从原型上去取
	console.log(kidd.constructor === Person.prototype.constructor) // true
	```

	原型链
	`console.log(Object.proptotype.__proto__ === null) // true`
	Object.prototype没有原型

### 继承
	1. 原型链继承

	``` javascript
		function Animal(type) {
			this.type = type
		}
		Animal.prototype.getType = function() {
			console.log(this.type)
		}

		function Human() {
		}

		Human.prototype = new Animal();
		var hu = new Human();
		hu.getType()
	```
	问题：
	a. 引用类型的属性被所有实例共享 b. 创建Human实例时，无法向Animal传参

	2.构造函数（经典继承）

	``` js
		function Animal(type) {
			this.type = type;
		}

		function Human(type) {
			Animal.call(this, type)
		}

		var hu = new Human('human');
		var newH = new Human('newHuman');
	```
	优点：
	a. 避免了引用类型的属性被所有实例共享 b. 可以在 Human 中向 Animal 传参
	问题：
	Animal方法都会在构造函数中定义，每次创建实例都会创建一遍方法

	3.组合继承

	``` js

	```

### 技术沉淀？
!!!

### 单元测试 & 功能测试
### *** setState 原理
https://zhuanlan.zhihu.com/p/44537887
从setState到state更新页面渲染整个过程是一个异步过程，
<!-- react 会将多个setState合并成一个， -->
<!-- 具体方式是通过一个队列来保存每次setState的数据，然后异步去清空这个队列，在清空的过程中执行合并和更新state，最后渲染组件。但是如果只是根据合并setState的队列去渲染的话，那么同一个组件可能会因为多次setState去渲染多次，所以又多了一个队列去保存每次更新state对应的组件，而且这个队列中同一组件只入队一次，之后在清空队列的操作中，遍历组件的队列去渲染每一个组件。
至于异步，用的是Promise.resolve -->

具体实现是通过2个队列分别去保存每次SetState的操作和对应的组件，但是后者对于同一组件只会入队一次，之后就是异步去清空这两个队列，在清空的过程中去执行合并更新State和渲染组件。
队列机制 先进先出 push shift

### ** HOOKS
函数组件没有状态，
hook让函数组件可以拥有状态，而且提供了类似didMount和didUpdate等生命周期方法
丰富了函数组件的使用场景
Class 类组件因为自己本身的状态存在太重了
当然官方也说了HOOKS不会替代class

useState 入参是state的初始值，返回了一个包含2个元素的数组，前者是当前state的key，后者是更新该state的函数
而存放这些的hook数组是react调用函数组件的时候设置的，一开始它是空的，每调用一个hook，react都会向这个数组去添加一个hook

useEffect 接受一个函数作为参数，同时这个函数能返回一个函数，这个返回的函数会在组件卸载时自动调用，


### 渲染属性（Render Props) 和 高阶组件（High-Order Components）
### ** Fiber 解决了什么问题 引申 时间切片

### 算法 
	单链表

	二叉树

### React Diff

### React Context

### http 2.0
	与前端相关：
	多路复用：允许同时通过单一的http连接发起多重的请求
	http头部压缩和缓存
### promise async/await
	Promise，相较于之前的回调函数，是一种更优雅合理的异步编程的解决方案。
	作为对象，内部只有三种状态 pending fulfilled rejected,状态只会单向流转，也不能cancel

### bind apply call 
	三者都是用来改变this指向的
	bind 返回了一个新函数 新函数的this指定为bind()的第一个参数，如果undefined或为null,就会指向当前执行作用域的this,

	call 除了第一个参数，其他正常依次传参

	apply 只接受两个参数，第二个将参数作为数组传入即可

<!-- 三者第一个参数都是this要指向的对象，如果如果没有这个参数或参数为undefined或null，则默认指向全局window。 -->
	三者都可以传参，但是apply是数组，而call是参数列表，且apply和call是一次性传入参数，而bind可以分为多次传入。
	bind 是返回绑定this之后的函数，便于稍后调用；apply 、call 则是立即执行 。

### redux
	#### 三大原则
	1. 单一数据源
		整个应用的 state 存储于 object tree 中， 且这个 object tree 只存在于唯一一个 store 中
	2. state 只读
		唯一改变 state 的方式就是触发 action，action 是一个用于描述已发生事件的普通对象
	3. 使用纯函数执行修改
		为了描述 action 如何改变 state tree, 你需要编写 reducers
		
### new 语法糖
	函数调用前加上 new 就可以把任何函数当作一个类的构造函数去使用

### 基本数据类型 & 原始数据类型
	原始数据类型：
	Undefined, Null, Boolean, Number, BigInt, String, Symbol

	引用数据类型：
	Object

### 堆与栈
	栈 会自动分配内存空间，自动释放
	堆 动态分配内存，大小不定不会自动释放

	栈 heap
		原始数据类型直接存储再栈中，引用数据类型只存储一个地址来表示对堆内存的引用
	堆 stack 
		引用数据类型存储在堆中

引申下复制
	基本数据类型进行复制时，系统会自动为新变量在栈内存中分配一个新内存区域
	引用数据类型复制时，系统也会为新变量在栈内存中分配，但是这个值仅仅是一个指向原变量的堆内存的相同地址

### import & require
	require 是AMD规范引入方式 因为是在运行期调用，所以可以随处引用
	引用过程是赋值

	import 是ES6的一个语法标准，是编译时调用，必须放在文件开头引入
	只选择import的接口进行编译，性能上优于require
	支持编译时静态分析
	import是解构过程


### event loop
	MacroTask: script全代码， setTimeout, setInterval, I/O UI Rendering

	MicroTask: Process.nextTick(node), Promise, MutationObserver

	main thread 主线程
	call-stack 调用栈 所有的任务都会被放到调用栈等待主线程去执行

### react class/函数组件
	前者有实例，后者无，react内部对两种组件的实现还是有明显区分的，前者是new一个实例，后者直接运行。判断标识是 Component.prototype.isReactComponent = {}

### JS运行机制
	页面存在大量用户交互，强调注重同一时刻只做同一件事	

### arguments 对象
	箭头函数没有arguments对象

	``` js
	// 类数组对象转数组 keyword 迭代器
	// 1 拓展运算符
	function getArguments() {
		[...arguments].map(x => {
			console.log(x);
		})
	}
	// 2 call
	function getArguments() {
		console.log(arguments);
		// [].slice.call(arguments).map(x => {
		Array.prototype.slice.call(arguments).map(x => {
			console.log(x);
		})
	}

	// 3 Array.from
	function getArguments() {
			Array.from(arguments).map(x => {
				console.log(x)
			})
	}

	// PS: 针对 arguments 也可以使用 rest运算符直接替代 arguments
	function getArguments(...args) {
		args.map(x => {
			console.log(x)
		})
	}

	getArguments(1,2,1,4,3)
	```

#### 防抖 debounce & 节流 thorttle
	防抖是在单位时间内减少重复调用的次数
	节流是不减少次数但是控制多次调用间的间隔
	整体上都是降低频率

	``` js
	debounce = function (callback, time = 0) {
	let timer;
	return function (params) {
		if(timer) clearTimeout(timer);
		setTimeout(() => {
			callback(params)
		}, time)
	}
}

thorttle = function (callback, time = 0) {
	let timer;
	return function (params) {
		if (!timer) {
			setTimeout(() => {
				callback(params);
				timer = null;
			}, time)
		}
	}
}
	```

### 深拷贝 & 浅拷贝
	```  js
	function shallowCopy(obj) {
		let copy = {};
		for(prop in obj) {
			if(obj.hasOwnProperty(prop)) {
				copy[prop] = obj[prop]
			}
		}
		return copy;
	}

	function deepCopy(obj) {
		if(typeof obj !== 'object') return obj;
		let copy = typeof obj === 'symbol'? obj : new obj.constructor()
		if(obj instanceof RegExp) return new RegExp(obj);
		if(obj instanceof Date) return new Date(obj)
		if(obj instanceof Set) return new Set(obj)
		if(obj instanceof Map) return new Map(obj)
		for( prop in obj) {
			if(obj.hasOwnProperty(prop)) {
				copy[prop] = deepCopy(obj[prop])
			}
		}
		return copy
	}
	```
### 内存泄漏	
	- 闭包
	- 意外的全局变量 
	``` js
		function a() {
			let a= b = 0
		}
	```
	-未及时清除的定时器
	-脱离dom的引用

### ES6新特性 
	块级作用域 class 箭头函数 模板字符串  Object,Array的一系列方法或操作（解构 rest/拓展运算符 promise Symbol Map Set proxy

### 什么是高阶函数
	-函数作为参数或返回值的函数
	``` js
	function highOrder(params, callback) {
		return callback(params)
	}
	```

### reduce 
	``` js
	// 数组扁平化 对应方法有 arr.flat(n)
		fn = (arr) => {
			return arr.reduce((pre, cur) => {
				return pre.concat(Array.isArray(cur) ? fn(cur) : cur);
			}, [])
		}
	
	// 数组求出现次数
		total = (arr) => {
			return arr.reduce((pre, cur) => {
				pre[cur] = pre[cur] ? pre[cur] + 1 : 1; 
				return pre
			}, {})
		}

	// 数组去重
		duplicateRemoval = (arr) => {
			return arr.reduce((pre, cur) => {
				if(!pre.includes(cur)) {
					pre.push(cur)
				}
				return pre
			},[])
		}

	// my_name 转 驼峰
			toCamelCase = (str) => {
			const arr = str.split('_');
			return arr.reduce((pre, cur, index) => {
				console.log(pre, cur, index);
				return pre += cur.charAt().toUpperCase() + cur.substr(1)
			})
		}	
	```	

### substr & substring
	substr(startIndex, length) 
	若startIndex小于0，则看作是 length + startIndex,即从末尾开始数
	substring(startIndex, endIndex)	
	参数最小值为0，且始终会让 startIndex < endIndex

### slice & splice（TBC）
	slice(startIndex, endIndex) 浅拷贝数组
	若startIndex省略，则从0开始
	若startIndex小于0，则看作是 length + startIndex,即从末尾开始数
	若startIndex大于length - 1，则返 []

	若endIndex省略，则取到末尾
	若endIndex小于0，则看作是 length + endIndex,即从末尾开始数
	若endIndex大于length -1，同上

	若startIndex和endIndex 不合理，也返 []

	splice(startIndex, deleteCount, item1,item2,...) 删除数组，返回的是实际删除的数组
	若startIndex省略，则从0开始
	若startIndex小于0，则看作是 length + startIndex,即从末尾开始数
	若负数绝对值大于length,则从0开始

### 观察者模式
	观察者被动接收更新，功能耦合度降低，各自专注自身功能逻辑
	不足：不能对事件通知进行细分处理，所有观察者都会收到通知
### 发布-订阅模式

### 单例模式




