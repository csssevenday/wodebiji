###jq

+ on绑定事件  
+ 
  		  // 语法：
 
		$(selectorParent).on(events[,selector][,data],handler);
		$(selectorParent).on(events[,selector], handler);
		$(selector).on(events,handler);
		data: 给事件传参, 可以使用 event.data 来接收
		
		on 绑定样式 可以传obj	
		$(".box").on("click","div",obj,function(e){
				console.log(e.obj)
			})
        

         取对象的方法 e.data
		var obj = {
				name:"zhangsan"
			}
			$(".box").on("click","div",obj,function(e){
				console.log(e.data);
			})
+ off解绑

			// on 方式解绑
			/*$("button").click(function (){
				$(".box").off("click","div",fn);	
			})*/	

###	事件触发
			简单事件触发
				$(selector).click(); //触发 click事件
			trigger方法触发指定事件	


###jq对象
			$(".box").mousedown(function (e){
				console.log(this);
							// console.log(e);
				console.log(e.currentTarget);
			})输出结果相等  为<div class="box"></div>
			e.currentTarget == this  当前dom对象

+  e.target与e.currentTarget 区别
+  
			$("ul").click(function (e){
				console.log(e.currentTarget);	//谁绑定的事件,就指谁  //ul>li
				console.log(e.target);		// 当前的点击对象
			})

+	event.stopPropagation()；	阻止事件冒泡
+	event.preventDefault(); 	阻止默认行为
+	event.type 					事件类型：click，dbclick…
+   event.which 					鼠标的按键类型：左1 中2 右3
+   event.keyCode			aksm	键盘按键代码 enter为13

			$(".ipt").keydown(function (e){
			// console.log(e.keyCode);
			if(e.keyCode === 13){
				console.log($(".ipt").val()) //input里面输入的值
			}

###3种获取下标的方法
   
    //1使用 js 方法给 li 绑定事件 获取下标

 	var lis = docmentgetElementByTagName("li"); 
	for(var i = 0; i < lis.length ; i ++){
				lis[i].onclick = function (n){
					return function (){
						console.log(n);
					}
				}(i)
			} 

     //2  使用之前 jq 所学的方式获取下标

	 $("ul li").click(function (){
			var i = $(this).index();   //获取下标
			console.log("li[" + (i+1) + "]======>" + i);
		}) 

     //3  使用 jq 的 Each 方式获取下标

	$("li").each(function (index,element){
			
			$(element).click(function (){
				console.log($(element).text(),"========>" + index);
			})
	  })

####入口函数

			$(function(){
				console.log("jqery的入口函数3");
			})

###jq 选择器

		     jq 的选择器
					id #id  class .class   tagName  div
					* 通配符,选择页面上所有元素
					空格 后代选择器	$(".box p")
					, 并集选择器		$(".box,.inner")

####   >  子代选择器			选择所有的子代元素
####   +  紧邻选择器		    选择紧挨着的下一个元素 下一个兄弟节点  nextElementSibling
####   ~ 兄弟选择器		选择后面的所有的兄弟元素
####   ~ 后面可以不加元素,如果不加获取		后面所有的兄弟节点


##   jq的过滤选择器
+   :eq(index)		index是从0开始的一个数字，选择序号为index的元素。选择第一个匹配的元素。
+    :gt(index)		选择序号大于index的元素	(index,...]
+    :lt(index) 	选择小于index 的元素   [...,index)
+    :odd 	选择所有 下标为奇数 元素
+    :even 选择所有 下标为偶数 元素
+    :first  选择匹配第一个元素
+    :last 选择匹配最后一个元素

###jq的属性选择器
+  $(“a[href]”)   选择所有包含href属性的元素
+  $(“a[href=’baidu’]”)  选择href属性值为baidu的所有a标签
+  $(“a[href!=’baidu’]”)   选择所有href属性不等baidu的所有元素，包括没有href的元素
+  $(“a[href^=’web’]”)		选择所有以web开头的元素
+  $(“a[href$=’cn’]”)  选择所有以cn结尾的元素
+  $(“a[href*=’i’]”)  选择所有包含i这个字符的元素，可以是中英文
+  $(“a[href][title=’内容’]”)  选择所有符合指定属性规则的元素，都符合才会被选中。

##jq的筛选选择器

+ find(selector)		查找指定元素的所有后代元素（子子孙孙）
+ children()		查找指定元素的所有子元素（亲儿子元素）
+ siblings()		查找所有兄弟元素,必须能区分开（不包括自己）
+ parent()  查找父元素（亲的）

##jq事件
+ jq绑定方法 不需要on,而且click接受的参数为 函数类型
+  在jq的事件里,this指向绑定该事件的dom元素本身,不能执行jq的方法 错误:this.css("width","400px")
 
			$('.d1').click(function () {
				console.log(this); // this 是 dom 对象
				// $(this) 是jq对象
				$(this).css("width","400px");
				this.css("height","400px");
			})

###jq对象与dom对象的转换
+	       jquery	对象	     jqBox = $(".box")
+	       jq 转 dom 对象     var box1 = jqBox[0];
+       dom转jq对象       var jqBox = $(box1)    box1 == box;
   
###jq设置属性 box.style.width   box.setAttribute("style","width:400px")

###jqCss

		.css()
				获取样式  .css("样式名")
				设置单个样式		.css("样式名","样式值");
				设置多个样式  参数为json对象或者对象形式
				.css({
					样式名: 样式值,
					样式名: 样式值,
					...
				})

###jq属性操作
+ 相当于js中的getAttribute()
 
				.attr()
					获取属性		.attr("属性名")		// 行内样式
					设置属性
				
						设置单个属性:
							.attr("属性名","属性值")
							
						设置多个属性:
							.attr({
								"属性名": "属性值",
								"属性名": "属性值"
								...
							})
							
					删除某一属性	removeAttr(属性名)
+ 例子

		var bgc = $(".box.d1").attr("class");
			$(".box").attr("style","background-color: orange");
			$(".box").attr({
				style: "background-color: green",
				class: "box d1 d2"
			})
			console.log(bgc);
			$(".box").removeAttr("class");

###html() 与 text()
+  与js中的innerText/innerHTML/value
+ 没有参数是取值，传入参数是设置值
+ 
					text()
					html()
					val()
+  例子

			var t = $(".box").text();
			console.log(t);
			$(".box").text("hello world");
			var h = $(".inner").html();
			console.log(h);		//text() 不凡学院		html()  <span>不凡学院</span>
			// $(".inner")[0].innerHTML = "<p style=\"color: red\">hello world</p>";
			$(".inner").html("<p style=\"color: red\">hello world</p>");
			
			var v = $(".ipt").val();
			console.log(v);
			$(".ipt").val("hello world");

##jq操作类名

		addClass() - 向被选元素添加一个或多个类
		removeClass() - 从被选元素删除一个或多个类
		toggleClass() - 对被选元素进行添加/删除类的切换操作  没有添加;存在删除
		hasClass()- 判断是否存在类
+  例子

			$("button:eq(0)").click(function (){
				$(".box").addClass("d1 d2 d3");
			})   //class = box d1 d2 d3 
			
			$("button:eq(1)").click(function (){
				$(".box").removeClass("d1 d2");
			})     //class = box  d3 
			
			$("button:eq(2)").click(function (){
				$(".box").toggleClass("d3");
			})    //有d3删掉d3  没有 加d3
			
			$("button:eq(3)").click(function (){
				$(".box").hasClass("d3");
				if($(".box").hasClass("d3")){
					alert("有")      //判断有没有d3
				}else{
					alert("没")
				}
			})


###jq DOM查找

		 	
				siblings()  除了自己以外的所有的兄弟节点
				next()	下一个兄弟
				nextAll()		后面所有的兄弟
				nextUntil()	后面所有的兄弟直到…			ele.nextUntil(nextEle) (ele,nextEle)
				
			
				prev()	前面的兄弟
				prevAll()		前面所有的兄弟
				prevUntil()		…
				parent()		
				parents()		所有的父节点
				parentsUntil()
			
###jq动画

		hide方法			$(xx).hide(time,callback)
					作用：让匹配元素隐藏掉
					time: 运动的时间   可以是自己设的毫秒数, 也可以是 slow：600ms、normal：400ms、fast：200ms
					省略 time 则使用默认值：400毫秒
					callback: 回调函数,当元素隐藏后执行
		show方法			$(xx).show(time,callback)
					作用：让匹配的元素展示出来
					参数同上

		滑入滑出动画  向上向下滑
					1 滑入动画效果
						$(xx).slideDown(speed,callback);
							speed: 省略参数或者传入不合法的字符串，那么则使用默认值：400毫秒
					
					2 滑出动画
						$(xx).slideUp();
					
					3	滑入滑出切换动画效果
						$(xx).slideToggle(speed,callback);

		淡入淡出动画  
					1 淡入动画效果
							$(xx).fadeIn(speed, callback);

					2 淡出动画效果
							$(xx).fadeOut(1000);

					3淡入淡出切换动画效果
							$(xx).fadeToggle('fast',function(){});

		改变透明度到某个值
				作用：调节匹配元素的不透明度 
					$(xx).fadeTo(1000, .5); //  0全透，1全不透

+ 自定义动画

	注意: 所有能够执行动画的属性必须只有一个数字类型的值。
				语法：$(selector).animate(styles,speed,easing,callback)
					第一个参数表示：要执行动画的CSS属性（必选）{width: 200,height: 200}
					第二个参数表示：执行动画时长（可选）
					第三个参数表示: 执行动画运动的贝塞尔曲线(可选)		内置：swing/linear
					第四个参数表示：动画执行完后立即执行的回调函数（可选）
     
	动画可以  连写  会按顺序执行 
 
	停止动画
				1.stop()
					作用：停止当前正在执行的动画
					为什么要停止动画？如果多个动画同时作用于一个单位上面，那么多个动画会进入排队。后一个动画的执行必须等前面的执行完毕。
				2.stop(stopAll,goToEnd);
					stopAll  停止队列中所有的动画.	是否全部停止，默认false 
					goToEnd  是否将停止的动画  停止在当前动画的最后一个状态 默认false

###jq节点操作

		1.创建元素
			// 可以把字符串转变为一个jq对象
			// js  var p = document.creatElement("p");p.style.xx = xx;p.innerText = "xxx";
       例子
			var $p = $("<p>hello world</p>");
			console.log($p);
		
		        //js中 appendChild()  insertBefore()
			
				添加元素
				1 在元素的最后一个子元素后面追加元素：
				append()   
					参数 $node(jq对象)   或   标签字符串
					作用：在被选元素内部的最后一个子元素（或内容）后面插入内容（存在或者创建出来的元素都可以）
					如果是页面中存在的元素，那么调用append()后，会把这个元素放到相应的目标元素里面去；但是，原来的这个元素，就不存在了。
					如果是给多个目标追加元素，那么方法的内部会复制多份这个元素，然后追加到多个目标里面去。
				appendTo()
					作用：把$(selector)追加到node中去	
					$(selector).appendTo(node);
         例子

				$(".box").append($p);
				$(".box1").append($p);

+ 
			prepend()
					作用：在元素的第一个子元素前面追加内容或节点
					$(selector).prepend(node);
					====================区分=====================
				after()
					作用：在被选元素之后，作为兄弟元素插入内容或节点
					$(selector).after(node);		将node插入到selector 之后

				before()
					作用：在被选元素之前，作为兄弟元素插入内容或节点
					$(selector).before(node);  将node插入到selector之前

+  清空元素
				$(selector).empty();
				$(selector).html(“”);
				$(selector).remove();  //会把对象也干掉
			
			// $(".box1").empty();
			// $(".box1").html("");
			$(".box1").remove();
			
			
			$(".box").append($p);
			// 复制元素		$(selector).clone();  深度克隆
			$(".box").append($(".box").clone());

####      // $("input[type='checkbox']").prop("checked");
			//用于遍历 form表单中的多选框和单选框的选中状态
			$('.btn1').click(function()  {
				alert($('.like').prop('checked'));
				alert($('.sex').prop('checked'));
			})

##jq事件绑定

		    $(".box").on("click",function (){
				console.log("添加到 box 自身的事件");
			})

+  事件解绑

			on 方式解绑
			$("button").click(function (){
				$(".box").off("click","div",fn);	
			})

###事件触发

   			$(".box").click(function (){
				console.log("box 被点击了 ...");
			})

			$(".content").click(function (){
				console.log("box 的父类的点击事件被触发了 ...");
			})

###  jq事件对象介绍  e.tagete

			$("ul").click(function (e){
				//console.log(e.currentTarget);		// 谁绑定的事件,就指谁
				console.log(e.target);		// 当前的点击对象
			})