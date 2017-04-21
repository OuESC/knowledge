*********************************************   AJAX   *******************************************************

## 1、通俗的讲，能够提供某种服务的机器（计算机）称为服务器

## 2、按照不同的划分标准，服务可划分为以下类型：
		1、按服务类型可分为：文件服务器、数据库服务器、邮件服务器、Web 服务器等；
		2、按操作系统可分为：Linux服务器、Windows服务器等；
		3、按应用软件可分为 Apache服务器、Nginx 服务器、IIS服务器、Tomcat服务器、Node服务器等。


## 3、C/S结构：
		C:client 客户端  用户必须在电脑上安装对应的客户端软件  QQ  迅雷  快播
		S:server 服务器

		优点：用户体验比较好
		缺点： 需要下载 更新， 占用空间

		B/S结构：
		B:Browser 浏览器  用户不需要安装任何客户端软件，只需电脑有浏览器即可
		S:服务器

		优点：不需要安装任何客户端 
		确定： 用户体验 没有c/s好


## 4、网络基础
		ip： 在互联网中 没台电脑的身份证号
			缺点：没有意义 不方便记忆
		域名：
			解决ip地址 难以记忆的问题
			www.baidu.com
			www.jd.com

		DNS:记录了 ip和域名的对应关系
		
		本机的host文件中也记录有ip和域名的对应关系，在浏览器中输入域名是 会优先查找本地的host文件，如果拿到ip 就直接访问服务器， 如果host文件中没有记录，则再去查找dns服务器，拿到ip,在访问服务器
		C:\Windows\System32\drivers\etc\hosts		
		
		端口： 定位到程序


## 5、服务器配置：
		httpd.conf
		 1、设置  根目录
		 	doumentRoot   2个地方  178  205  
		 2、 2个权限 
		 	 #deny  from all 
		 	  allow from all 
		 3、 释放了虚拟主动的 注释   vhost  

	    httpd-vhosts:
	    	复制 虚拟主机的配置 格式
	    	修改了 documetroot  根目录
	    	域名    别名 

	    	    DocumentRoot "e:/www/test/"
			    ServerName  test.com
			    ServerAlias www.test.com   

	    hosts文件:
	    	绑定ip域名的关系
	    	127.0.0.1   www.study.com
	    	127.0.0.1    study.com  
## 6、基本语法
		window  + apache +mysql + php

		php 是一个后台的编程语言：需要编译才能执行 


		基本语法：
		<?php   ?>

		echo 向客户端输出信息

		变量：
		 1、变量以$开头 字母/数字/下划线 不能以数字开头
		 2、大小写敏感（区分大小写）

		 echo 用于输出简单的数据类型
		 print_r() 用于输出复杂的数据类型
		 var_dump() 用于输出数据的详细信息


		遍历关联数组的语法格式：
		 foreach ($variable as $key => $value) {
			# code...
		}

  ## 7、 表单处理
	   	name 属性的是用来提供给服务端接收所传递数据而设置的
		action属性设置接收数据的处理程序
		method属性设置发送数据的方式 get post 

		当上传文件是需要设置 enctype="multipart/form-data"，且只能post方式
		$_GET接收 get 传值
		$_POST接收 post 传值
		$_FILES接收文件上传


		get请求：从服务器上请求数据，在地址栏后面拼接的方式传递数据，只能传输文本，大小有限制4kb 
				 执行效率比post好，如果是做数据查询就用get方法。
		post请求：发送数据到服务器，大小没有限制，相对安全。如果是做数据添加、修改、删除，建议用post
		GET和POST请求方式的区别：
			1、GET没有请求主体  xhr.send(null)
			2、GET可以通过在请求URL上添加请求参数  
			3、POST可以通过请求主体发送数据     xhr.send('name=itcast&age=10')
			4、POST需要设置请头部    Content-Type:application/x-www-form-urlencoded
			5、GET效率更好（应用多）
			6、GET大小限制约4K，POST则没有限制

 ##	php常用方法：
		in_array() 是否在数组中
		count() 计算数组长度
		array_key_exists ()检测数组中是否存在key
		file_get_contents读取文件
		move_uploaded_file(要移动的文件，移动的地方) 两个参数 移动上传的文件


 ##	http协议：
   		即超文本传输协议，网站是基于HTTP协议的，
   		例如网站的图片、CSS、JS等都是基于HTTP协议进行传输的。
   		HTTP协议是由从客户机到服务器的请求(Request)和从服务器到客户机的响应(Response)进行了约束和规范

   		1xx：指示信息--表示请求已接收，
   		继续处理
		2xx：成功
		3xx：重定向--要完成请求必须进行更进一步的操作
		4xx：客户端错误
		5xx：服务器端错误

		常见的有200代表成功、304文档未修改、403没有权限、404未找到


 ## ajax:
   		Ajax 特点: 可以在不刷新页面的情况下，更新网页的局部数据;
   		本质上是在http协议的基础上以异步的方式与服务器进行通信
		ajax是利用js中内置的XMLHttpRequest对象和服务器通信

 		Asynchronous  Javascript  And  XML
 		AJAX 是一门的新的语言，而是对现 有持术 的 综合利用。
 		异步： 
 		执行的属顺序和书写顺序无关 其优势在 于不阻塞程 序的执行， 从而提升 整体 执行 效率。

 		var xhr = new XMLHttpRequest() ;
 		xhr.open() 发起请求，可以是get、post方式
		xhr.setRequestHeader() 设置请求头
		xhr.send() 发送请求主体get方式使用xhr.send(null)
		xhr.onreadystatechange = function () {} 监听响应状态
		
		xhr.status=200 响应状态码  成功 ok
		xhr.readyState = 4时，DONE 响应完成

		xhr.responseText : 响应结果；

		xhr.readyState = 0时，UNSENT open尚未调用
		xhr.readyState = 1时，OPENED open已调用
		xhr.readyState = 2时，HEADERS_RECEIVED 接收到头信息
		xhr.readyState = 3时，LOADING 接收到响应主体
		xhr.readyState = 4时，DONE 响应完成


		//设置超时
		xhr.timeout=3000;
		//超时监听事件
		xhr.ontimeout = function(){
			alert('网络超时，请重试')；
		}


		11.2FormData
			a) 提供了一个新的内建对象，可用于管理表单数据 
			b) 首先要获取一个表单元素form
			c) 然后在实例化时 new FormData(form)，将表单元素form传进去
			d) 会返回一个对象，此对象可以直接做为xhr.send(formData)的参数
			e) 此时我们的数据就是以二进制形式传递了
			f) 注意我们这里只能以post形式传递，浏览器会自动为我们设置一个合适的请求头

		11.3二进制
			a) 我们上传文件是以二进制形式传递的
			b) 我们可以通过表单<input type=”file”>获取到一个文件对象
			c) 然后file.files[0]可以获取文件信息
			d) 然后再利用var formData = new FormData() 实例化
			e) 然后再利用formData.append(‘upload’, file.files[0])将文件转成二进制
			f) 最后将 formData 做为xhr.send(formData)的参数

		实例：
		<script>
    	//点击按钮 获取表单数据 异步提交到服务器

    		document.querySelector('[type=button]').onclick=function(){

    			var formData=new FormData();

    			var file=document.querySelector('[type=file]');

    			formData.append('name','zs');
    			formData.append('pwd','123456');
    			formData.append('file',file.files[0]);

    			var xhr=new XMLHttpRequest();

    			xhr.open('post','02-formData.php');

    			xhr.send(formData);

    			xhr.onreadystatechange=function(){
    				if(xhr.readyState==4&&xhr.status==200){
    					console.log(xhr.responseText);

    					var html='<img src="'+xhr.responseText+'"/>';
    					document.querySelector('.info').innerHTML=html;
    				}
    			}
    		}
    	</script>


		11.4上传进度
			a) 利用XMLHttpRequest我们可以实现文件的上传
			b) 并且我们可以通过xhr.upload.onprogress = function (ev) {// code}，监听上传的进度
			c) 这时我们上传的进度信息会保存在事件对象ev里
			d) ev.loaded 表示已上传的大小，ev.total表示文件整体的大小
			e) var percent = ev.loaded / ev.total

		实例：<script>
    	//点击按钮 获取表单数据 异步提交到服务器

    		document.querySelector('[type=button]').onclick=function(){

    			var formData=new FormData();

    			var file=document.querySelector('[type=file]');
   			
    			formData.append('file',file.files[0]);

    			var xhr=new XMLHttpRequest();

    			xhr.open('post','02-formData.php');

    			xhr.upload.onprogress=function(e){

    				var value=(e.loaded/e.total)*100+'%';

    				document.querySelector('.curr-progress').style.width=value;

    			}

    			xhr.send(formData);


    			xhr.onreadystatechange=function(){
    				if(xhr.readyState==4&&xhr.status==200){
    					console.log(xhr.responseText);
    					
    				}
    			}

    		}
    	</script>



    	// 兼容写法
		//  兼容ie5 ie6的写法 
		
		var  xhr=null;
		if(XMLHttpRequest){
			xhr=new XMLHttpRequest();
		}else{
			xhr=new ActiveXObject("Microsoft.XMLHTTP");
		}




 ##	xml 与 html 的区别
	xml在php的页面中第一行必须写上：<?xml version = '1.0' encoding = 'utf-8' ?> 必须是第一行
	xml就是把代码都放到页面上，必须有一个根目录，下面是一小块一小块的方式
	相同点：都是使用标签，都是描述性语言 ；注释一样
	不同点：html用于展示数据：超文本标记语言 ；
			xml用于存储和传输数据：可拓展标记语言


	示例：<root>
			<item>
				<name type="star">王力宏</name>
				<photo>./images/wlh.jpg</photo>
				<album>&lt;&lt;改变自已&gt;&gt;</album>
				<age>39</age>
				<sex>男</sex>		
			</item>
			<item>
				<name type="star">周杰伦</name>
				<photo>./images/wlh.jpg</photo>
				<album>&lt;&lt;我很忙&gt;&gt;</album>
				<age>39</age>
				<sex>男</sex>		
			</item>
		  </root>

  	客户端想拿到xml的数据，需要告诉客户端返回的是xml格式的数据：header('content-type:text/xml ;charset : utf-8')
  	读取数据：file_get_contents('star.xml') ;  file_get_contents() ;


  	json格式的数据写法：必须是双引号，单引号没用:很多对象的时候要用数组包裹，但是一个的时候就直接{}就可以了
  	[ {
		"name" : "兰兰" ,
		"age" : 18 ,
		"sex" : "男",
		"album" : "<<自我修养>>"
	},
	{
		"name" : "荣荣" ,
		"age" : 20 ,
		"sex" : "女" 
	} ]

	//json格式的字符串
		var str = '{"name":"zs","age":18,"sex":"男"}' ;



	//js的两个转换方法：JSON.parse();JSON.stringify();这里的JSON是要大写的
	JSON.parse() ;  把json格式的字符串转换成js的对象
	JSON.stringify() ; 把js的对象转化为json格式的字符串

	示例：//json格式的字符串
			var str = '{"name":"zs" ,"age":18 , "sex": "男"}' ;

			//把json格式的字符串转换成js的对象
			str = JSON.parse(str) ;
			console.log(str) ;//输出的是一个对象：Object {name: "zs", age: 18, sex: "男"}
			console.log(str.name) ;//输出的是zs


			//下面是js对象
			var obj = {
				"name" : "zs" ,
				"age" : 18 ,
				"sex" : "男"
			}
			//把js对象转换为json格式的字符串
			obj = JSON.stringify(obj) ;
			console.log(obj) ;//{"name":"zs","age":18,"sex":"男"}
			console.log(typeof(obj)) ;//string类型


	//php的两个转换方法：json_decode(); json_encode();
	json_decode(); 把json的字符串转换成php的对象 ；
	json_encode(); 把php的对象、关联、数组转换为json的字符串

	示例：// json格式的字符串
			$str = '{"name":"zs","age":18,"sex":"男"}';

			//把json格式的字符串转换成php的对象
			$str = json_decode($str) ;
			//判断类型
			// echo gettype($str);

			//obj.name    obj.sex
			
			// var_dump($str);

			// echo $str->name;

			// echo $str->age;


			//php的对象，关联，数组 转成json格式的字符串
			$arr = array(
					"name"=>"zs",
					"age"=>18,
					"sex"=>"男"
				);
			$arr = json_encode($arr) ;

			echo gettype($arr) ;//输出string类型
			
			echo $arr ;//输出json格式的字符串：{"name":"zs","age":18,"sex":"\u7537"}

			//把json格式的字符串转换成php对象
			$info = json_decode($info) ;
			//访问php对象的属性就是用->符号
			echo $info->age;

	json是js与php语言之间的桥梁，语言之间不能相互访问，但是可以通过转化为json字符串，两者之间使用各自的两种方法
	可以相互访问


	//eval()函数可以计算某个字符串，并执行其中的js代码
		str = '{"name":"zs","age":18,"sex":"男"}'
		//也可以把json格式的字符串转换成js对象
		str = eval('('+str+')') ;
		console.log(str.name) ;


	//array_rand($messages) 随机返回数组的一个下标
	//array_rand($messages): 返回的只是数组的一个下标，想要取值还是要$messages[array_rand($messages)] ;
	sleep(1.5);
	
	echo   $messages[array_rand($messages)];


## jquery的ajax语法中 都是必须要引入jquery包的

		jquery中的ajax写法格式
		$.ajax({
			"type" : "get" ,
			"url" : "get.php" ,
			"data" : {'name':'zss','age':18},
			success: function(info) {
				console.log(info) ;
			}
		})

		//也可以单独写
		$.get('get.php',{"name":"zs","age":18},function(info){
						console.log(info) ;
					});

		$.post("post.php",{"name":"zs","age":18},function(info){
						console.log(info) ;
					}) ;

		//JQAjax中getJAON的方法获取json文件
		$.getJSON('star.json',{"name":"zs","age":18},function(info){
			console.log(info);//获取的是json里面包含多个对象的数组
		});

		// 可以动态向页面中引入js文件
		$.getScript("test.js",function(){
						song() ;
					});

		//test.js中的代码如下
		function song() {
			alert("今天天气真好！") ;
		}

		//jquery中加载文档的语法：load() ;
		$('div').load('template.html');
		//template中的代码
		<h1>总有刁民想朕！</h1>
		<p>苍茫的天涯我的爱....</p>
		<p>苍茫的天涯我的爱....</p>
		<p>苍茫的天涯我的爱....</p>

		$.ajax({
			"type":"get",
			"url":"star.php",
			"data":null,
			"dataType":"json",//客户端希望接收到数据类型
								//如果设置为json ，$.ajax返回会自动把接收到的json字符串转成js对象或和数组
			"timeout":1000,
			beforeSend:function(){
				alert(1);
			},
			success:function(info){
				console.log(info) ;//拿到服务器返回的数组
				//定义一个空的字符串变量，然后遍历拿到的数组
				var html = '' ;
				for(var i = 0 ; i < info.length ; i ++) {
					//把数组的结果拼接成表格
					html += "<tr>" ;
					html += "<td>"+info[i].name+"</td>";
					html += "<td>"+info[i].age+"</td>";
					html += "<td>"+info[i].sex+"</td>";
					html += "<td>"+info[i].photo+"</td>";
					html += "<td>"+info[i].album+"</td>";
					html += "</tr>" ;
				}
				//把拼接的表格数据放到页面中的table里
				//  html() 方法设置或返回被选元素的内容（innerHTML）。
				$('table').html(html) ;
			},
			error:function(error) {
				console.log(error) ;
			},
			complete:function(){
				alert(2);
			}

		//表单序列化方法：serialize(); 直接转化成例如：name=zs&pass=123123&repass=123123 ；

## 模板引擎的使用
		<!-- //模版引擎的使用：
					// 1、引入模版引擎的插件
					// 2、准备好模版 
					// 3、准备数据
					// 4、把数据和模版 进行组装，生成需要渲染的结构

					//注意： 传给模版的数据必须是一对象，
					//		在模版中直接使用对象的属性，不用写对象名
		 -->


		<!-- 使用模板引擎可以不要字符串拼接的麻烦了，工作之后较多使用模板引擎 -->

		 <!-- <% %>:模板的逻辑表达式语法 -->
		 <!-- <%= %>:模板的输出变量的值 -->

		 实例：	 
		 <!-- 准备模板 -->
			<script type = "text/template" id = "tmp">
			//在模板中直接使用对象的属性，不用写对象名
				<h1><%= title %></h1>
				<ul>
					<% for(var i = 0 ; i < list.length ; i ++){ %>
						<li><%= list[i]%></li>
					<% } %>
				</ul>

			</script>

			<!-- 引入模板的插件 -->
			<script src = "js/template-native.js"></script>	
			<script>
			//准备数据
				var data = {
					"title" : "标签" ,
					"list" : ['文艺', '博客', '摄影', '电影', '民谣', '旅行', '吉他']
				};

				//把数据和模板进行组装
				var html  = template("tmp",data) ;
				console.log(html) ;
				//追加到body页面
				document.body.innerHTML = html ;
			</script>


			//实例二
			<!-- 准备模板 -->
			<script type = "text/template" id = "tmp">
			<!-- 说明传递的对象里面必须有一个list属性 -->
				<% for(var i = 0 ; i < list.length ; i ++) { %>
					<tr>
						<td><%= list[i].name %></td>
						<td><%= list[i].age %></td>
						<td><%= list[i].sex %></td>
						<td><%= list[i].photo %></td>
						<td><%= list[i].album %></td>
					</tr>
				<% } %>
			</script>
			<script src = "../../js/jquery.min.js"></script>
			<script src = "../../js/template-native.js"></script>
			<script>
				$(function(){
					//点击按钮，
					$('button').click(function(){
						//通过JQajax发送请求
						$.ajax({
							"type":"get",
							"url":"star.php",
							"data":null ,
							"dataType":"json",
							success:function(info) {
								console.log(info) ;//接受返回来的数据:包含多个对象的数组
								//把上面模板和数据组装
								//由于要传递 的数据是对象，并且此时对象要求有一个list属性
								var data = {list:info} ;
								var html = template("tmp",data) ;
								console.log(html) ;
								//追加到table中，显示在页面
								$('table').append(html) ;

								
							}
						});
					})
				})
			</script>


## //封装jquery插件
		本质上就是给 $.fn 添加方法
		//1.封装一个颜色的方法如下
		$.fn.setColor = function(color) {
			$(this).css('background',color);	
		}
		$('div').setColor('red') ;


		//2.$.extend();方法
			var obj = {
				name : 'congcong' ,
				age : 18 ,
				hobby : '看片'
			}
			var obj1 = {
				name : 'feifei' ,
				sex : '弯'
			}
			//把obj和obj1合并成一个对象，有则覆盖，无则添加
			var obj2 = $.extend(obj,obj1) ;
			console.log(obj2);


			实例二：
				//option是对象 要求用户传递用户名
				function setName(option) {
					var defaults = {name:'zs'};
					defaults = $.extend(defaults,option);
					console.log(defaults.name);
				}
				setName();


## ajax的跨域请求
		<!-- 同源就是域名、协议、端口都是完全相同的 -->
		//跨域就是域名、协议、端口不一样！
		跨域不可以进行ajax请求和dom操作

		//如何实现跨域访问
			<!-- www.study.com 当前页面的域名 -->

		<!-- 需求：从当前页面的域名访问api.study.com域名的页面： -->
		<!-- 1.先使用框架标签的src属性引入另个域名的地址 -->
		<!-- 2.再通过给两个域名里的文件设置同一个顶级域名实现跨域访问 -->
		document.domain = "study.com" ;//这句代码是在两个域名的文件里的script标签里面都必须要有的


		<!-- 在跨域的情况下，不可以进行ajax请求，不能是XMLHttpRequest对象进行异步请求
		不能进行ajax请求
		不能进行dom操作 -->

		<!-- 但是跨域可以进行以下操作
		src href属性 具备跨域请求资源的能力 -->

		src/href属性具备跨域请求资源的能力，不必要有任何辅助
		实例：<!-- 其实就是图片的src属性 -->
		<img src="http://www.itcast.cn/images/slidead/BEIJING/2017280914284800.jpg" alt="">

		<!-- link的src引入属性 -->
		<link rel="stylesheet" href="http://api.study.com/02css.css">

		<!-- link也可以引入php文件 -->
		<link rel="stylesheet" href="http://api.study.com/04setColor.php">

		<!-- 可以使用script标签的src属性 -->
		<!-- 可以弹出提示框 -->
		<script src = "http://api.study.com/03js.js"></script>

		<!-- 获取到资源之后再地址后面直接拼接设置的属性和值 -->
		<link rel="stylesheet" href="http://api.study.com/05getColor.php?color=blue">
		<p>你好</p>

		<!-- link的回调:在引入路径src里面直接拼接数据 -->
		api 域名里面的代码
		<?php 
			header('content-type:text/js;charset:utf-8') ;

			$callback = $_GET['callback'] ;

			echo $callback.'()' ;//这里是回调函数拼接后面的括号
		?>

		study域名里面的代码
		<script>
			function say() {
				alert("哈哈") ;
			}
		</script>

		<script src = "http://api.study.com/06getFunction.php?callback=say"></script>


		<!-- jsonp的原理：动态创建script标签；本质：回调函数与数据，数据就是json数据；
		1.调用$.ajax方法是：如果dataType:jsonp 此时方法不会创建XMLHttpRequest对象，而是 动态生成一个script标签，会把url赋值给script标签的src属性，会把传递的数据用name=zs&age=18拼接在url的后面，还会动态创建一个方法，并且把方法名传递给后台（callback）;

		2.请求到了服务器之后，首先会$_GET['callback']获取函数名，把数据以参数的形式拼接在函数的调用中，并返回这个函数调用；

		3.请求完成之后，自动删除创建的script标签 -->


		ajax的优缺点
			优点：1.不刷新整个页面的情况下，局部刷新页面，有利于用户体验
				  2.异步请求数据，与服务器通信，更加迅速的响应能力
				  3.减轻服务器和带宽的负担
				  4.界面与应用分离，有利于分工合作，提高效率

			缺点：1.ajax干掉了back和history功能，即对浏览器机制的破坏
				  2.ajax的安全问题：因为ajax会有跨域请求，引入其他域名的内容，如果有js脚本的恶意代码攻击，会有安全隐患
				  3.不利于网站的SEO优化：因为搜索引擎的爬虫搜索会屏蔽所有的js文件，而ajax的页面基本上都是js去完成，所						以搜索引擎会把ajax当成透明的，所以并不利于seo优化
				  4.ajax并不能很好的适用于手机移动端？


	  	ajax跨域的实现
	  		1.给不同域名的页面的script标签中设置统一的顶级域名
	  		2.jsonp实现跨域
	  		3.php服务端设置 header( 'Access-Control-Allow-Origin:*' );
	     					header( 'Access-Control-Allow-Origin:http://www.test.com' );
			4.反向代理
			