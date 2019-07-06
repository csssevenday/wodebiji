###js
+ 是一门解释性的语言
+ 是一门脚本语言
+ 是一门弱类型语言
+ 是一门基于对象的语言

+ 
+ 

+ 关于"a++"   "++a"的问题
		
		b=a++   ====>  b=a; a=a+1;
        b=++a   ====>  b=1+a

+ alert()  弹窗

+ console.log()  将信息输入到控制台

+ prompt()    让用户输入信息
 
+ var

 		var a=10;
            b=20;
  	        c=30;
            d=40;
	    console.log(a)   //10


+ 六大类型
   
 		     number      数
            string       字符串
			boolean      布尔
			null         空
			underfined   未定义
			object       对象

+ typeof(变量名)

			var num = 10;
            var str = "小黑";
            var fla = true;
         console.log(typeof num);  //num
         console.log(typeof str);  //string
         console,log(typeof fla);  //boolean


+ NaN  不是一个数字

###date  日期

          var date = new Date（）;
    年    var year = date.getFullYear（），
    月        month = date.getMonth(),
    日        day = date.getDate(),
    星期      week = date.getDay(),
    小时       hour= date.getHours(),
    分钟       minte = date.getMintes(),
    秒        second= date.getSeconds();

          var dateStr = year +"-"+ month +"-"+ day +" 星期"+ week +" "+ hour +":"+ minute +":"+ second; 
 
          console.log(dateStr)

### math
 
   天花板函数
   

    var a= Math.ceil(3.3)  //4 
                .floor(3.3) //3
                .max(3,6);   //6
                .min(3,6);  //3
                .min("ss" 6);  //nan
                .random();   


    var c = Math.round();

   




###比较运算符

 < >  <=  >=    ==   ===   !=  !==

+ 比较运算符得出的值为布尔值  true false
 






###逻辑运算符

+ && 并且    都真才真  有一个false就为false
+   true 遇到false返回,没遇到 就返回之后一个  值 (表达式的值)
+ || 或    有一个真就是真  遇到true就返回true的值 没遇到 就返回之后一个  值 (表达式的值)   
+  
+ ! 非 
  
+ 短路语句: a>3&&console.log("aaa");  输出为underfind

+ !! 是将装换为  布尔类型

+ 转换为boolean值为false的有 null 0 underfined  nan  ""   false  


###显示转换  

+ Number（）  转为数字
+ String（）  转为字符串
+ Boolean（） 转为布尔


###if语句

    If(条件句){
       条件为真的时候去做
    }else{
       条件为假的时候去做
          }



+ 练习

		var hig = prompt("请输入你的体重");
		
		var her = prompt("请输入你的身高");
		
		var bmi= hig/Math.pow(her,2);
		
		if(bmi>=32){
			alert("非常肥胖");
		}else if(bmi>=28){
			alert('肥胖');
		}else if(bmi>=25){
			alert("过重");
		}else if(bmi>=18.5){
			alert('正常');
		}else{
			alert('过轻');
		}


###三元表达式

   表达式 ? 如果表达式为true执行这个 : 如果表达式为false
   和if-else语句一样


+ if-else if......; 一般是对范围的判断,针对多个分之 
+ switch-case语句;一般是对具体的值的判断,多个分之


### 1+"str"==1str ,,,,, 1+2+3+"str"=6str ,,,, "str"+1+2+3 =str123      
### 1-"str"==nan
### 加俩端出现字符串就会是字符串样式,
### - /  % * 会把字符串变为数字



###for循环
    
+ 在写for循环的时候for( var i=0; i<100;i++);其中 var省略掉的话不影响结果，但是会出问题，  

###break continue
+ b
+ 
+ ak 跳出当前所在循环
+ continue  直接进入下一次循环

###数组
+  定义: 存储一组有序的数据,数据类型可以不一样
+  作用: 一次性存储多个数据
+  数组元素: 数组中存储的每个数据
+  数组的长度: 数组的元素的个数叫数组的长度
+  索引 :存储数组元素的编号,从0开始到数组的长度-1,索引是用来存储和读取数组的元素
+  冒泡排序: 求数组的和,最大值,最小值,平均值
+  var 数组名=[];空数组

###函数

+ 函数:把一些重复的代码封装起来,在需要的时候直接调用这个函数
+ 函数的作用: 代码的重用
+ 函数定义: 

         function函数名(){
                 函数体 
                 }

+ 函数调用: 函数名();

+ 参数:形参和实参
+ 形参:函数定义的时候函数名字后面的小括号内的变量, 
+ 实参:函数调用的时候小括号里的内容
+ 返回值: returen
+ 如果函数中有return,但后面没有内容这个函数没有明确返回值,如果函数调用了并且接受了结果为underfined

###函数形参和 arguments 的映射

+ 是有实际参数组成的数组，也是形参的数组

+ arguments callin 就是函数本身

### 函数表达式可以直接在后面直接加小括号（），，， 声明函数（（），或者,）(),但是function前要加括号,(function





###对象
 
+ 创建对象 
+ 实例化对象   
      
         var obj = new Object();
         对象有特征--属性和行为--方法
+ 添加属性 --对象.名字=值;
  
        obj.name="小苏";
        obj.age = 38 ;
        0bj.sex ="男";
+  添加方法   ---对象.名字=函数

        obj.eat=function(){
        console.log("吃西瓜")
            }

+ 输出  

         console.log(obj.name);
        
         方法的调用
         obj.eat();


+ instanceof   知道对象属于什么内容

+ 2  工厂模式创建对象
+   一次性创建多个对象,吧创建对象的代码封装在一个函数中
       
         function  creatObject(name,age){
           var obj =new Object();
            obj.name="name";
            obj.age = "age";  
            obj.say=function(){
               console.log("我叫"+this.name+"我今年"+this.age);
             }
            return  obj;
         }
         //创建人的对象
         var per1 = creatObject("小黄","10" );
         per1.say();
          //在创建一个人的对象
          var per2= creatObject("阿明","20");
          per.say();

+  自定义构造函数创建对象
    
          function Person(name,age){
            this.name="name";
            this.age= "age";
            this.say=function(){
           console.log("我叫"+this.name+"我今年"+this.age);
              };
         }
         var obj= new Person("小米","10");
         console.log(obj.name);
         console.log(obj.age);
         obj.say();
         var obj2= new Person("小黑","20");
  
         没有retunrn  
        console.log(obj instanceof   Person);  //ture
        console.log(obj2 instanceof Person);  //ture
+ 3 字面量的方式创建对象

        var obj ={
            name:"小明",
            age:20,
            sayHi:function（）{
               console.log(this.name)
              },
             eat:function(){
                console.log(this.age)
              }
         } ; 
        obj.sayHi（）;
        obj.eat();

        注意里面都是逗号
###json

      var json ={
        "name":"xiaoming",
        "age" : " 10",
        }
    遍历对象不能通过for;无序
     var key = "name"
     console.log(json[key]

    可以通过for in来循环
    for(var key in json){
        console.log(key);
        console.log(json[key]);

###内置对象 :

+ Math
+ Date
+ String
+ Array
+ Object  

###阻止超链接跳转 

      return false 

###concat方法

		var arr = [1,2,3,4];
		arr = arr.concat(1,2,["a","b","c"]);
		arr = [1,2,3,4,1,2,"a","b","c"]

###join
  
 		  // 数组各个元素是通过指定的分隔符进行连接成为一个字符串，并返回
			// 字符串。语法： arrayObject.join(separator)
			var arr = [1,2,3,4,5];
			arr = arr.join(" / ");
			console.log(arr);
###split

split() 将字符串转换成数组形式的字符串并返回数组。语法：
stringObject.split(separator,howmany)

			var str = "smith,john,gina,white,kate";
			// var arr = str.split();	// ["smith,john,gina,white,kate"]
			// var arr = str.split(",");	// ["smith", "john", "gina", "white", "kate"]
			// var arr = str.split("h");		//	["smit", ",jo", "n,gina,w", "ite,kate"]
			var arr = str.split(",", 3);		//写0为0	,写3长度为3,不是下标 ["smith", "john", "gina"]
			console.log(arr);

###域的问题

+ 	所有在script里面的是   window   的域
+  函数里面是他自己的作用域       函数里面的域可以调用外面域的内容,反过来不可以

###声明提升

+ js 执行的时候有一个预编译的过程,将所有声明的变量和函数提升
+ 变量声明先提升，函数声明再提升

### 函数参数就近原则

		function add(a,b){
				// 1,2
				a = 10;
				console.log(a);
				
				b = 20;
				function a(){
					
				}
				console.log(a + b);
			}
			
			add(1,2);

###立即执行函数

		    1. 函数表达式可以直接在后面加小括号,声明函数不能这样做
			var fn = function (){
				console.log("aaa");
			}();
			// fn();


			 2. 声明函数(function fn(){}())
			(function fn1(){
				console.log("aaa1");
			}());
			// 3. 声明函数(function fn1(){})()
			(function fn2(){
				console.log("aaa2");
			})();
			// 4. 
			var fn3 = (function (){
				console.log("aaa3")
			})();

###arguments 

        add(1,3,4,5,6,7);
		function add(a,b){
			arguments = [a,b];   
	
		console.log(arguments);
			console.log(arguments[0]);
		console.log(a === arguments[0]);
		} 
        传入实参的数组     但是arguments还是4


###对象

			// 通过字面量形式创建对象
			var obj = {
				name: "张三",
				age: 20,
				say: function (){
					alert(this.name);
				}
			};

###数组高级api

+  	 把数组转换成字符串，每一项用,分割
  	
			var arr = [1,2,3,5,4,6];
			var str = arr.toString();
			console.log(str);//1,2,3,5,4,6

+  	 翻转数组,更改了原对象
  	
			// arr.reverse();	//  [6, 4, 5, 3, 2, 1]

+  数组索引,找到返回相应下标,如果没找到返回-1 
 
         var arr1 =     ["str","adc","b","fff","t","adc","t","h","adc"];
					// 数组索引,找到返回相应下标,如果没找到返回-1
		 			if(arr1.indexOf("h") !==    -1){
		// 				alert("true");
		// 			}else{
		// 				alert("false");
		// 			}
					var m = arr1.indexOf("adc");
					var n = arr1.lastIndexOf("adc");
					console.log(m,n);    m=1  n==8

+  slice    从当前数组中截取一个新的数组，不影响原来的数组，

        slice (0)  是所以
		slice ( 0,2) 从下标0 到小标2 不包括下标2

+ push  加到最后

+  splice    
+    splice(start,deleteCount,options) 参数 start,deleteCount,options       (要替换的项目) 
				arrayObject.splice(index,howmany,item1,.....,itemX),改变了原数组,返回了被删除的元素
				删除：2个参数，起始位置，删除的项数 [start,start+number]
				插入：3个参数，起始位置，0，插入的项
				替换：任意参数，起始位置，删除的项数，插入任意数量的项  

+ 	数组的清空
			// arr.length = 0;
			arr = []; // 清空数组常用

+    sort(函数) 给数组按 unicode 编码排序 在原数组上进行更改
			/*
				可带参,参数必须是函数,有两个形参
				函数返回值为负数 前面的值在前面
				函数返回值为正数,后面的值在前面
				函数返回值为0,不动
			*/

       var arr5 = [6,2,1,5,8,9,5,6,3,2,12,16,25];
			// arr5.sort();  a - b
		
			若 a 小于 b，在排序后的数组中 a 应该出现在 b 之前，则返回一个小于 0 的值。
			若 a 等于 b，则返回 0。
			若 a 大于 b，则返回一个大于 0 的值。
		
		主要运用正倒排序
        	arr5.sort(function(a,b){				
				return a - b;       // 正序
				// return b - a;	// 倒序
			})
			console.log("arr5====>" , arr5);
			

###字符串的高级api
 
  			// charAt() 获取相应位置字符
			var str = "hello world";
			console.log(str.charAt(0));  //h  5为空格


			//charCodeAt() 方法可返回指定位置的字符的 Unicode 编码。这个返回值是 0-65535 之间的整数。
			console.log(str.charCodeAt(3));  //l的码是108


			// indexOf() 返回字符在字符串中的位置
			console.log(str.indexOf("h"));    //0
			// lastindexOf()
			console.log(str.lastIndexOf("o")); //7


			// concat() 连接字符串
			console.log(str.concat("!"));   //把!与hello world连接为 										hello world!


			// slice() 方法可提取字符串的某个部分，并以新的字符串返回被提取的部分。
			console.log(str.slice(-3))  //-3为rld  //(1,3)为el //3为								  lo world 


			// substr() 用的非常多 substr(起始位置,[取的个数])
			// 返回一个新的字符串，包含从 string 的 start（包括 start 所指的字符）处开始的 length 个字符。
			console.log(str.substr(0,5));   //hello  (从0开始截取5个)
											//(1,1)  e

			// toUpperCase() toLowerCase()	变为大小写 ,不影响原字符串
			console.log(str.toUpperCase());
			// console.log(str.toLowerCase());

###  json   	// json 保存数据的时候不保存方法function

		   /* 遍历对象的方法和属性 for in 循环 */
			  for(var i in obj){
				 console.log("i====>" + i);
				 console.log("obj["+i+"]====>" + obj[i]);
			}

+ 	var obj1 = JSON.stringify(obj);  转换成json对象的方法
+ 	
			    {                    //json对象
			     "name":"zhangsan",
			      "age":20,
			      "frind":["white","role","jack","Kyte"]
			     } 	

+ JSON.parse() 方法将数据转换为 JavaScript 对象。

		var obj2 = JSON.parse(obj1);
		{
			name: "zhangsan", 
			age: 20,
			 frind: Array(4)
		}		

##dom

+  	事件三要素: 事件源,事件触发,事件处理

+ 获取类名            给css添加样式 类名 标签名 id
			// 获取节点的方式 类名(class) 标签名 id
			var box = document.getElementById("box");
			var pEle = document.getElementsByTagName("p"); // [p.title,p]	 在IE<=8下不兼容
			var bEle = document.getElementsByClassName("title"); // [box,p]

+ 节点属性
            var box = document.getElementById("box");	
			console.log(box.nodeType);                   //标签 1
			var iNode = box.getAttributeNode("id");	
			console.log(iNode.nodeType);             // 获取属性节点	2
			console.log(iNode);                      //id = "box"
			
			console.log(box.childNodes[0].nodeType); // 文本3
			console.log(box.nextSibling.nodeType); // 注释8

+ 更改样式
 
            元素.style.样式key值 = "value";
			更改样式有 - 的必须使用小驼峰命名,第二个首字母大写
			box.style.width = "300px";
			box.style.height = "300px";
			box.style.backgroundColor = "blue";
			
			更改元素的类名 元素.className = "value"
			box.className = "box d2";
			var box2 = document.getElementsByClassName("box")[0];

+  父亲节点

       <div class="box">
			<p class="title">不凡学院</p>
			<p class="text">info1...</p>
			<p class="text">info...</p>
		</div>

           var pEle = document.getElementsByTagName("p")[0];
			// var p2 = document.getElementsByClassName("text")[1];
			

			var dEle = pEle.parentNode;
			// var dEle = p2.parentNode; 	
        	dEle  都为    <div class="box">
							 <p class="title">不凡学院</p>
							 <p class="text">info1...</p>
							 <p class="text">info...</p>
						  </div>
###兄弟节点

+  下一个兄弟节点
      兼容写法: nodeEle = 节点 .nextElementSibling || 节点 .nextSibli 

+ 上一个兄弟节点    

		兼容写法: nodeEle =节点 .previousElementSibling || 节点 .previousSibling 

###子节点 

+ 获取第一个子元素

	 兼容写法: childNode = 元素.firstElementChild || 元素.firstChild

+ 获取最后一个子元素

	兼容写法: childNode = 元素.lastElementChild || 元素.lastChild

+ 获取所有的子元素 childNodes children

		var allChild = box.children	// box下的所有元素节点

+   封装获取孩子节点的方法
			function allChildren(pNode){
				var childArr = [];
				var pChild = pNode.childNodes;
				for(var i = 0; i < pChild.length; i ++){
					// 返回元素节点 nodeType == 1
					if(pChild[i].nodeType == 1){
						childArr.push(pChild[i]);
					}
				}
				return childArr;
			}

###创建节点

+  创建标签元素
			var pEle = document.createElement("p");
			pEle.innerHTML = "不凡学院<span> 今天天气真好啊 </span>";

+  往页面中添加元素
			1. 通过父节点插入子节点   父节点.appenChild(要插入的元素);
			box.appendChild(pEle);   插入的为<>标签形式
                 inner.HTML ()       插入的为
			 父节点.insertBefore(要插入的节点，参考节点)；
             

			box.insertBefore(imgEle,pEle);
		    box.appendChild(imgEle);
			// 注意: 同一个对象不能重复插入,后面的会替换前面的

+ 删除节点   父节点.removeChild（子节点）
			 box.removeChild(pEle);

			不知道父级的情况下，可以节点自己删除自己
			pEle.parentNode.removeChild(pEle);

+ 克隆节点   oldNode.cloneNode（true）
			var p2 = pEle.cloneNode();	    // 不加参数是浅克隆 不克隆元素内部的东西
			box.appendChild(p2);

			var p3 = pEle.cloneNode(true);	// 加 true 表示全部克隆,包括子节点

+  js中  节点属性操作  style  src   href

		获取：getAttribute(名称)
				设置：setAttribute(名称, 值)
				删除：removeAttribute(名称)
			
			var c = box.getAttribute("style");
			var imgSrc = imgEle.getAttribute("src");
			

         设置
			box.setAttribute("class","box d1 d2");
			/*box.setAttribute("style","background-color: orange");

			// 设置style就是设置行内样式   要传"style"与 "css中的样式"
              改变css样式还可以写出  box.style.display = block;

 +      删除照片路径
			img.removeAttribute("src");


###jq中属性改变
+ $(".mask").show();显现    $(this).hide();隐藏
			
  

###插入文本或者标签

		var box = document.getElementsByClassName("box")[0];
			
			box.innerHTML = "<p>不凡学院</p>";
			var pEle = box.children[0];    // <p>不凡学院</p>
			pEle.style.color = "orange";
			pEle.innerHTML = "不凡学院<span></span>";
			var spanEle = pEle.children[0];
			spanEle.innerText = "666";


###js拿输入的信息

			$(".submit")[0].onclick = function (){
 			 拿信息
 				var uname = $(".uname")[0].value;
 				var age = $(".age")[0].value;
 				var phone = $(".phone")[0].value;
 				console.log(uname, age, phone);
 			}

###jq中拿信息

				 获取数据
				var uname = $(".uname").val(),
						age = $(".age").val(),
						phone = $(".phone").val();

####改变li里面的class属性 删其他act 给当前点击加act, 

		// 接受一个元素和下标
			function fn(index){
				
				if(n !== index){
					n = index;
				}//让n与下标同步  需要的时候才写
				
				// 找到带有激活样式的元素 [0];
				var act = document.getElementsByClassName("act")[0];
				// 去除 激活样式 将 act 类名删除 class===>"list"
				act.setAttribute("class","list");
				// 给当前被点击的元素添加激活样式 class===>"list act"
				lis[index].className = "list act";
				// 取出 被点击元素 子元素图片 的路径
				var src = lis[index].children[0].getAttribute("src");
				// 将路径赋给box的背景
				box.style.backgroundImage = "url(" + src + ")";
			}

####字符串拼接  并加入到body里面

		var body = document.getElementsByTagName("body")[0];
		    // innHTML 字符串
			var str = "<ul>";
			for(var i = 0; i < 4; i ++){
				str += "<li class=\"list" + (i===0? " act": "" ) + "\"  onclick=\"fn(" + i + ")\"><img src=\"./img/m" + (i+1) + ".jpg\" alt=\"\"></li>";
			}
			str += "</ul><div class=\"box\"></div>";
			body.innerHTML = str;

####添加和删除类名的方法

			// 添加 和 删除 类名 方法
			/*
				1. 写函数
				2. 写形参  element  添加的类名
				3. 获取 element 所有的类名
			*/
			var box = document.getElementsByTagName("div")[0];
			removeClass(box,"d2");
			function addClass(ele,value){
				// className 没有类名为"",getAttribute("class")在没有class的时候返回null
				var str = ele.className;

				// 判断要添加的类名是否已存在
				if(str.indexOf(value) === -1){
					// class = "box d1 d2"
					if(str.length){
						str += " " + value;
					}else{
						str += value;
					}
				}
				ele.setAttribute("class",str);
			}


			function removeClass(ele,value){
				var str = ele.className;
				// "box d1 d2" 删除 d1				slice,substr
				var index = str.indexOf(value);
				if(index !== -1){
					// 证明 要删除的类名存在,index就是要删除的类名起始位的下标
					if(index + value.length === str.length){
						// 如果相等 证明要删除的元素是以后一个类名 " d2"
						str = str.slice(0,index-1);
					}else{
						// 要删除的元素不是最后一个 删除 "d1 "
						str = str.slice(0,index) + str.slice(index+value.length+1);
					}
				}
				ele.setAttribute("class",str);
			}


### bom 

+  事件监听
  
			min.addEventListener("click",fn,true);//true  外到内
			inner.addEventListener("click",fn,true);
			box.addEventListener("click",fn,true);
			body.addEventListener("click",fn,true);
			
			min.addEventListener("click",fn,false);//内到外
			inner.addEventListener("click",fn,false);
			box.addEventListener("click",fn,false);
			body.addEventListener("click",fn,false);

####定时器
+   延时	setTimeout		setTimeout(执行函数,时间(单位:毫秒))
+   时间循环 setInterval(执行函数,时间(单位:毫秒))

+   倒计时		getTime()	获取时间戳(当前时间的字符串表示)
			
			var futureTime = new Date("2019-4-1 9:58:00").getTime(),
					hourTime = 60*60*1000,
					minTime = 60*1000;
			var timer = setInterval(function (){
				var nowTime = new Date().getTime();
				if(nowTime >= futureTime - 1000){
					alert("boom");
					clearInterval(timer);		// 删除定时器 定时器必须有名字
				}
				var	countTime = futureTime - nowTime,	// 时间差
					hour = Math.floor(countTime/hourTime),
					minute = Math.floor((countTime % hourTime)/minTime),
					second = Math.floor((countTime % minTime) / 1000);
				
				var str = "还剩下" + hour + "时" + minute + "分" + second + "秒";
				box.innerText = str;
				
			},1000)

####offset
+   offset宽/高 = 盒子自身的宽/高(width/height) + padding + border返回数字,只读属性

+  家族成员： `offsetWidth` `offsetHeight` `offsetLeft` `offsetTop` `offsetParent`

#### `offsetWidth`  `offsetHeight`  （检测盒子自身宽高）

> 这两个属性，他们绑定在了所有的节点元素上。获取之后，只要调用这两个属性，我们就能够获取元素节点的宽和高。

>` offset宽/高  =  盒子自身的宽/高(width/height) + padding +border`

#### `offsetLeft`  和  `offsetTop`  （检测距离父盒子有定位的左/上面的距离）

> 如果父级都没有定位则以 `body` 为准, `offsetLeft` 从父亲的 `padding` 开始算,父亲的 `border` 不算。
> 在父盒子有定位的情况下，`offsetLeft == style.left`(去掉 px)

#### `offsetTop/Left` 和 `style.top/left` 的区别：

1. 最大区别在于 `offsetTop/Left` 可以返回没有定位盒子的距离左侧的位置。而 `style.top/left` 不可以

2. `offsetTop/Left` 返回的是整数，而 `style.top/left` 返回的是字符串，除了数字外还带有单位：`px`


####闪现动画

		<div class="box"></div>
		
		<button>调到400px</button>
		<button>调到800px</button>
		<script type="text/javascript">
			var box = document.getElementsByClassName("box")[0];
			var btn1 = document.getElementsByTagName("button")[0];
			var btn2 = document.getElementsByTagName("button")[1];
			
			btn1.onclick = function (){
				box.style.left = "400px";
			}
			btn2.onclick = function (){
				box.style.left = "800px";
			}

####匀速动画

		btn1.addEventListener("click",function(){
				move(box,400);
			},false);
			btn2.addEventListener("click",function(){
				move(box,800);
			},false);
			
			// ele: 运动元素		target: 终点
			var timer;
			function move(ele,target){
				clearInterval(timer);		// 进函数就清除定时器
				var start = ele.offsetLeft;		// 起点
				var step = target>start?5:-5;
				timer = setInterval(function (){
					var start = ele.offsetLeft;		// 起点
					ele.style.left = start + step + "px";			// 每次运动
					var cha = target - start;	// 获取终点和起点的距离
					if( Math.abs(cha) <= Math.abs(step) ){		// 判断距离是否大于步长
						ele.style.left = target + "px";		// 直接终点
						clearInterval(timer);		// 清除定时器 清除速度
					}
				},17)
			}

####缓动动画

			btn1.onclick = function (){
			move(box,400);
			}

			btn2.onclick = function (){
			move(box,800);
			}
			var timer;
			function move(ele,target){
				timer = setInterval(function (){
					var start = ele.offsetLeft;		// 起点	offsetLeft 获取的始终是整数
					var step = (target - start) / 10;
					/*console.log(step);*/
					// step < 1 的时候 	终点和起点的距离	10 以内的整数
					if(Math.abs(step) < 1){
						step = step > 0 ? 1 : -1;
						
					}
					if(start === target){
						clearInterval(timer);
						return;
					}
					ele.style.left = start + step + "px";
					console.log(ele.style.left)
				},17)
			}

####立即执行函数传参

	for(var i = 0; i < lis.length; i ++){
				/* 
					点击事件每次访问 I 的时候 I 都是 5
					lis[i].onclick = function (){
						console.log(i);		// 5
					}
				*/
				lis[i].onclick = function (n){
					console.log(n);		// 立即执行的时候每次访问的 i 都是当前值 0,1,2,3,4
					return function (){
						console.log(n);
					}
				}(i)
			}



+  立即执行函数传参		1. 传值 (必须有形参接收)		2. 变量
			/* var a = 10;
			var fn = function (name){
				console.log(name);
			}("lisi");
			(function fn1(name){
				console.log(name);
			})("zhangsan"); */
			// 传变量		如果传入的值被形参接收,传入的变量就变成局部变量
			// 如果没有被形参接收,传入的变量就是全局变量
			/* var n = 30;
			(function fn2(n){
				n = 20;
				console.log(n);
			}(a)) */


####事件

+  	// 如果事件的执行函数里面写了一个形参,这个形参就是 event 对象,写多了形参无效
			// 一般写成 e 作为 event 的简写
			box.onmousedown = function(e,m){
				e = e || window.event;
				console.log(e);
				
				// 事件目标		兼容写法 e.target = e.target || e.srcElement
				//console.log("e.target===>",e.target);
				//console.log("e.target===>",e.srcElement);
				
				// 获取鼠标位置
			}

###  返回页面被卷入的高度

+ function sct(){
				return document.documentElement.scrollTop || window.pageYOffset || document.body.scrollTop;
			}

####onscroll 事件在元素滚动条在滚动时触发。
+ onmousemove  鼠标移动

### 鼠标跟随

	window.onmousemove = function (e){
				// console.log("aaa");
				e = e || window.event;
				var x = e.pageX;		// 获取鼠标横坐标
				var y = e.pageY;		// 获取鼠标纵坐标
				// 给box设置左上的定位置
				box.style.left = x - box.offsetWidth/2 + "px";  //
				box.style.top = y - box.offsetHeight/2 + "px";
			}

#### 拖拽案例
+ e就是 inner.onmousedown 这个事件下面需要他的距离 所以写了

			inner.onmousedown = function (e){
				e = e || window.event;
				// 按下改变透明度
				inner.style.opacity = 0.5;
				var offsetX = inner.offsetLeft,
						offsetY = inner.offsetTop,
						// 鼠标距离inner盒子的上边距和左边距
						distanceX = e.pageX - offsetX;
						distanceY = e.pageY - offsetY;
				// 按下鼠标移动才算数,所以写在按下鼠标的事件里面
				window.onmousemove = function (e){
					// 需要重新获取 鼠标距离页面的 上边距和左边距
					e = e || window.event;
					var moveX = e.pageX - distanceX;
					var moveY = e.pageY - distanceY;
					inner.style.left = moveX + "px";
					inner.style.top = moveY + "px";
					// 在移动的添加边界
					if(inner.offsetLeft <= 0){
						inner.style.left = 0;
					}else if(inner.offsetLeft >= (box.offsetWidth-inner.offsetWidth)){
						inner.style.left = box.offsetWidth-inner.offsetWidth + "px";
					}
					
					if(inner.offsetTop <= 0){
						inner.style.top = 0;
					}else if(inner.offsetTop >= (box.offsetHeight - inner.offsetHeight)){
						inner.style.top = box.offsetHeight - inner.offsetHeight + "px";
					}
				}
			}
			
			window.onmouseup = function (){
				// 松开还原透明度
				inner.style.opacity = 1;
				window.onmousemove = null;
			}

#### 淘宝放大镜需要用到
+  imgEle 移动的距离是 2 倍 的inner.offsetL / T    
+  
					imgEle.style.marginLeft = -4 * inner.offsetLeft + "px";
					imgEle.style.marginTop = -4 * inner.offsetTop + "px";

####   获取样式的元素   要获取的样式名字    getStyle(box,"height");
      
            function getStyle(ele,styleName){
				if(ele.currentStyle){
					return ele.currentStyle[styleName];       //ie
				}else {
					return window.getComputedStyle(ele,null)[styleName];   //谷歌
				} 
			}


				<style>
				#mydiv {
				     width : 300px;
				}
				</style>
				则:
				
				复制代码
				var mydiv = document.getElementById('mydiv');
				if(mydiv.currentStyle) {
				      var width = mydiv.currentStyle['width'];
				      alert('ie:' + width);
				} else if(window.getComputedStyle) {
				      var width = window.getComputedStyle(mydiv , null)['width'];
				      alert('firefox:' + width);
				}

###    对象获取属性的两个方式

			// obj.attrName			obj["attrName"]
			var obj = {
				name: "zhangsan",
				age: 28
			}
			console.log(obj.name);     console.log(obj["name"]);  

			// 当获取的属性名是一个变量的时候		obj[变量]
			var a = "name";
			// obj[a]		// "zhangsan"

###  伪元素

		before  在所有子元素之前 		after 在所有子元素之后  添加样式的时候 content 必须写  -->  写在getComputedStyle
		<script src="js/main.js" type="text/javascript" charset="utf-8"></script>
		<script type="text/javascript">
			var box = $(".box")[0];
			var result = getComputedStyle(box, "::before").content;
			//console.log(result); 		// "hello world!"
			
			var value = getStyle(box,"height");

###事件委托  
+ 委托给父亲  或者父亲的父亲

		lis[0].parentNode.onclick = function (e){
				e = e || window.event;
				// var t = e.target;			// e.target  事件的目标  在IE下有兼容问题  e.srcElement
				var t = e.target || e.srcElement;
				console.log(t);
				// 元素的 元素.tagName 的返回值都是大写
				if(t.tagName === "LI"){
					t.style.color = "red";
				}
			}

####阻止冒泡

		var box = $(".box")[0];
			box.onclick = function (){
				this.style.display = "none";
			}
			box.children[0].onclick = function (e){
				e = e || window.event;
				e.stopPropagation?e.stopPropagation():e.cancelBubble = true;
			}