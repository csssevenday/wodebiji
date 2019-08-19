###  mock 设置数据 

			for (var i = 0; i < 10; i++) {
		      this.sub.push({
		        id: Random.guid(),
		        img: Random.image("130x130", Random.color()),
		        name: Random.name(),
		        num: Random.integer(222, 1888)
		      });
		    }
		    this.target = this.sub.concat();
## vueX
### 实现数据的双向绑定   Vue内部通过Object.defineProperty方法属性拦截的方式，把data对象里每个数据的读写转化成getter/setter，当数据变化时通知视图更新
  
### 当组件进行数据修改的时候我们需要调用dispatch来触发actions里面的方法。actions里面的每个方法中都会有一个commit方法，当方法执行的时候会通过commit来触发mutations里面的方法进行数据的修改。mutations里面的每个函数都会有一个state参数，这样就可以在mutations里面进行state的数据修改，当数据修改完毕后，会传导给页面。页面的数据也会发生改变。

###　由于传参的方法对于多层嵌套的组件将会非常繁琐，并且对于兄弟组件间的状态传递无能为力。我们经常会采用父子组件直接引用或者通过事件来变更和同步状态的多份拷贝。以上的这些模式非常脆弱，通常会导致代码无法维护。所以我们需要把组件的共享状态抽取出来，以一个全局单例模式管理。在这种模式下，我们的组件树构成了一个巨大的“视图”，不管在树的哪个位置，任何组件都能获取状态或者触发行为！另外，通过定义和隔离状态管理中的各种概念并强制遵守一定的规则，我们的代码将会变得更结构化且易维护。




###lodas正序倒序  排序
 
		_.sortBy(arr, function(item) {
		  return item.createTime;
		});
		倒序：
		
		_.sortBy(arr, function(item) {
		  return -item.createTime;
		});
		注意前面的负号 

##  豆瓣电影 图片显示需要这句话

+   <img :src="'https://images.weserv.nl/?url='+movie.images.small" alt />
   
##  mock模拟Web数据：

+ 生成随机域名(每次运行结果不同)：

		var Random = Mock.Random
		Random.domain()  //   "nhou.org.cn"
+ 生成随机IP(每次运行结果不同)

		var Random = Mock.Random
		Random.ip()   //  "74.97.41.159"
生成随机URL(每次运行结果不同)

	Random.url()  //   "news://wrmt.na/rbcgbws"

模拟地理位置数据： 

生成随机省份：

	var Random = Mock.Random
	Random.province()  //"海南省"
 

生成随机城市：

	var Random = Mock.Random
	Random.city()   // "澳门半岛"
 
生成在某个省份的某个城市：

	var Random = Mock.Random
	Random.city(true) // "广东省 广州市"
 

模拟文本数据：

 
生成一条随机的中文句子：

	var Random = Mock.Random
	Random.csentence()   //  "会候权以解包党心要按总场火义国而片精。"
【注意】

1.默认一条句子里的汉字个数在12和18之间

2. 通过Random.csentence( length )指定句子的汉字个数：

    Random.csentence(5)  // "文斗领拉米。"
3.通过Random.csentence( min?, max? )指定句子汉字个数的范围：

    Random.csentence(3, 5)  // "住验住"
 

生成随机的中文段落：

    var Random = Mock.Random
    Random.cparagraph()  
// "电力速率离老五准东其引是外适只王。体区先手天里己车发很指一照委争本。
   究利天易里根干铁多而提造干下志维。级素一门件一压路低表且太马。"
 

【注意】

cparagraph可以看作是多条csentence以逗号连接后的字符串，默认条数为 3 到 7条csentence
			通过Random.cparagraph(length )指定句子的个数
			Random.cparagraph(2) 
		// "而易除应精基还主局按选际复格从导。天第们国分比积造业王该回过白亲。"
4.通过Random.cparagraph(min?, max?）指定句子的个数的范围：

	Random.cparagraph(1, 3)
	//  "作养装军头确应当号天革来人车号把文。证细专物转民相解状律极或经较把马。
     其省级支际标业强龙算建物况。"
模拟颜色数据：

	var Random = Mock.Random
	Random.rgba()  // "rgba(122, 121, 242, 0.13)"
 

模拟日期/时间数据：

日期：

		Random.date('yyyy-MM-dd')  // "1975-04-27"
		Random.date('yy-MM-dd')    //   "00-01-08"
 

时间：

       Random.time()   // "05:06:06"
模拟图片：

      Random.image('200x100', '#4A7BF7', 'Hello')
 

不指定参数则取随机的宽高并显示对应的宽高数据：



模拟姓名数据：

模拟全名：

     Random.cname()   // "黄秀英"

模拟姓氏：

     Random.cfirst()   // "龙"
 

模拟名字

     Random.clast()  // "秀英"

##守卫 

		 beforeRouteEnter(to, from, next) {
		    console.log(this, 'beforeRouteEnter'); // undefined
		    console.log(to, '组件独享守卫beforeRouteEnter第一个参数');
		    console.log(from, '组件独享守卫beforeRouteEnter第二个参数');
		    console.log(next, '组件独享守卫beforeRouteEnter第三个参数');
		    next(vm => {
		      //因为当钩子执行前，组件实例还没被创建
		      // vm 就是当前组件的实例相当于上面的 this，所以在 next 方法里你就可以把 vm 当 this 来用了。
		      console.log(vm);//当前组件的实例
		    });
		  },

?例子
		 beforeRouteEnter(to, from, next){
		    if(to.name== "goodsDetail"){
		     next(vm =>{
		             
		       vm.parr ="par"
		     })   
		    }   
		  },   

###返回上一级    @click="$router.go(-1)"

		  <img @click="$router.go(-1)" src="@/assets/imgs/kind/back.png" alt class="icon-back">

### 路由写法
     {
      path: '/home',
      name: 'home',
meta 可以用来传参
      meta:{
        footShow: true     //让底部显示
      },
      // route level code-splitting
      // this generates a separate chunk (about.[hash].js) for this route
      // which is lazy-loaded when the route is visited.    懒加载
      component: () => import(/* webpackChunkName: "home" */ '@/views/home/Home.vue')
     },

###  模拟  axios  promise
		   
           import {
			   resolve,
			   reject
			} from '_any-promise@1.3.0@any-promise';    模拟的时候可以不写  应该
 
 
			function getBannerImgs() {
			   var imgs = [];
			   imgs.push({
			      id: 1,
			      img: require('@/assets/imgs/home/swiper-1.png')
			   })
			   imgs.push({
			      id: 2,
			      img: require('@/assets/imgs/home/swiper-2.png')
			   })
			   imgs.push({
			      id: 3,
			      img: require('@/assets/imgs/home/swiper-3.png')
			   })

			   var promise = new Promise((resolve, reject) => {
			      setTimeout(() => {
                     //正确的时候
			         resolve(imgs);   
			      }, 200)
			   })

			   return promise;
			}

3 导出  方法
		export default {
		   getBannerImgs,
		}

4 导入   import homeApi from "@/api/home";
    
#### vue swiper
+下面为轮播的导入方式    无关 promise     npm install vue-awesome-swiper --save
		   // swiper 样式
			import "swiper/dist/css/swiper.css";
			// 引入组件
			import { swiper, swiperSlide } from "vue-awesome-swiper";
+组件的导入   无关 promise
		+ import thy from "./components/Monday" 
		+ import tuesday from "./components/Tuesday"

5 created 生命周期声明

		      created() {
调用方法
			     this.getBannerImgs();
			  },
			  methods: {
 promise 写法      
                getBannerImgs(){
                      homeApi.getBannerImgs().then(res => {
			          this.bannerImgs = res;
			         });
                 }
			  }


###   跳页面
    :to="{name:'goodsDetail',params:{subKindId:$route.params.subKindId,id:1}}"
 
###    子路由的 配置  的写法
  
		 path: '/find',
         name:'find',
	      redirect:'/find/recommend',  默认进的时候 那个路由优先
	      meta:{
	        footShow:true,      底部框显示  
	      },
	      component: () => import(/* webpackChunkName: "kind" */ './views/find/Find.vue'),
	      children:[     子路由
	        {
	          path: 'recommend',
	          name: 'recommend',
	          meta:{
	            footShow:true,
	          },
	          component: () => import(/* webpackChunkName: "kind" */ './views/find/recommend/Recommend.vue'),
	        },
	        {
	          path: 'article',
	          name: 'article',
	          meta:{
	            footShow:true,
	          },
	          component: () => import(/* webpackChunkName: "kind" */ './views/find/article/Article.vue'),
	        }
	      ]
	    },

###  导组件的过程  防止页面过长 或者把一些 功能性的东西 放到外面多次引入 

+ 写好子组件 
+ 导到父组件  自己命名  import MyComments from './components/Comments.vue'
+ 在 components:{ MyComments }  中声明一下 
+ 在页面中写入组件 <my-comments  class="comments-com"></my-comments>

###<router-link></router-link>

+ 路由进行跳转页面   多个点击  一个坑 不用导入组件 什么的  路由配好 即可  
+ 静态to 默认跳转  动态to是 需要{name:"xxx" , params{键值对  根据路由写 一般为id} }
		  <router-link tag="div" class="artic"  to="/find/article">精选文章</router-link>
          <router-link tag="div" class="findgoo"  to="/find/goods">好物推荐</router-link>
 
           <router-view></router-view>


###   &.router-link-exact-active {
          color: #010e0d;
       }
+这个是  vue路由切换总是默认添加一个class   router-link-exact-active   切换到谁谁有


###  完整的 api  模拟

			import Mock from "mockjs"
			import {
			    resolve,
			    reject
			} from "_any-promise@1.3.0@any-promise";
			const Random = Mock.Random;
			
			function goodsList() {
			    var list = [];
			    list.push({
			        tag1: 'NEIWAI2019秋冬',
			        tag2: '针织新品优惠',
			        url: require('@/assets/imgs/find/good1.png')
			    })
			    list.push({
			        tag1: 'Paola Paronetto',
			        tag2: '手作摆件艺术',
			        url: require('@/assets/imgs/find/good2.png')
			    })
			    list.push({
			        tag1: 'hot wind',
			        tag2: '热风',
			        url: require('@/assets/imgs/find/good3.png')
			    })
			    
			    for (var i = 0; i < 12; i++) {
			        list.push({
			            id: Random.guid(),
			            url: Random.image('365x160', Random.color()),
			            tag1: Random.ctitle(10, 20),
			            tag2: Random.csentence(5, 7),
			        })

			        // 合并覆盖  list 为0 的

			        // Object.assign(list[0], {
			        //     tag1: 'NEIWAI2019秋冬',
			        //     tag2: '针织新品优惠',
			        //     url: require('@/assets/imgs/find/good1.png')
			        // })
			       
			
			        var promise = new Promise((resolve, reject) => {
			            setTimeout(() => {
			                resolve(list);
			            }, 100)
			        })
			    }
			    return promise;
			}
			export default {
			    goodsList,
			}

###  $nextTick 是在下次 DOM 更新循环结束之后执行延迟回调，在修改数据之后使用 $nextTick，则可以在回调中获取更新后的 DOM      
   在dom元素执行完以后   再 执行 里面的 数据    

###  完整的覆盖修改list的例子

			function subKindList(){
		    var list = []
		    for(var i = 0 ; i <12 ; i ++){
		        list.push({
		            id: Random.uuid(),
		            brand: Random.title(1),
		            title: Random.ctitle(),
		            price:  Random.integer(100,999),
		            saleCount: Random.integer(100,999),
		            img: Random.image('130x130',Random.color() ),
		        })
		    }
		
		    var nowData = [
		        {
		            img: require('@/assets/imgs/kind/detail1.png'),
		            barnd: 'NEIWAI',
		            title: 'Cozy女士家居服莫代尔'
		        },
		        {
		            img: require('@/assets/imgs/kind/detail2.png'),
		            barnd: 'TRIUMPU',
		            title: '文胸内裤套装'
		        },
		        {
		            img: require('@/assets/imgs/kind/detail3.png'),
		            barnd: 'ESSENCE',
		            title: '女士Cozy圆领吊带性感'
		        },
		        {
		            img: require('@/assets/imgs/kind/detail4.png'),
		            barnd: 'LAPERLA',
		            title: '女士Bra-top蕾丝美背无'
		        },
		        {
		            img: require('@/assets/imgs/kind/detail5.png'),
		            barnd: 'CRYSTALS',
		            title: '零敏洛丽无钢圈内衣'
		        },
		        {
		            img: require('@/assets/imgs/kind/detail6.png'),
		            barnd: 'JUDYHUA',
		            title: '女士高端网纱交叠无钢'
		        }
		    ]
		    for(var i = 0 ;i < nowData.length ; i ++){
		        Object.assign(list[i],nowData[i]);
		    }
		    return list
		}


# vueX
          mutations: {
		    // n可以被用来传值  默认为1
		     insCount(state,n=1){ 
		      state.count += n  
		     }
		  },

+   mutations中  可以传个 对象 
		   mutations: {
		    // 
		     insCount(state,stepObj){
		       if(!stepObj){
		         var stepObj = {}
		         stepObj.step = 1 ;
		       }
		      state.count += stepObj.step 
		     }
		  },
+解构的形式 书写
+         insCount(state,{step}){  
		      if(!step){
		        state.count ++ 
		        return 
		      }
		     state.count += step 
		    },
+  运行 商品页面 product中 
//mutations中想修改 state 的值  需要在methods  中用 commit
	     methods: {
	    //   点击修改 state.count的值 用 commit   
	    goCount(){
	        this.$store.commit('insCount',{
	            step:5  为对象的模式
	        })
	    }

###解构   es6
      1 insCount(state,{step,name}){  
		      if(!step){
		        state.count ++ 
		        return 
		      }
		     state.count += step 
		    },
      2
      goCount(){
       this.$store.commit('insCount',{
         step : 2 ,
         name:vuex,   2个属性
       }) ;
     }
调用一个 step   {}  即可  {可以写多个进来}  下面用即可
     insCount(state,{step}){  
     state.count += step 
    },


###  action  延时 处理数据   异步操作  
+在actions 对象中  必须有个回调函数 context或{{commit}}
			actions: {
+ 里面要传入  context  的 回调函数  或者是  {commit}解构写法
+ context 是一个大对象 里面有   commit  与  dispatch
		     insCountSync( context // {commit}解构写法  ){
		        setTimeout(()=>{
 一秒后执行   mutations    
 用 commit 调用  mutations   中的方法   (insCount) 并传值
		          context.commit('insCount',{step:1}) 
		        },1000)  
		     }
		  }

+页面点击事件  

		 insCountSync(){
 点击 让actions运行   必需用 dispatch 
	        this.$store.dispatch('insCountSync')
		   }

###getters  计算属性



## 购物车案例 组件  vuex    不适合储存数据   只是 交换/共享 一些状态
+ 先写 2个 分组件     
+ 引入到主页面中 ( 声明组件  <自己起的名字> </自己起的名字>  )
+ 分配2个 vux文件 在 store 文件夹中 
  --自己创建4个 对象 为 state mutations getters actions 
  --导出   需要用到    namespaced:true命名区间
+ 把2个vuex 导入到 store下的 index.js 中   并且main.js 切换导入的路径  /store/index  
   -- index.js中 注意点 
     ---import Vue from 'vue'
        import Vuex from 'vuex'
//引入2个组件   其他为固定写法 
        import cart from "./modulice/cart"
        import product from "./modulice/product"
        
        Vue.use(Vuex)

        export default new Vuex.Store({
		    modules: {
//导出2个组件
		        cart,
		        product,
		    }
		})

+  信息需要在 vuex中 
  
+  mock 模拟 商品信息  在state中声明一下
+  如何拿商品信息呢         state中的信息运用  计算属性值 
   --product.vue 页面中 的 计算属性中 拿到信息 return this.  $store.state.product.list 
   -- 在页面中展示信息即可   遍历一下      商品信息

+  点击增加
+  
+  中显示 相关产品信息  用id 进行信息交换 
+  点击传出  id
+  methods里面  commit 调用  cart购物车.js/mutations 里的方法 为了获取新的列表信息   并传id    id判断列表信息
		+   addToBuy(id) {
		      // 调用cart/insBuy的方法
		      this.$store.commit("cart/insBuy", id);
		    }

+ 购物车 的vue页面 mutations 中 方法 接受  insBuy( state, id ) 
+ 如果没有id    push  id count为  1
		        if (!state.buy.some(item => item.id == id)) {
		            state.buy.push({
		                id,
		                count: 1
		            })
+如果  有id  找到buy[]  的数组对象   并且count++
		        } else {
		            var item = state.buy.find(item => item.id == id);
		            item.count++
		        }
		        console.log(state);
			    },
			}  
+ 购物车 页面展示的话 产品的信息来自 rootState 的信息
+ 
+ 在 vuex的 getters 计算属性里面进行处理信息 传出  

		var getters = {
		    buyList(state, getters, rootState, rootGetters) {
// 如何获取??   1  后台 api  2 拿product.js中的 方法如下
// 跨模块拿信息   根state=rootState
//  通过state 中的 id 获取到 rootState.product.list 的信息
		        return state.buy.map(item => {
//  map buy[]
//  获取  rootState.product.list 中 id==item.id 的对象
		            var Pitem = rootState.product.list.find(obj => obj.id == item.id)
//item  为  原 buy []
//Pitem 为 商品列表  
//合并起来 为我们想要的 商品列表 + buy.count
		            Object.assign(item, Pitem);
// 总价
		            item.totle = item.count * item.price;
		            return item;
		        })
		    }
		}

+ 购物车页面 接受产品信息处理  
+ 在计算属性中 处理
    computed: {
// 获取购物车的信息  为state中的信息  不是 mutations 修改数据
    buyList() {
// return this.$store.state.cart.buy;
// 获取 根state下的信息  即调用 带命名空间的 getters 
固定写法下面为
      return this.$store.getters['cart/buyList']
    }
  }
+ 上方 v-for 遍历 buyList 即可拿到信息  

+  disabled="true"   按钮不可用

+  商品里面点加的时候  库存变少的解决方法 
    --  里面有 跨model的 mutations  必需写在actions中 
		 var actions = {
		    // 调用其他module 中的 mutations  在actions中 commit 如果是全局的话 {root,true}
		    // 添加到购物车      context上下文对象解构为下面这些对象  解构写法
		    addBuy({
		        dispatch,
		        commit,
		        getters,
		        rootGetters
		    }, id) {
		        // 在  actions 中 调用了 insBuy的方法    
		        commit('insBuy', id)
		        // 跨model 修改商品的 库存 
		        commit('product/desStock', id ,{root:true})
		    },
		} 
+页面获取信息 显示库存 的增减
    addToBuy(id) {
      // 由于 需要减少数量   要调用actions  跨model 代用 mutations 
      // 调用cart/addBuy  让商品库存减少 购物车数量增加  传进去 一个 id 控制那个商品增减
        this.$store.dispatch("cart/addBuy",id) 
    }
  }

####### 小概括
+    商品信息   从product.js 中 获取商品的信息  到 product.vue
+   添加购物车  调用的 是 product.vue 中的方法 到 在 cart.js 生成列表 

+   减少商品的库存 调用 cart.js 的方法  从而修改了   product.js 的库存

+ 获取购物车中的内容 拿的 是 cart.js中的数据  减去库存的话 调用 cart.vue的方法 修改 cart.js 再还原product.js 的库存 



#打包目录配置
publicPath:"/site/zaowu"

#vuex  动画 
 
+ enter
+ enter active
+ enter to 
+ leave
+ leave active
+ leave to

+ 可以给路由 配置 让他有动画
+ <transition>   
     <router-view> </router-view>
+ </transition>  

####  watch用法  监听  nv ov  
 
		watch: {
			$route(to, from) {
				this.getdiscount(to.params.couponUserId); 监听改变在调用一次数据请求 
				// console.log('from=====',from.params.couponUserId)
				// console.log('to=======',to.params.couponUserId)
			}
		}

#### 案例边框改变颜色  点击第几个框让第几个边框 改变为红色

        :class= "{'content':true,'cc':this.liid==coup.id}"

          liid:1 ,  

        yy(id){
	       this.liid = id;
	    },  

        //样式
        .content {
          border: 1px solid #ededed;
          &.cc{
             border: 1px solid red;
          }

####  axios拼接数据
       
        pageIndex:1 ,

       "http://59.110.138.169/api/douban/movie/top250?start=" + this.pageIndex + "&limit=10"

####  从本地 获取 
  +1  
            const TokenKey = 'BUFAN-TEC'

			export function getToken() {
			    // 字符串类型
			  var res = localStorage.getItem(TokenKey);
			  if(res){
			      res = JSON.parse(res);
			  }else{
			      res = undefined;
			  }
			  return res;
			}
			
			export function setToken(obj) {
			    // setItem 必须是字符串
			    localStorage.setItem(TokenKey,JSON.stringify(obj));
			}
			
			export function removeToken() {
			  localStorage.removeItem(TokenKey);
			}   
     
         引入 import { getToken } from '@/utils/myAuth' // get token from cookie
         
          const hasToken = getToken()

			  if (hasToken) {
			    console.log('hasToken',hasToken);
			    if (to.path === '/login') {
			      // if is logged in, redirect to the home page
			      // next({ path: '/' })
			      NProgress.done()
			    } else {
			      // 从vuex获取的  咱们简化  从localstorage huoqu 
			      // const hasGetUserInfo = store.getters.name
			      //获取用户名
			      const hasGetUserInfo = hasToken.username;
			      if (hasGetUserInfo) {
			        next()
			      } else {
			        next(`/login`)
			          NProgress.done()
			      }
			    }
			  } else {
			    /* has no token*/
			
			    if (whiteList.indexOf(to.path) !== -1) {
			      // in the free login whitelist, go directly
			      next()
			    } else {
			      // other pages that do not have permission to access are redirected to the login page.
			      next(`/login`)
			      NProgress.done()
			    }
			  }
+2  
            created() {   
		    const hasToken= JSON.parse(localStorage.getItem('BUFAN-TEC') )   存进来的key值
		    console.log( "123", hasToken  )
		    console.log( "123", hasToken.userId  )
		  },
 
###  刷新验证码 
+		   点击图片的方法

		    refreshImg() {
		      // /admin/login/imgCode?ts=1234234
		      this.imgCode = Url.imgCode + "?ts=" + new Date().getTime();
		    },

##### $router 也可以被用来监听   
+  app 点击下方 跳转的页面 动画 
  
 			 watch: {
			    $route(to, from) {
			      const tabPath = [
			        "/home",
			        "/kind",
			        "/find/article",
			        "/find/goods",
			        "/main"
			      ];
			      if (
			        tabPath.some(item => item == to.path) &&
			        tabPath.some(item => item == from.path)
			      ) {
			        this.transitionName = "fade";
			      } else {
			        // console.log('to.path',to.path)
			        const toDepth = to.path.split("/").length;
			        const fromDepth = from.path.split("/").length;
			        this.transitionName =
			          toDepth < fromDepth ? "slide-right" : "slide-left";
			      }
			    }
			  }
+动画设置 与 时间过度的设置

		     .fade-enter {
				  opacity: 0;
				}
				.fade-enter-active {
				  transition: all ease 0.2s;
				}
				
				.slide-left-enter-active {
				  animation: slideLeft 0.4s;
				}
				.slide-right-enter-active {
				  animation: slideRight 0.4s;
				}
				@keyframes slideLeft {
				  0% {
				    opacity: 0;
				    transform: translateX(100%);
				  }
				  100% {
				    transform: translateX(0);
				    opacity: 1;
				  }
				}
				
				@keyframes slideRight {
				  0% {
				    opacity: 0;
				    transform: translateX(-100%);
				  }
				  100% {
				    transform: translateX(0);
				    opacity: 1;
				  }
				}

##### lable 点击文本 就会触发
+for 指向id
			<label for="male">Male</label>
            <input type="radio" name="sex" id="male" />

###点击购物车的  -  让其数量减少 以及 商品的数量增加 
+ 1 点击 - 号 传出商品的id 
+ 2 在 购物车页面 的methods中调用 购物车的.js 中  mutations中的方法 并传出 id {
+                      用到commit
+                   }
+ 3 在购物车.js中的  mutations中的方法 写出对数据的处理 如果商品数量大于 1 就 减去1 为 0 删除数组
	  +  desBuy(state,id){
        // 根据id删除某一个对象 或者使当前对象的count --
        // {
        //     id:'xx',
        //     count: 0
        // }
        var item = state.buy.find(item=>item.id == id);
        //找到
        if(item.count>1){
            item.count --;
        }else{
            //删除 数量少的话可以  过滤出 不等于当前id的数组 删除掉点击的本条数组 
            state.buy = state.buy.filter(item=>item.id!=id);
        }

###  var actions = {  addBuy({ dispatch, commit, getters, rootGetters },id){ 
                          commit('product/desStock',id ,{ root: true }); }   
        
+  跨module 修改商品库存 需要用到{ root: true }  

+   再在 购物车vue中 methods中  this.$store.dispatch('cart/removeBuy',id);  把commit舍弃掉
       
    commit是调用 mutations 中的方法  
    dispatch 是调用 actions 中的方法 actions中会commit调用 mutations中的方法 
    actions  处理异步操作

##清空购物车 
+  是购物车的功能 写到购物车里面  
+  全买 掉购物车 让购物车数组为空 
    -- 分2步  
      -- 1 muntations 中 {
                 clearbuy (state){
                        state.buy = []  让 state.buy的数组为空  
                  }
                }
      --2   actions中 {
              方法 allIn( {commit} ){
                      commit("clearbuy")  ;
                   }
            }  
     --3  购物车.vue中 methods调用   this.$store.dispatch('cart/allIn');

## 删除购物车 并且使商品的数量增加 
+ 购物车.js 中 传出 数组给商品.js  并且清空 购物车的数组  
+ actions  中  异步 需要 {root:true}
    clearAll({commit,state}){
        // 1.先还原数据
        commit('product/resetStock',state.buy,{root:true});   传出 数组给商品.js 
        // 2.清空购物车
        commit('clearBuy');
    }

+ 商品.js 中 重置 stock
    //重置 stock   传入对象` foreach 遍历 对象 
    // buyArr = [{id:xx,count:3},{id:xx,count:6}]
+   mutations中 处理 接受到的 数据 
    resetStock(state,buyArr){
									
        buyArr.forEach(item=>{   
            //找到符合的对象
            var objItem = state.list.find(obj=>obj.id==item.id);
            // 修改对象的stock
            objItem.stock += item.count;
        })
    }
+  点击清空购物车 
+  methods 中 
    clearBuy(){
      this.$store.dispatch('cart/clearAll');
    }

##checked 的小技巧  

         <div class="rig">  // position: relative;
            <input type="checkbox" class="viewshow input">   //position: absolute;
            <div class="viewshow"></div>
          </div>

 		 .rig {
          position: relative;
          .viewshow {
            display: block;
            float: right;
            width: 43px;
            height: 26px;
            background-image: url("../../../assets/imgs/main/imgs/noshow.png");
            background-size: 100%;
            &.input {
              position: absolute;
              background-color: red;
              right: 0;
              top: 0;
              opacity: 0;
              &.input:checked + .viewshow {
                background-image: url("../../../assets/imgs/main/imgs/show.png");
              }
            }
          }
        }

### 豆瓣 图片
      :src="'https://images.weserv.nl/?url='+m.images.small" alt="">
          

### 豆瓣 星星 

              <li v-for="k in n.zs" :key="k.id"> 根据星星的个数 来遍历星星
                <img src="../../assets/imgs/indent/星复制 2.png" alt>
              </li>
+ getaverage 可以当成一个方法 并且传出数据 
              <li>{{n.rating.average}}分，{{getaverage(n.rating.average)}}</li>
   
	          	 methods: {
				    getaverage(average){
				      if(average<3){
				        return "差劲"
				      }else if(average<7){
				        return "一般"
				      }else{
				        return "很好"
				      }
				    }
				  },


### vue 中 router-link  点击 的时候 排他加 颜色 
+  router-link  中有特有的  router-link-active 属性 直接给他加上就 ok    
         &.router-link-active{
          color: gold ;
          // border-bottom: 2px solid gold ;  
        }

+ 如果是给其子类添加  就用   &.router-link-active .子类的class名字 


### ::v-deep  可以深度穿透 修改掉其他组件的样式不可被修改的样式  



###   2个return   includes()  包含 item.title.includes(this.searchText)
+ 如果input 里面 输入的长度 不是 0 就让下面的展示框显示  并且 返回 一个 与名字匹配的对象
        if(this.searchText && this.hotList.length != 0){
        // 显示
        this.searchShow = true

        return this.hotList.filter(item =>{
+ 返回 一个数组 电影名包含的 input中的字 的数组             
          return item.title.includes(this.searchText)
        })


###foreach()  方法用于调用数组的每个元素，并将元素传递给回调函数。