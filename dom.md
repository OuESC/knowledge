## 二、js中阶开始，学习dom操作，之后学习bom动画等，再之后是JQ等一些插件的使用。(从原理再衍生的之后的一些插件等方法，会越来越简单，工作中要懂得化繁就简)

> DOM开始啦！！！

> ！！！dom语法的时候，就是单单的找对象，设置元素的属性、样式，动态创建元素，并没有动画等一些效果显示，！！！比较原生的js语法。这时候只需要在script标签里去写代码。

## 1.getElementById('demo');通过id找对象
	  getElementsByTagName('input');通过标签名获取元素，是一个伪数组，可以遍历；
	  	//getElementById只能被document调用
		//getElementsByTagName即可以被document调用又可以被普通的元素对象调用
		//被document调用 表示获取页面上所有这一类型的标签
		//被普通的元素对象调用 表示获取指定范围内的这一类型的标签

## 2.事件
	  点击事件：onclick
	  双击事件：ondbclick
	  鼠标经过：onmouseover
	  鼠标离开：onmouseout
	  获得焦点：onfocus
	  失去焦点：onblur
	  键盘按下的时候触发：onkeydown
	  键盘弹起的时候触发：onkeyup
	  输入内容的时候触发：oninput

## 3.绑定事件
  	> 事件源.事件 = function() {事件处理程序} ;39

## 4.表单的常用属性
   	disabled、selected、checked属性都是布尔类型的属性，值是true或者false；其他表单元素的值和标签中的值都是一样的，值基本上都是字符串型，比如type、value、id等

5.标签的自定义属性
  setAttribute(name,value);name:属性名，value：属性值
  getAttribute(name);获取标签的属性(包括自定义属性和固有属性)
  removeAttribute(name);name：需要移除的属性名(包括自定义和固有属性)
  对于标签的自定义属性只能是这三个方法去设置、获取、和移除；

6.标签内容
  innerHTML：获取的是内容，还包括html标签；在设置标签内容的时候，会识别html标签
  innerText:获取的仅仅是内容，会丢弃html标签，在设置标签内容的时候，不识别html标签，会对标签进行转义

7.排他思想
  干掉所有人，留下我自己；

8.classList.remove('current');
  classList.add('current');

  children[0]:第一个孩子，children就是找子代，不包括孙子;
  nextsibling:下一个兄弟节点(这个可能会找到空格，换行，注释的一类节点)
  nextElementSibling:下一个兄弟元素(这个是直接找到兄弟标签)，有兼容问题
  previousSibling:上一个兄弟节点
  previousElementSibling:上一个兄弟元素，有兼容问题
  firstChild:第一个孩子节点
  firstElementChild:第一个孩子元素，有兼容问题
  lastChild：最后一个孩子节点
  lastElementChild：最后一个孩子元素，有兼容问题

9.style属性
  1. 标签有style属性，可以设置样式，对象也有对应的style属性。
  2. 这个style对象里面有很多很多的属性，这些属性都是我们可以写的样式。
  3. 设置的时候，如果获取的时候带了单位，设置的时候一定也要记得带单位。
  4. style如果获取的话，只能获取行内样式
  5. style通常不是用来获取样式的，而是用来设置样式的。
  var demo = document.getElementById("demo");
  console.log(demo.style.width);//获取
  demo.style.width = "400px";//设置

10.善于用flag去假设,善于保存原有的一些样式

11.设置不透明度
	style样式里设置如下(这两个必须一起设置，兼容)：
	opacity：0.5 ；
	filter：alpha(opacity=50);
	js中设置如下：
	element.style.opacity='0.5';
	element.style.filter='alpha(opacity=50)'

12.!--
        1. 设置不透明，一般要设置两次
        2. 设置位置，一定要有定位，不要忘了单位
        3. 设置层级，一定要有定位
    -->


	什么时候用style，什么时候用className

    1. 如果设置的样式比较少，style
    2. 如果一次要设置很多个样式，className
    3. 如果设置的这个值，一直在变化，用style

13.# 克隆节点

	语法：var newNode = node.cloneNode(deep)

	功能：在内存中克隆一份节点

	参数：deep

	* false：默认值：是浅复制，只会复制标签，节点本身，不会复制节点的孩子。
	* true:深度复制，会复制标签，还会复制标签的所有内容 ***常用*** 



	> 1. 克隆出来的节点跟原来的节点没有关系了，修改了也不会相互影响。
	> 2. 如果克隆的节点带了id，我们需要给id重新设置一个值，不让id冲突

14.# 添加节点

	## appendChild

	语法：parent.appendChild(newChild)

	parent:调用者，父节点来调用

	newChild:需要添加的那个孩子。

	作用：把newChild添加到parent的孩子的最后面。



	> 如果添加的是页面中本来就存在的元素，是一个剪切的效果，原来的就不在

15.## insertBefore

	语法：parent.insertBefore(newChild, refChild);

	parent:必须要父节点来调用

	newChild：需要添加的那个节点

	refChild:添加到哪一个节点的前面。



	```javascript
	var ul = document.getElementById("list");
	var li = document.createElement("li");
	li.innerHTML = "骥骥";
	//就是添加到子节点的最前面。
	ul.insertBefore(li, ul.children[0]);

16.## createElement:创建节点

	语法：var element = document.createElement("tagName");

	作用：在内存里面创建了一个节点

	返回：一个元素

	用途非常的广泛。

17.## 字符串的indexOf方法



	语法：var idx = str.indexOf(searchStr)

	功能：在str这个字符串里面搜索searchStr这个字符串第一次出现位置。



	> 如果没有找到，会返回-1



18.## 删除节点：removeChild(child)

	语法：parent.removeChild(child);

	功能：有父盒子调用，删除里面的一个子元素。


19.预解析
	javascript解析器执行js代码的时候，分为两个过程：

	1. 预解析过程
     * 判断代码有没有语法错误。如果有语法错误，直接就不执行了。
     * 把变量的声明提前到当前作用域的顶部。只会提升变量的声明，不会提升变量的赋值。（对所有的变量进行标识。方便挖坑。）
     * 把函数的声明提升到当前作用域的顶部，只提升函数的声明，不会提升函数的调用。
     * 先提升var，再提升function
	2. 代码执行过程，代码一行一行的往下执行。


20.全局变量和局部变量

	1. 全局变量：在script标签内，在函数外定义的变量就叫全局变量。***在哪儿都能访问得到*** 
	2. 局部变量，在函数内部定义的变量就叫局部变量。***局部变量只有在自己这个function内部才能访问到*** 
	3. ***特殊：如果没有使用var声明的变量，那么，这个变量是全局变量。（尽量不要使用）*** 



	# 全局作用域与函数作用域

	作用域：变量起作用的区域。

	全局作用域：在script标签内，在函数外的区域就叫全局作用域，在全局作用域内定义的变量就叫全局变量。

	函数作用域：在function内部的区域，就叫函数作用域，在函数作用域里面定义的变量就叫局部变量。





	当要使用某一个变量的时候，会先从自己的作用域里面去找这个变量，如果自己有的话，就用自己的。如果自己没有，就去全局里面找。



	## 在js里面没有局部作用域

	在js里面只有全局作用域和函数作用域

	只要不是在函数里面定义的变量，都是全局变量。


21.# 操作对象属性的两种方式
	第一种：.语法

	```javascript
	var obj= {
	  "name":"zs",
	  "age":18,
	  "sex":"不详"
	}

	console.log(obj.name);// 没有=，就是获取   意思：获取obj的name属性的值
	console.log(obj.score);//没有=，也是获取， 意思：获取obj的score属性的值，但是没有，所以是undefined。

	obj.name = "ls";//有=，就是设置，  意思：设置obj的name属性的值为ls，如果有这个属性，那么就会覆盖原来的值
	obj.score = "100";//有=，就是设置  意思：设置obj的score属性的值为100，没有这个属性，那么就添加了这么一个属性



	第二种语法：[]语法：关联数组的方式：把对象当成数组来看

	```javascript
	var obj= {
	  "name":"zs",
	  "age":18,
	  "sex":"不详"
	}
	obj["name"]; //获取obj的索引为name的值。
	obj["score"];//获取obj的索引为score的值，没有，索引会返回undefined

	obj["name"] = "ls";//设置name为ls


	//有一种情况，只能用[]语法
	//如果属性名或者说索引名存在一个变量中的时候，只能用[]方式
	var key = "name";
	obj[key];//只能用这种方式
	obj.key;//不能用这种方式，因为这个时候，用.语法找的不是变量，意思：obj的key属性。
	```