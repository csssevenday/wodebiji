###	边框图片

+   border-image 属性是一个简写属性，用于设置以下属性：
+	border-image-source  图片
+	border-image-slice	图片边框向内偏移量
+	border-image-width	边框宽度(不写默认边框宽度)
+	border-image-outset  边框图像区域超出边框的量(默认 0 ,每次移动 1*border 的宽的  	距离)
+   border-image-repeat   图像边框是否应平铺(repeat)、铺满(round)或拉伸(	stretch)。
		
		会使边框原本的颜色失效

###线性渐变       linear-gradient

+   线性渐变（Linear Gradients）- 向下/向上/向左/向右/对角方向
+	语法：background: linear-gradient(direction, color-stop1, color-  	stop2, ...);
		background: -webkit-linear-gradient(bottom, red , purple);	
+	direction: 方向 可以使 角度(10deg)顺时针  也可以是 to top/left/right/bottom
			
+   颜色后面可以跟百分比,表示从百分几开始渐变
			
+   重复渐变: background: repeating-linear-gradient(to right, red 10%, green 	20%)
			也可以只写颜色background: orangered;
+   一般是通过ui设计稿 直接提取的渐变 角度 颜色比重

###径向渐变  radial-gradient   -webkit  为了兼容谷歌

+   radial-gradient径向渐变指从一个中心点开始沿着四周产生渐变效果
+	语法：background: radial-gradient(center, shape size, start-				          	color, ..., last-color);
		 background: radial-gradient(10% 20%,yellow,red,green);
	     background: -webkit-radial-gradient(10% 20%,yellow,red,green);
	     border-radius: 50%;
	     -webkit-border-radius: 50%;
+ shape size:参考 http://www.runoob.com/try/try.php?filename=trycss3_gradient-radial_size

###transparent 不可调节透明度，始终完全透明

###  1、结构伪类。
+		重点通过E来确定元素的父元素。
+		E:first-child第一个子元素
+	 	E:last-child最后一个子元素
+		E:nth-child(n) 第n个子元素
+		E:nth-last-child(n) 同E:nth-child(n) 相似，只是倒着计算；

###  E::before、E::after

>E::first-letter文本的第一个字母或字；
>案例：首字下沉
>E::first-line 文本第一行；  文本第一行高亮..
>E::selection 可改变选中文本的样式；

### 文本 (shadow阴影)

>text-shadow，可分别设置偏移量、模糊度、颜色（可设透明度）。
>1、水平偏移量 正值向右 负值向左；
>2、垂直偏移量 正值向下 负值向上；
>3、模糊度是不能为负值；

+ 可以有多个影子，用逗号隔开       浮雕文字.   bgc gray

###阴影 (box-shadow)
+	box-shadow: 1px 1px 5px rgba(0,0,0,.7);
>box-shadow: h-shadow v-shadow blur spread color inset;
>blur： 模糊半径
>spread:  扩展范围
>color: 颜色

### CSS3中可以通过box-sizing 来指定盒模型，即可指定为content-box、border-box，这样我们计算盒子大小的方式就发生了改变。
+ box-sizing 有两个值:content-box  border-box
+ 可以分成两种情况：
+  1    content-box:对象的实际宽度等于设置的width值和border、padding之和
+  2     border-box： 对象的实际宽度就等于设置的width值，即使定义有border和padding也不会改变对象的实际宽度，即 ( Element width = width ) 
     我们把这种方式叫做css3盒模型

###

+  cover会自动调整缩放比例，保证图片始终填充满背景区域，如有溢出部分则会被隐藏。
+  contain会自动调整缩放比例，保证图片始终完整显示在背景区域。

	Background:url  repeat  position
			background-image
			background-size 			设置背景图片的尺寸
					width height 直接设置宽高 百分比
					cover  会自动调整缩放比例，保证图片始终填充满背景区域，如有溢出部分则会被隐藏。
					contain  会自动调整缩放比例，保证图片始终完整显示在背景区域,可能会有留白。

			background-origin  (原点，起点)设置背景定位的原点
					border-box 		以边框做为参考原点；
					padding-box 	以内边距做为参考原点；
					content-box 	以内容区做为参考点；

			background-clip 	设置背景区域clip(裁切)
					border-box    裁切边框以内为背景区域；
					padding-box   裁切内边距以内为背景区域；
					content-box   裁切内容区做为背景区域；


###   过渡 
		transition: transition-property transition-duration transition-timing-function transition-delay
		transition-property   规定应用过渡的 CSS 属性的名称 (一般都写 all);
		transition-duration   定义过渡效果花费的时间。默认是 0
		transition-timing-function: 规定过渡效果的时间曲线。默认是 "ease"。
					linear|ease|ease-in|ease-out|ease-in-out|cubic-
		bezier(n,n,n,n);
		transition-delay 			规定过渡效果何时开始。默认是 0。
		

###  document.querySelector单个      document.querySelectorAll全部

 			var bgSize = document.querySelector(".bgSize");
			var bgOrigin = document.querySelector(".bgOrigin");
			var box = document.querySelectorAll("select")[0];
			console.log(box);



###    transform:          旋转
		缩放 scale(x, y) 可以对元素进行水平和垂直方向的缩放，x、y的取值可为小数，不可为负值；
				一个值表示 x/y 都缩放
		移动 translate(x, y) 可以改变元素的位置，x、y可为负值   一个值表示x
		旋转 rotate(deg) 可以对元素进行旋转，正值为顺时针，负值为逆时针

		transform-origin  旋转点    
		transform-origin:  left top;  左上   centent bottom  下中心

				/* transform: scale(2); */   放大2被
				/* transform: translate(200px,200px); */  移动
				transform: rotate(360deg);    旋转角度
		 -->

###		transition  过渡  移动
	transition: transition-property transition-duration transition-timing-function transition-delay
		transition-property   规定应用过渡的 CSS 属性的名称 (一般都写 all);
		transition-duration   定义过渡效果花费的时间。默认是 0
		transition-timing-function: 规定过渡效果的时间曲线。默认是 "ease"。
					linear|ease|ease-in|ease-out|ease-in-out|cubic-
		bezier(n,n,n,n);
		transition-delay 			规定过渡效果何时开始。默认是 0。

###拼接问题

			<span style="background-color: '+des[i].color +' "><span>
				
			var str = "<ul>"
			var details = course[0].details;
			console.log(details);    //获取到了details的数组
				console.log(details.length);		
			for(i=0 ; i< details.length; i++){
				
						str+='<li><span style="background-color:'+details[i].color+'"></span> <h3>'+details[i].title+'</h3>';
						var pcontent = details[i].pcontent;
						for( j = 0 ; j < pcontent.length ; j ++){
							str+="<p>"+ pcontent[j] +"</p>"
						}
						str += "</li>"

			}
			str += "</ul>";
			box.innerHTML = str;



var box =  document.getElementsByClassName("box")[0];  不加点
js加点  $(.)[0]    $(#)    $(div)[0]

### 2个盒子要是都想浮动就需要都加float;



##3d转换   perspective
<!-- 
		电脑显示屏是一个 2D 平面，图像之所以具有立体感（3D效果），其实只是一种视觉呈现，通过透视可以实现此目的。透视可以将一个 2D 平面，在转换的过程当中，呈现3D效果。
		perspective有两种写法
			a) 作为一个属性，设置给父元素，作用于所有3D转换的子元素
			b) 作为 transform 属性的一个值，做用于元素自身,子元素的3D效果可呈现
			
		backface-visibility：visible/ hidden 		设置元素背面是否可见

		 -->
/* 开启3d舞台 使子类元素呈现3d效果 */
				transform-style: preserve-3d;
				
/* 当元素旋转到背面的时候 是否可见 */
				/* backface-visibility:hidden; */

+ flat：所有子元素在 2D 平面呈现
+ preserve-3d：保留3D空间

	.d1:hover{
				transform: rotateX(180deg) rotateY(180deg) rotateZ(180deg);
			}
			.d2:hover{
				transform: rotateY(180deg);
			}
			.d3:hover{
				transform: rotateZ(180deg);
			}

###  classlist

+  classList 属性返回元素的类名，作为 DOMTokenList 对象。

+ 该属性用于在元素中添加，移除及切换 CSS 类。

+ classList 属性是只读的，但你可以使用 add() 和 remove() 方法修改它。

+  add(class1, class2, ...)	在元素中添加一个或多个类名。

				如果指定的类名已存在，则不会添加
				contains(class)	返回布尔值，判断指定的类名是否存在。
				可能值：
				
				true - 元素包已经包含了该类名
				false - 元素中不存在该类名
				item(index)	返回元素中索引值对应的类名。索引值从 0 开始。
				
				如果索引值在区间范围外则返回 null
				remove(class1, class2, ...)	移除元素中一个或多个类名。
				
				注意： 移除不存在的类名，不会报错。
				toggle(class, true|false)	在元素中切换类名。
				
				第一个参数为要在元素中移除的类名，并返回 false。 
				如果该类名不存在则会在元素中添加类名，并返回 true。 
				
				第二个是可选参数，是个布尔值用于设置元素是否强制添加或移除类，不管该类名是否存在。例如：
				
				移除一个 class: element.classList.toggle("classToRemove", false); 
				添加一个 class: element.classList.toggle("classToAdd", true);
				
				注意： Internet Explorer 或 Opera 12 及其更早版本不支持第二个参数。

+ 	li:nth-child(1):hover p{
				color : #af7ead;
			}	第一个li

##动画

		
		动画是CSS3中具有颠覆性的特征之一，可通过设置多个节点来精确控制一个或一组动画，常用来实现复杂的动画效果。
			1、必要元素：
				a、通过@keyframes指定动画序列；
				b、通过百分比将动画序列分割成多个节点；
				c、在各节点中分别定义各属性
				d、通过animation将动画应用于相应元素；
			
			2、关键属性
				1. Animation-name			 动画名称(必填)
				2. Animation-duration	 动画持续时间
				3. animation-timing-function
						linear/ease/ease-in/ease-out/ease-in-out/cubic-bezier(n,n,n,n)：	特定的贝塞尔曲线类型，4个数值需在[0, 1]区间内
				4. animation-delay		 动画延迟（只是第一次）
				5. animation-iteration-count	 重复次数	infinite 无限次
				6.animation-direction		动画是否重置后再开始播放
						alternate动画直接从上一次停止的位置开始执行，倒着来
						normal	动画第二次直接跳到0%的状态开始执行
				7.animation-fill-mode		动画执行完毕后状态
						forwards	当动画完成后，保持最后一个属性值（在最后一个关键帧中定义）。
						backwards	在 animation-delay 所指定的一段时间内，在动画显示之前，应用开始属性值（在第一个关键帧中定义）。
						both	设置对象状态为动画结束或开始的状态，结束时状态优先
			
			语法:	animation: name duration timing-function delay iteration-count direction fill-mode;
			name duration iteration-count 必须写,其余可以都不写
			
			animation-play-state		播放状态（ running 播放 和 paused 暂停 ）


###动画事件监听

		x.addEventListener("animationend", myStartFunction);
		动画的事件：
			•	animationstart - CSS 动画开始后触发
			•	animationiteration - CSS 动画重复播放时触发
			•	animationend - CSS 动画完成后触发

###    animation: circle(名字)  60s(时间)  steps(60)(步数)  infinite(重复) both( 终止);

###字体引用

		@font-face {
				font-family:"mzd";//自定义名字
				src: url("lib/FZQTJW.TTF");//引入名字
			}
			.p1{
			font-family: 'mzd';
			font-size: 30px;
		}

###  js监听滚轮事件
+ 滚动监听
+ 火狐	方向: 3 往下; -3 往上  
		关键代码：if(window.addEventListener){
				window.addEventListener("DOMMouseScroll",this.scroll,false);  //火狐  监听
			}



+  ie 
		window.onmousewheel = this.scroll;   //IE  除了火狐之外 ，这种方式都能处理   监听

            // 			wheelDelta可以测试滚动
			// 			可以判断滚动方向 但是无法判断滚动幅度.
			// 			方向: -120 往下滚动  ; 120 往上滚动
			// 			如何判断滚动幅度呢?

			window.onmousewheel = function (event) {
						console.log(event.wheelDelta);	
					} 


+ 例子

		windowAddMouseWheel();
		function windowAddMouseWheel(){
			var scrollFn = function (e){
				e = e || window.event;
				if (e.wheelDelta) {  			 	// 判断浏览器IE，谷歌滑轮事件
					if (e.wheelDelta > 0) { 	    // 当滑轮向上滚动时
						alert("滑轮向上滚动");
					}
					if (e.wheelDelta < 0) { 	     // 当滑轮向下滚动时
						alert("滑轮向下滚动");
					}
				} else if (e.detail) {  		    // Firefox滑轮事件
					if (e.detail< 0) { 				// 当滑轮向上滚动时
						alert("滑轮向上滚动");
					}
					if (e.detail> 0) { 				// 当滑轮向下滚动时
						alert("滑轮向下滚动");
					}
				}
			}
			//给页面绑定滑轮滚动事件  火狐监听 DOMMouseScroll 事件
			if (document.addEventListener) {
			  document.addEventListener('DOMMouseScroll', scrollFn, false);
			}
			//滚动滑轮触发scrollFunc方法          //其他监听
			window.onmousewheel = document.onmousewheel = scrollFn;
		}
