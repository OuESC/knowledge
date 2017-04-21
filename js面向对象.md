## 1.try - catch - finally：进行异常处理
		// 代码报错以后，会阻碍后续代码的执行！
			try{
				// 放置可能会出现异常的代码
				// 手动抛出异常：
				// throw 扔
				// throw new Error('代码出错了！');
				// throw '字符串';
			}catch(e) {
				//如果try中代码出现了异常，此时就会被捕捉到，并通过e获取到响应的错误；如果try中没有出现异常，那么 catch 中的代码是不会执行的！
			}finally {
				//不管什么情况下，这里的代码都会执行
			}

## 2.面向对象的相关概念
		> 面向对象是一种编程的思想，同时也是一种语法规范，让我们能够通过这个语法规范，实现面向对象编程！
		
		// 1 面向对象 与 面向过程的区别
		// 2 JS中如何实现面向对象
		// 3 其他语言中面向对象
		
		// 面向过程：所有的步骤都是需要我们亲历亲为，其实就是一个：执行者
		// 面向对象：只需要找到相应的对象，然后，这个对象就能够帮我们完成整个操作
		// 					 其实就是一个：调度者
		
		// 案例：动态创建元素，并且设置内容
		/*var dv = document.createElement('div');
		// dv.innerText = '动态设置内容';
		// 创建文本节点
		var txt = document.createTextNode('动态设置内容');
		dv.appendChild( txt );

		document.body.appendChild( dv );*/
		
		// jQuery的实现方式：
		// $('<div>动态设置内容！！！</div>').appendTo('body');

		// 面向对象的方式要比面向过程的方式要简单很多，能不能说明：
		// 			面向过程就没什么用处了？？？
		// 面向对象还是由面向过程来实现的！
		
		// 适用于中大型项目中，以及各个框架中：
		// 面向对象思想不会提高代码的执行效率，提高了代码的可维护性以及扩展性


##	3.构造函数
		 1 使用对象不适用于创建多个对象的场景，如果要使用对象，只能复制代码！那么可以通过构造函数在new出多个对象

		// Person就是一个构造函数
		// 构造函数本质上就是一个普通的函数，如果一个函数要作为构造函数，那么约定：首字母大写！
		// 如果要给创建出来的对象添加属性，需要在构造函数中
		// 通过 this.属性名 = 值 这种形式来添加！
		function Person() {
			// 只要是给 this 添加的属性，就可以通过new创建出来的对象访问到！
			this.name = '小明';
			this.age = 18;
			this.gender = 'male';
		}

		// 并且调用的时候，需要配合 new 运算符来使用
		// 作用：创建Person类型的对象
		var p1 = new Person();
		console.log(p1);

		var p2 = new Person();
		console.log(p2);

		// 创建对象, 每次使用 new Person() 都在内存中创建了一个新对象！

		// 构造函数中一般情况下只放：公共的属性
			// 注意：构造函数中可以放置方法，但是不推荐这么做！
			// 			 因为函数的逻辑都是相同的，所以，是可以实现复用的！
			// 			 但是，如果将方法放到了构造函数中，那么，每创建一个对象
			// 			 在内存中就会有这个方法的一个副本！
			// 			 因为将方法放到构造函数中，会造成内存的浪费！

		//那么这就引出了构造函数的原型 放置方法
			// 原型：构造函数的prototype属性的值
			// 注意：
			// 1 只要是创建一个函数，就会有prototype属性
			// 2 prototype属性的类型是 object 类型的
			// 3 原型的作用：实现数据共享，
			// 4 原型中用于存放各个对象共有的属性或方法
			// 5 通过构造函数创建出来的对象，默认情况下，就可以使用原型对象中的属性和方法

			//使用面向对象的方式组织代码
				1.属性都放在构造函数中
				2.方法都放在原型中


			// __proto__ 是一个非标准的属性! 不能用在实际项目开发中!
			// 这个属性,一般就是用来查看 对象与原型对象 之间的关系!
			// 
			// __proto__ 是站在创建出来的对象的角度, 来访问 原型对象
			// prototype 是站在构造函数的角度, 来访问 原型对象
			// 这两个属性表示的是同一个对象!


##	4.js继承：
		A：js的混入式继承：利用 extend 封装一个方法

			//让对象obj继承自o1 和 o2 
			var obj = {} ;
			var o1 = {
				name:'zs',
				age:18,
				say;function() {}
			};
			var o2 = {
				run:function(){},
				sex:'man'
			};
			//使用extend方法
			obj.extend = function(o) {
				//遍历
				for(var k in o) {
					obj[k] = o[k] ;
					//或者也可以写成:谁调用方法，this就指向谁
					//this[k] = o[k]
				}
			};
			//使用
			obj.extend(o1) ;
			obj.extend(o2) ;
			console.log(obj) ;

			//或者也可以自己去扩展
			obj.extend = function() {
				html:function(){},
				attr:function(){}
			};
			//上面代码可以简写
			obj.extend({
				html:function(){},
				attr:function(){}
			});

		B：原型式继承：对象继承自原型对象，是对象和原型对象之间的关系，如果想让对象使用某些公共的属性或方法，只需要将这些属性和方法，添加到原型中即可。

				//给原型添加成员的方式：
				1.利用对象的动态性(可以在任何情况下，给对象添加属性和方法)
				2.利用覆盖原型对象的方式
				3 利用混入式继承来添加成员

				//混入式继承
				function Person() {} 
				Person.prototype.extend = function(obj) {
					for(var k in obj) {
						this[k] = obj[k] ;
					}
				}
				//调用这些方法：这些方法是添加给原型的
				Person.prototype.extend({
					coding: function() {
						console.log('js是世界上最好的语言！')
					},
					sleeping: function() {},
					legs: 2
				});

				var p2 = new Person();
				p2.coding();

				console.log(p1.legs);
				p1.coding();

				//覆盖原型对象
				// 默认情况下，原型对象中有一个属性：constructor 会指向当前的构造函数！
				Person.prototype = {
					// 仅仅是为了与默认情况下的原型保持一致！
					// constructor: Person,

					legs: 2,
					say: function() {},
					coding: function() {}
				};
				var p1 = new Person();
				console.log(p1.legs);*/

				// 1 对象的动态性
				/*function Person() {
					this.age = 19;
				}

				var p1 = new Person();
				console.log(p1.legs)

				Person.prototype.legs = 2;
				Person.prototype.coding = function() {};
				Person.prototype.say = function() {}

				console.log(p1.legs);*/

		C：经典继承：Object.create();
		
			// 语法：var newObj = Object.create( 被继承的对象 );

			// 返回的新对象 newObj 就会继承自 参数对象obj
			// 两个对象的关系：参数对象obj 变为了 返回对象newObj的 原型对象
			var newObj = Object.create( obj );
			console.log( newObj );

			console.log(newObj.__proto__ === obj);*/

			// create方法的参数必须是一个对象或者null
			// 如果传入一个 null，那么会创建一个不会继承自其他对象的对象
			// 此时，就相当于创建了一个没有原型对象的对象
			var obj = Object.create( null );
			obj.name = '123';
			console.log(obj);
			console.log(obj.__proto__);

			// Object.create方法的特点：
				// 1 会创建一个新对象
				// 2 新创建的对象会继承自 参数对象
				// 3 会把创建的新对象放回

##	5.原型链
		// 什么是原型链？
		// 任何一个对象都有一个原型对象，原型对象也是对象，所以，原型对象也有原型对象
		// 这样，一环扣一环，形成了一条链式结构，把这个链式结构称为：原型链
		
		// 从原型链的角度定义原型式继承：
		// 任何一个对象都有一条原型链，所谓的原型式继承，就是通过任意手段来修改这条原型链的
		// 层次结构，对象可以访问原型对象中的属性和方法，从而实现继承！

		// 通过对象的 __proto__ 这个属性，可以访问到当前对象的原型对象

		// 任何一个对象都直接或间接的继承自 Object.prototype 
		// 也就是说，任何对象都可以使用 Object.prototype 这个对象的中的属性和方法

		// 1 创建对象的时候，原型对象就已经定下来了！
		  // 		其实，该对象的整个原型链就定下来了！
		  // 2 创建对象的时候，当前的原型对象是谁，对象的原型对象就是谁！

##	6 原型链
		// 继承就是沿着原型链继承的！ 对象继承的所有的原型对象都在原型链中
		// 属性搜索原则：也是沿着原型链进行搜索的！
		// 原型链其实就是-->构造函数、原型对象、实例对象 三角形关系

		// 面向对象的三大特征
		// 封装 继承 多态

		//任何一个对象都与 Object.prototype 这个对象有关系


##	7. Object.prototype中的成员

		//1.constructor 构造器 指向 当前的构造函数

		//2.hasOwnProperty('属性')；
		// 作用：用来判断某个属性是不是对象自身提供的，如果是返回true，否则：返回false
		// 语法： var hasProp = 对象.hasOwnProperty(属性)
		// 结论：只有自身的属性，结果才为true
		// for-in 循环只能遍历自定义的属性，内置的属性，是无法被遍历到的！

		//3.isPrototypeOf 是...的原型
			语法：var 布尔值 = 对象1.isPrototypeOf(对象2)
			作用：判断 对象2的原型链中 是否包含 对象1 如果包含，就返回：true
					 否则，返回 false

		//4 propertyIsEnumerable 判断属性是否可枚举
		语法： 布尔值 = 对象.propertyIsEnumerable(属性)
		// 作用：1 判断属性是不是对象自身提供
		// 			 2 判断属性是否是可枚举的！
		// 			 以上两点都是满足，结果为true，否则， 就为：false

##	8.instanceof运算符 
		// 作用: 用来判断 构造函数的prototype的值 是否在被检测对象的原型链上, 如果在 结果就是: true, 否则就是: false
	  
		// 语法: 布尔值 = 对象 instanceof 构造函数

		// 规律:
		// 创建对象以后,没有再修改过 构造函数的.prototype 的值
		// 那么结果就为: true, 否则就为:false 

##	9.遍历的方法
		// 数组中有很多遍历当前数组的方法:

		// arr.forEach 就是遍历数组, 但是无法停止循环
		var arr = ['a', 'b', 'c'];
		// arr.forEach(function(value, index) {
		// 	console.log('索引号为:' + index + ', 值为: ' + value);
		// });

		// arr.map 
		// arr.some
		// arr.filter

		// arr.every
		// 返回值由数组中所有项的回调函数的返回值决定,
		// 如果所有的返回值全部为: true, 那么 every 方法的返回值为: true
		// 否则, 为: false
		var ret = arr.every(function(value, index) {
			// 该方法会根据回调函数的返回值来确定是否继续循环
			// 如果当前函数的返回值能转化为: false, 那么循环就会停止
			// 否则, 循环继续
			console.log('索引号为:' + index + ', 值为: ' + value);
			return false;
		});
		console.log(ret);

##	10. new Function() 的使用
		 使用 new Function 来创建函数
	  	// 因为new是创建对象的, 此处, 是创建了一个函数对象, 所以, 函数也是对象!
	  	// 语法: var fn = new Function();

	  	实例：var sum = new Function('num1','num2', 'return num1 + num2 ;') ;
	  			console.log(sum(7,8)) ;

		实例二：var Max = new Function('num1','num2','return num1 > num2 ? num1 : num2 ;')
				console.log(Max(1,7)) ;

		new Function() 和 eval 的相同点：
		// 1 参数都是字符串
		// 2 将字符串当作代码来执行

##	11.对象原型连 与 函数原型链 之间的区别
		// 对象的原型链中：
		// 将函数看作是 构造函数，其作用是用来创建对象（实例）
		// 
		// 函数的原型链中：
		// 将函数看作是 对象 ，此时，函数看作是Function的实例
		
		// 对象的原型链：
		// 构造函数：   Person
		// 对象：		p
		// 原型：		Person.prototype
		// function Person() {}
		// var p = new Person();
		
		// 函数的原型链：
		// 构造函数：	Function
		// 对象：		Fn
		// 原型：		Function.prototype


##	12.静态成员 与 实例成员
		成员：对象的属性和方法统称为成员
		实例（对象）：由构造函数创建出来的对象
		实例化：由构造函数创建对象的过程，称为实例化的过程

		实例成员：由实例对象能够访问到的成员，就叫做 实例成员；
					一般情况下，实例成员包括对象本身的属性和方法，也包括原型对象中的属性和方法

		静态成员：是与构造函数相关的，由构造函数能够直接访问到的属性和方法，就叫做：静态成员
					一般情况下，只能通过 构造函数.成员 = 值; 这种形式添加一个静态成员

		静态成员 和 实例成员中的成员是不会共享的！
		也就是说： 静态成员访问不到实例成员中的属性和方法，反之，也是如此！

		实例：/*var Person = function() {
					this.name = '小明';
				};

				Person.prototype.say = function() {}

				// p是一个实例对象
				var p = new Person();

				// 实例成员！
				console.log(p.name)
				p.say();

				// 静态成员：
				Person.each = function() {};
				Person.each();*/

##	13.场景： 静态成员 与 实例成员 中可能会存在一个相同的方法
		// 
		// 最佳实践：
		// 给静态成员添加这个方法，如果实例成员要使用这个方法，只需要调用静态成员中
		// 提供的方法即可！
		实例：var Person = function() {} ;
			  Person.each = function(num1,num2) {
			  	console.log('静态方法' + num2) ；
			  }
			  Person.prototype.each = function(num1) {
			  	Person.each(num1,123);
			  }
			  var p = new Person();
			  p.each(1234);

##  14.函数的相关成员介绍
    	fn函数

    	length属性 ： 表示形参的个数
    	console.log(fn.length)

    	name属性：表示当前函数的名字，字符串格式；IE中不支持这个name属性

    	arguments : 任何一个函数都有 arguments 变量，arguments 只能在函数内部来使用
    				arguments 是一个伪数组，无法使用数组的方法
    				arguments中有一个 length 属性表示：实参的个数
    				arguments中还有一个 callee 属性，表示当前函数的引用

    				作用：用来获取实参列表

		如何判断函数传入的参数个数是否正确？
		var fn = function(num1,num2){
			//fn.length 表示形参的个数， arguments.length 表示实参的个数
			if(fn.length !== arguments.length ) {
				throw new Error('请输入正确的参数')
			}
		}

		arguments.callee === fn 


##	15 递归的应用
		函数自己调用自己
		//怎么写递归：1.什么时候递归：化归的思想：将要解决的事情，归结为之前解决过的问题上
					  2.什么时候结束递归：找到临界条件，让当前函数停止执行

		  死递归：会造成堆栈溢出（占用内存太多）

		  实例：斐波拉契数列
		  var fib = function(num) {
		  	if(num === 1 || num === 0) {
		  		return 1 ;
		  	}
		  	return fib(num - 1) + fib(num -2) ;
		  };
		  console.log(fib(5)) ;

		  实例二：求阶乘
		  var fact = function(n) {
		  	if(n === 1) {
		  		return 1 ;
		  	}
		  	return fact(n - 1) * n ;
		  }
		  console.log(fact(5));

##	16.作用域：变量的作用范围
		两种作用域：块级作用域  函数作用域(词法作用域)

		块级作用域：
			代码块： {}花括号内部构成了一个代码块
		 				在支持块级作用域的编程语言中，在代码块内部声明的变量，在代码块的外部是无法访问到的！
		 				// ES6 规范中，可以使用 let 声明一个局部变量，在代码块中起作用！
						// 就相当于通过 let 关键字，让js支持了 块级作用域
				
		词法作用域：
			又称函数作用域，因为在js中只有函数才能形成一个作用域，变量的作用域范围在书写代码的时候，就已经定下来了，与运行时（代码执行）无关	
			对于函数来说，函数的作用域范围只与函数声明的位置有关，而与函数在什么位置调用没有关系
			**规律：在分析函数作用域问题的时候，只看函数在哪个位置创建的，而不管在什么位置调用的

		js代码执行的过程：
		// 1 预解析 -> 变量提升！
		// 2 一行一行从上往下执行代码
		// 3 变量：只提升声明，不提升赋值；函数：是把整个函数提升，或者为：将函数名字（变量）提升并且给这个变量设置了默认值：函数

		对于变量来说，只看变量声明！
		// 查找变量的时候，首先会在当前作用域中查找变量的值
		// 如果当前作用域中没有声明变量，会到上一级作用域中查找


##	17.作用域链
		作用域链：
		// 任何一个函数都能够形成一个作用域，这个函数有可能是嵌套在其他函数中的，
		// 嵌套函数也是有作用域的，这样多个作用域也形成一条链式结构：就把这个
		// 链式结构称为： 作用域链

		// 变量的搜索原则：是沿着作用域链进行搜索的
		// 1 首先在当前作用域中查找（声明！）有没有声明这个变量，如果有就直接使用
		// 2 如果没有，就到上一级作用域中查找
		// 3 这样一直往上找，直到全局作用域
		// 4 如果在全局作用域中也没有找到（声明），那么就会报错！

##	18.绘制作用域链
		// 绘制作用域链逻辑图的时候，只绘制在当前作用域中声明的变量或函数！
		// 将全局作用域看作是：0级别的链
		// 如果在全局环境中创建了一个函数，此时，就在当前链级别的基础上加1

##	19 怎么理解函数的参数？
			// 把函数的参数理解为函数内部的局部变量！
			// 参数，就相当于是我们自己声明的变量

##	20 函数声明 与 函数表达式 的 区别
		使用函数声明创建的函数，会将整个函数体提升到当前作用域的最顶端！
		对于函数表达式来说，仅仅是把声明变量提升了
		使用函数声明的形式创建函数，只能出现在两种位置：
		// 1 全局作用域中
		// 2 出现在其他函数中！


##	21 总结
		// 1 属性的读取和设置
		// 读取：（原型链）
		// 		首先在当前对象中查找，如果有，就直接返回
		// 		如果没有，就在对象的原型对象中查找，如果有，就返回
		// 		如果还没有，就继续在原型对象的原型对象中查找，直到 Object.prototype
		// 		如果还是没有找到，就返回 undefined
		// 
		// 设置（只与当前对象有关）：
		// 		只会操作对象本身，如果对象中没有该属性则创建该属性，并赋值；
		// 		如果对象中有，则修改

		// 2 变量的读取和设置
		// 读取：（作用域链）
		// 		首先在当前作用域（n级链）中查找(只查找声明)，如果有，就直接返回
		// 		如果没有，就在 n-1级链 中查找，如果有，就返回
		// 		如此往复，直到 0级链（全局作用域）
		// 		如果还没有找到，就报错（因为访问了一个没有声明的变量所以会报错）
		// 		
		// 设置：（创建全局变量）
		// 		首先在当前作用域（n级链）中查找，如果有，就直接赋值
		// 		如果没有，就在 n-1级链 中查找，如果有，就直接赋值
		// 		如此往复，直到 0级链
		// 		如果还没有找到，就创建全局变量（不要这么做！）
		// 		
		// 		使用变量的时候，一定要先声明再赋值！


		// 作用域分两种：
		// 1 块级作用域（JavaScript不支持）
		// 	if(true) { var num = 123; }
		// 	for() {}
		// 2 词法作用域 （函数作用域）
		// 		a. 变量的作用范围在书写代码的那一刻，就定下来了，与运行时无关
		// 		b. 在函数内部定义的变量，在函数外部无法访问到
		// 		c. 在函数内部能够访问到函数外部声明的变量，但是在外部无法访问到内部函数的变量


		// 什么叫词法作用域？
		// 变量在声明的时候，作用域就定下来了，与运行时无关
		// 
		// 对于作用域的问题，只看函数是在哪个环境中创建的，而不管是在哪个环境中调用的！


		// 在作用域链 或者 原型链中的同名的属性，会被“覆盖”,同名的变量或属性
		// 只能够访问到最近的一个！


		// 作用域链：
		// 每个函数都会形成一个作用域，如果函数被其他函数包裹，
		// 包裹函数也有作用域，一直往上直到全局环境。
		// 这样就形成了一条作用域链。


		// 作用域链绘制规则
		// 1 绘制的时候指绘制：当前作用域中声明的变量或者函数
		// 2 如果遇到函数，就引出一条新的链出来，如果函数是在n级链中声明，
		// 			那么就 引出 n + 1 级链
		// 
		// 变量搜索原则： 从相关的高级链往低级链中查找

		 // 怎么理解函数的参数？
		  // 把函数的参数理解为：函数内部的局部变量
		  // 相当于js引擎：帮我们创建了一个变量a，并且赋值为：实参的值
		  // 

##	22 变量 函数 参数 命名冲突的问题
		1.如果一个变量与一个函数命名冲突：赋值之前访问，返回函数，赋值之后访问，返回变量
				/*var fn = 123;
				function fn() {}
				console.log(fn); // 123*/

				/*var fn;
				function fn() {}
				fn = 123;
				console.log(fn); // 123*/

				/*console.log(fn); // function fn() {}
				var fn = 123;
				function fn() {}*/

				/*var fn;
				function fn() {}
				console.log(fn); // function fn() {}
				fn = 123;*/
		2.参数与变量命名冲突：
		// 规律：// 如果一个函数与参数命名冲突了，此时，结果就是：函数的值
				  // 如果一个变量与参数命名冲突了，此时，
				  // 	如果是在赋值之前访问的，那么，结果就是：实参的值
				  // 	如果是在赋值之后访问的，那么，结果就是：赋值之后的值！
				  /*(function(a) {
					    console.log(a);//function a() {}
					    var a = 10;
					    function a() {}
					  }(100));*/

					  /*(function(a) {
					  	var a = 100;
					    console.log(a);//100
					    var a = 10;
					    function a() {}
					  }(100));*/



##  23. 自调用函数：
	  // 前面小括号的作用：是将函数声明转化为函数表达式！
	  // 	小括号中只允许出现表达式！
	  // 	就是告诉 js解析引擎 将函数解析为函数表达式，而不是函数声明！
	  	/*(function() {})();
		  (function() {}());
		  !function() { console.log( 123 ) }(); // 推荐
		  +function() { console.log( 123 ) }();
		  -function() { console.log( 123 ) }();*/

##  24.闭包：就是封闭和包裹，也就是在函数内部创建的变量，在函数外部是无法访问的，
			 因此就说这个函数形成了一个闭包

	  因为函数内部是一个独立的作用域，所以在函数内部声明的变量，在函数外部无法访问到

	  js中任何一个函数都可以形成一个闭包

	  闭包有两部分组成：函数体，函数所处的环境

	  另一方面理解闭包：闭包是由函数体以及函数所处的环境构成的一个综合体

	  闭包是作用域的应用：不管函数在哪个函数中调用，最终都要回到创建他的环境中执行

	  很多认为：函数内部嵌套另外一个函数把这种形式称为一个闭包

	  常用的闭包模型：
	  var fn = function(){
	  	var num = 123;
	  	return function(){
	  		console.log(num);
	  	}
	  	}

	  	闭包的作用:对函数内部的变量起到了保护作用
	  				闭包的多次调用，能够共享同一个变量


##	25.普通函数 与 闭包函数 之间的区别

	  	// 普通的函数：
			/*var fn = function() {
				var num = 0;
				num++;
				console.log(num);
			};
			fn(); // 1
			fn(); // 1*/

			// 为什么结果是两个1？？？
			// 1 调用函数的时候，浏览器会自动的给这个函数分配一块内存
			// 2 在函数内部声明的变量，就保存在这块内存中了！
			// 3 只要函数调用结束了，这块内存(调用函数产生的内存)就自动释放掉（由js的垃圾回收机制完成，自动回收）！
			
			// 闭包的函数：
			var fn = function() {
				var num = 0;

				return function() {
					num++;
					console.log(num);
				};
			};
			
			// 函数 fn的代码仅仅执行了一次，因为函数fn只被调用了一次！
			var f = fn();
			// 接下来的操作，都是调用 函数fn内部返回的函数了！
			// 因为 返回函数是在函数fn内部创建的，所以，能够访问到 函数fn 内部的值！
			f();
			f();
			f();
			
			// 闭包占用的内存是不会被释放掉的！
			// 所以，应该是在必须要使用闭包才能解决问题的时候，才使用闭包！
			// 没有被释放掉的原因：是因为内部函数的作用域链包含了外部的函数
			// 										 并且是内部的函数只要是在调用的时候，
			// 										 就可以访问到外部函数中的变量！



			// https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Memory_Management
			// 垃圾回收机制：浏览器会在特定的时间来检查js中是否有不在使用的内存了，如果有，
			// 							 垃圾回收机制，会在某个特定的时间点，将这块内存回收（将内存释放，
			// 							 其他的js代码就可以使用内存了，如果不释放，那么这块内存就一直被
			// 							 占用，其他的js代码，也无法使用！
		


##	26.缓存机制
		// 缓存： cache 
		// 缓存就是数据交换的缓冲区（称作Cache）
		// 对于编程来说，缓存的使用可以提高程序的执行效率！

		// 怎么通过js代码来实现缓存？
		// 一般情况下使用 对象 来当作缓存
		
		// 使用缓存的步骤：
		// 1 先从缓存中查找有没有需要的数据
		// 2 如果有，就直接拿过来使用
		// 3 如果没有，就计算，并且将计算的结果再放到缓存中
		
		// 往缓存中添加数据：给对象添加属性
		// 从缓存中取出数据：获取对象的属性

		/ 使用缓存来解决递归存在大量重复计算的问题！
		// 
		// 为什么要讲缓存对象放到 闭包中？
		// 因为使用缓存就是完全信赖缓存中的数据，所以，这个缓存应该收到保护！
		// 并且其他人员是无法来操作缓存的值的！

		 如何取数据：   cache[key]
  		// 如何设置数据： cache[key] = value

##	27.使用闭包和缓存解决重复计算的问题
		// 1 先到缓存中查找，如果有就直接使用
			// 2 如果没有，就计算，然后，要计算的结果放到缓存中

		方式一：var fn = function(num) {
			//缓存对象
			var cache = {} ;
			return function(num) {
				if(cache[num]){
					表示缓存中存在num对应的数据
					return cache[num];
				}
				if(num === 0 || num === 1) {
					将num对应的值放到缓存中
					return cache[num] = 1 ;
				}
					计算num对应的值，放到缓存中
					return cache[num] = arguments.callee(num - 1) + arguments.callee(num -2) ;
				}
		}();
		// 修改为自调用函数，这样用起来更加方便
		// 		因为就是通过函数表达式来创建的函数，所以，不要不需要外层的小括号
		console.log(fn(5));

##	28.沙箱模式
		在沙箱环境中做的任何操作都不会影响到外部的环境，沙箱是一个独立的环境

		在js中一般都是通过 自调用函数 来创建沙箱
		1.因为自调用函数不会再全局环境中创建任何变量，将全局污染降到最低
		2.因为在js中只有函数能够形成一个独立的作用域(环境)，函数只有调用 ，内部的代码才会执行

		推荐写代码的形式:将所有的代码都放到沙箱中，这样就会避免全局污染的问题

		 使用沙箱的目的：隔离，因为在沙箱中可能会创建很多的变量，但是
		  //                 因为函数形成了一个作用域，这样就避免了全局污染的问题！
		  
		  // 代码上线之前都是经过压缩处理的！压缩之后，文件的大小就会变的更小
		  // 网页的加载速度就会变快

		  // 将window作为参数传入到沙箱中目的：
		  // 1 减少变量的搜索
		  // 2 有利于代码压缩

		基本语法格式
			(function(){
				var num = 3 ;
			})() ;

			(function(){
				var str = 'abc'
			})();
		怎样使用沙箱模式暴露到全局环境中供其他开发人员使用？？
		var ret = (function(){
			var jQuery = function() {
				console.log('沙箱内部的jquery 函数') ;
			};

			return jQuery ;
		})() ;
		ret() ;

##	29.异步执行的概念  &&  js 执行的过程
		// 一般情况，会把setTimeout/setInterval/ajax称为一个异步执行的代码！
		// js执行的过程：
		// 1 首先会执行非异步的代码（主要的代码）
		// 2 等到主要的代码都执行完毕以后，才会执行异步的代码！

		// JavaScript 是一门单线程的编程语言！
		// 单线程：同时只能处理一件事情
		// 多线程：同时能够处理多件事情

		// JavaScript是事件（回调函数）驱动型编程语言

		// 数据结构：
		// 1 栈
		// 特点：先进后出
		// 数组的：unshift（添加） 和 shift（取出）

		// 2 队列
		// 特点：先进先出
		// 数组的：unshift（添加） 和 pop （取出）

		js 执行的过程
			// JavaScript语言本身是单线程的！
			// 
			// 浏览器是有一个多线程，与js相关的线程有三个：
			// 1 js主线程（作用：执行js代码）
			// 2 事件循环线程（作用：遍历事件队列，取出回调函数，交给主线程）
			// 3 UI渲染线程（将通过js或css设置的效果，渲染到页面中，这样用户就能看到效果了）

			// JS主线程 与 UI渲染线程是 互斥的！
			// 要么js主线程在执行，要么就是 UI渲染线程 在执行

			// 要把所有的js文件放到页面最底部引入！


##	30 setTimeout 依次打印出 0 --- 9 
		第一种方式：闭包和setTimeout 的应用
		for(var i = 0 ; i < 10 ; i ++) {
			var fn = function(index) {
				return function() {
					console.log(index);
				};
			};

			var f = fn(i) ;
			setTimeout(f, 500 * i) ;
		}

		第二种方式：沙箱(自调用)和setTimeout的应用
		for(var i = 0 ; i < 10 ; i ++) {
			setTimeout(function(index){
				return function() {
					console.log(index);
				};
			}(i),500 * i)
		}

##	31 函数中 this 的指向问题
		函数的四种调用方式：
			1.函数调用方式
			2.方法调用方式
			3.构造函数调用方式
			4.call 、apply 

		// 每个函数内部都有一个this, 所以, 需要区分this是属于哪个函数的！
		如果要查看函数中 this 的指向问题，只需要关注函数是以什么方式被调用的，而不管函数是怎么被声明的

		1、函数的调用模式：一个函数直接调用，与任何对象都没有关联，此时，this ==> window
			实例：function fn() {console.log(this) ;} ; fn(); // this === window

		2、方法调用模式：如果一个函数是作为对象的属性，此时称为：方法
							方法调用模式是与对象关联的
							在方法调用模式中 this 指向了调用该方法的对象
			实例：var obj = {say:function(){console.log(this);}}; obj.say(); // this === obj

		3.构造函数调用模式：一个函数如果是作为构造函数来调用的，构造函数模式中，this 是指向了新创建出来的对象
			实例：var Person = function() {console.log(this);}; var p = new Person(); // this 就是新创建出来的对象p  

			实例分析
				/*var age = 38;
				var obj = {
			    age: 18,
			    getAge: function() {
			        function foo() {
			        	// this -> window 每个函数都有一个this，要看this是放在哪个函数中的，这个是放在foo里面的
			          console.log(this.age); // 38
		        }
		        foo();// 这里使用函数调用的，所以this就指向了window
			    }
				};

				obj.getAge();*/

				var age = 38;
				var obj = {
				    age: 18,
				    getAge: function() {
				        alert(this.age);//38
				    }
				};

				var f = obj.getAge;// 这里定义了一个变量声明，但是this不管是怎样声明的，只管是以什么形式调用的
				f(); // 以函数调用模式调用，所以，this 指向的是：window

				var length = 10;
				function fn(){
				    console.log(this.length);
				}
				var obj = 
				{
				    length: 5,
				    method: function (fn1) {
				        fn1();   // 10
				        
				        // 方法调用模式:arguments[0] 表示的是fn ，fn里面就一句 console.log（this.length）this 指向的就是arguments 然后就是2

				        arguments[0](); // 2
				    }
				};

				obj.method(fn, 123);

		4.apply : 函数后面调用apply ；语法：fn.apply(); 上下文调用模式(借用方法调用模式)
				  在 apply 和 call 方法中，this 是动态的，需要我们指定的
				  fn.apply() 这种形式最终还是调用fn
				  参数：第一个参数：表示函数fn中this的指向(应该是一个对象类型的)
				  		第二个参数：是一个数组或者伪数组，数组中的每一项都将作为被调用函数的参数

				  		var fn = function() {
						// 1 为什么使用 Array.prototype？？？
						// 		使用 Array.prototype 的目的就是为了拿到 join 方法！
						// 		也可以通过 [].join 获取到 join 方法！

						// 2 第一个参数，代表被借用方法中this的指向
						//    也可以理解为：让第一个参数借用这个方法
						// 3 第二个参数，是一个数组或伪数组, 数组中的每一项会作为被借用方法的参数
						// 		在这个例子中，[',']中的','作为了 join 方法的参数！

						// var r = Array.prototype.join.apply(arguments, [',']);
						var r = [].join.apply(arguments, [',']);
						return r;
					};

					var ret = fn('a', 'b', 'c', 'd', 'e', 'f', 'g'); // a-b-c-d
					console.log(ret);

		5.call方法：
			// call 和 apply方法的语法、作用 是完全相同的！
			// 唯一不同的地方：第二个参数类型不同
			
			// apply方法的第二个参数：是数组或伪数组
			// call 方法除了一个参数外，其他所有的参数都作为被调用方法的参数
			var fn = function(num1, num2, num3) {
				console.log(this)
				console.log(num1, num2, num3)
			};

			var obj = {};

			fn.apply(obj, [1, 9, 7]);
			fn.call(obj, 1, 9, 7);


			var Person = function(name, age, gender) {
				this.name = name;
				this.age = age;
				this.gender = gender;
			};
			
			Person.prototype = {
				say: function() {},
				running: function() {},
				sleep: function() {}
			};
			
			var p = new Person('xiaoming', 19, 'male');
			console.log(p);

			var Student = function(name, age, gender, scores, stuNo) {
				/*this.name = name;
				this.age = age;
				this.gender = gender;*/

				// 当前的 this 是谁？？？
				// 
				// 1 首先要知道 this 是在哪个函数内部的？？？
				// 	this 是在 Student 函数中的
				// 2 当前函数是以什么模式被调用的？？？
				// 	当前函数以与new来配合使用的，所以，符合构造函数模式，
				// 	this 是 新创建出来的对象！
				var that = this;
				Person.call(that, name, age, gender);

				this.scores = scores;
				this.stuNo = stuNo;
			};
			
			// Student.prototype = new Person();
			Student.prototype = Person.prototype;
			var stu = new Student('xiaowang', 16, 'male', 99, 10001);
			console.log(stu);


##	32.工厂模式创建对象
			var Person = function() {};
			var Student = function() {};
			var Teacher = function() {}
			var factory = function(type) {
				switch(type) {
					case 'p':
					return 	new Person();
					case 'student':
					return new Student();
					case 'teacher':
					return new Teacher();
				}
			}
			var p = factory('p');
			var stu = factory('Student');
			var t = factory('Teacher');
			console.log(p, stu, t);

##	33.map遍历
		var arr = [1, 8, 9];
		// map作用：也是遍历数组，但是这个方法会返回一个新数组，新数组中的元素
		// 			 是由回调函数的返回值决定的！
		/*var newArr = arr.map(function(value, index) {
			return value * 10;
		});
		console.log(newArr);*/	10 80 90 


		// parseInt 方法有两个参数：
		// 第一个参数：是一个字符串
		// 第二个参数：表示 进制
		// 
		// 作用：根据第二个参数指定的进制，来进行数值的转换！

		// 就是调用 parseInt 的时候传入了两个参数
		var arr1 = ['1', '2', '3'].map(function(value, index) {
			return parseInt(value, index);
		});
		console.log(arr1);//1 NaN NaN




