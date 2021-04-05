### JS之父 Brendan Eich 布兰登 艾克

## 押题类型

### 技术沉淀？

### *** setState 原理
setState是异步操作，
队列机制
### ** HOOKS

### ** Fiber 解决了什么问题 引申 时间切片

### 算法 
	单链表

	二叉树

### React Diff

### http 2.0

### promise async/await

### bind apply call 

### dva 和 redux 的区别
	

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




