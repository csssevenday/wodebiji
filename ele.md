#豆瓣用element与vue的形式 包括分页 

### 运用了 单独api 

		import axios from "axios" 

		 function getMovieList(type,start) {
		  var url = "http://www.bufantec.com/api/douban/movie/"+type+'?start='+start+'&limit='+5 ;
		 
		  return axios.get(url) ;
		}

		export default {
		  getMovieList
		} 
+ 其中 type 为传进来 in_theaters  , coming_soon , top250  
+ start 为 要跳到的 页数   limit 为每页显示的条数 
+ 点击切换 type的时候 需要 执行 获取 api的方法 并且 传入 type 与 start

### 点击页数 跳转到 不同页 的时候  ele 有特定的写法 
+  @current-change="catpage"     调用catpage 方法 即可 
		   catpage(v) {
		      // 跳到哪一页
		      this.start = v;
		      this.getMovieList(this.type,this.start);  //调用api清单
		    },
        
 + ele 加loading   v-loading="loading"  请求之前让显示 请求之后隐藏 
        getMovieList(type, start) {
	      this.loading = true;    
	      setTimeout(() => {
	        movieListApi.getMovieList(type, start).then(res => {
	          this.movieList = res.data.data; //电影清单
	          this.pages = Math.ceil(res.data.count / this.limit); //总页数
	          this.loading = false;
	        });
	      }, 200);
	    },
         
+  :page-count="pages"           为显示的可以点击的页数 



###  有时候data 对象的下层还需要 特地声明 一下 直接写在对象里面
    oneList: {
        images: "",
        casts: ""
      },



## $nextTick() 

在Vue生命周期的created()钩子函数进行的DOM操作一定要放在Vue.nextTick()的回调函数中

在created()钩子函数执行的时候DOM 其实并未进行任何渲染，而此时进行DOM操作无异于徒劳，所以此处一定要将DOM操作的js代码放进Vue.nextTick()的回调函数中。与之对应的就是mounted()钩子函数，因为该钩子函数执行时所有的DOM挂载和渲染都已完成，此时在该钩子函数中进行任何DOM操作都不会有问题 。


#后台 登录  方面   从local存储 简化了 

###  需要 一个 登录 api   login.js  api
  
            // 引入封装好的axios
			import request from './request'  
			
			//执行登录
			function doLogin(data){
			  return request ({
			    url: '/admin/login/doLogin',  //相对路径
			    method:'post',  // get/post
			    data  // 固定写法
			  })
			}
			
			//获取用户明细
			function getUserInfo(data){
			    return request ({
			      url: '/admin/login/getUserInfo',  //相对路径
			      method:'post',  // get/post
			      data  // 固定写法
			    })
			  }
			
			export default {
			    doLogin,
			    getUserInfo
			}
+  为了省略前面的  http://59.110.138.169   所以封装了一个 axios 的方法      api/request.js
 
	// axios的封装 为了可以方便的统一的使用axios做数据请求
		import axios from 'axios'
		import qs from 'qs'
		import { Message, MessageBox } from 'element-ui'
		import router from '@/router'
		// create an axios instance
		// axios.defaults.withCredentials = false;
		const service = axios.create({
		  withCredentials:false,
		  baseURL: process.env.BASE_API, // api的base_url
		  timeout: 8000 // request timeout
		})
		
		// request interceptor
		service.interceptors.request.use(config => {
		  return config
		}, error => {
		  // Do something with request error
		  console.log(error) // for debug
		  Promise.reject(error)
		})
		
		// respone interceptor
		service.interceptors.response.use(
		  // response => response,
		  /**
		   * 下面的注释为通过在response里，自定义code来标示请求状态
		   * 当code返回如下情况则说明权限有问题，登出并返回到登录页
		   * 如想通过xmlhttprequest来状态码标识 逻辑可写在下面error中
		   * 以下代码均为样例，请结合自生需求加以修改，若不需要，则可删除
		   */
		  response => {
		    const res = response.data
		    if (res.tokenCode == 5000) {
		      Message({
		        message: '请重新登录!' ,
		        type: 'error' ,
		        duration: 5 * 1000
		      })
		      localStorage.removeItem('ms_username') ;
		      router.push('/login')
		      return Promise.reject('error')
		    } else {
		      return res
		    }
		  },
		  error => {
		    console.log('err' + error)   // for debug
		    return Promise.reject(error) 
		  })
		function http(config){          
		  if(config.method.toLowerCase() === 'post'){
		    config.data = qs.stringify(config.data,{arrayFormat: 'repeat',allowDots: true,allowDots: true}) ; 
		  }else{
		    config.params = config.data ;
		  } 
		  return service(config);
		}
		
		export default http;

+ 代理 中此设置   把以 / 开始的 转换为 以http://59.110.138.169开始的 还可以实现跨域  
  
    devServer{    // 开发特有的 模式 
     proxy{
      '^/': {       //  /admin/lgoing ==> http://localhost/admin/lgoing 
         target: `http://59.110.138.169`,
         changeOrigin: true,
         pathRewrite: {                
        }
      }
+ 开始 验证码了  url.js
 
		   export default {
		       imgCode: 'http://59.110.138.169/admin/login/imgCode'
		   }
##### 验证码图片 
+ 在登录页面  login/index.vue 中引入   import Url from "@/api/url.js";    
+ 页面中  
 
		       <el-input
		          v-model="loginForm.yan"
		          placeholder="验证码"
		          class="yan-input"
		          name="yan"
		          type="text"
		        />
		        <img @click="refreshImg" class="yan-img" :src="imgCode" alt>
  
	     data() {  
	         imgCode: " " ,
	 		 loginForm: {
			        username: "admin",
			        password: "123456",
			        yan: ""
			      },
	         }

+   点击刷新验证码    细节  后面跟时间戳 
 
	    refreshImg() {
	      //    /admin/login/imgCode?ts=1234234
	      this.imgCode = Url.imgCode + "?ts=" + new Date().getTime();
	    },

#####  登录拦截  验证登录信息 用户名 密码 与 验证码
+  引入       import LoginApi from "@/api/login";	
+  拦截设置    
+    ...this.loginForm.username 解构出来就为 username:this.loginForm.username
+    ...this.loginForm    解构出来就是  loginForm的完整对象 
+   验证表单信息 有就登录    
	    handleLogin() {
	      this.$refs.loginForm.validate(valid => {
	        //表单验证通过
	        if (valid) {     
	          LoginApi.doLogin({
	            // username:this.loginForm.username,
	            ...this.loginForm 
	          }).then(res => {
	            if(res.code == 'S'){       //如果为S 登录成功 需要手动跳转 
	              // Message element的组件  可以通过this.$message获取
	              this.$message({
	                message: '恭喜登陆成功,正在获取用户数据...',
	                type: 'success'
	              });
	              //登陆成功后 需要获取用户明细    头像 id 存到本地方便下次登录 
	              LoginApi.getUserInfo()
	                .then(res=>{
	                  // console.log('dd==>',res);
	                  //简化了 这里不需要用vuex
	                  var saveUser = {
	                    avatar:res.avatar,
	                    userId: res.user.id,
	                    username: res.user.username
	                  }   
	                  // 存储到本地localStorage
	                  setToken(saveUser) ;
	                  // 手动跳转   vue $router
	                  this.$router.push({name:'Dashboard'})
	                })
	
	
	            }else{
	              this.$message.error('登陆失败!');
	            }
	            
	          });
	        } else {
	        }
	      });   


+ 需要吧token值存到 local 中去  然后登录req请求带上token值     utils/myAuth.js 
 + Cookies 为一个库  
        import Cookies from 'js-cookie'
		const TokenKey = 'vue_admin_template_token'
		
		export function getToken() {
		    // 字符串类型
		  var res = localStorage.getItem(TokenKey);
		  if(res){
		      res = JSON.parse(res);
		  }else{
		      res = undefined;   如果为空 会有bug
		  }
		  return res;
		}
		
		export function setToken(obj) {
		    // setItem 必须是字符串
		    localStorage.setItem(TokenKey,JSON.stringify(obj));
		}
		
		export function removeToken() {
		  localStorage.removeItem(TokenKey) ;
		}

+  通过这一步 存到local中  import {Token} from '@/utils/myAuth';
  
+ 跳转 
+ 
+ import { getToken } from '@/utils/myAuth'     // get token from cookie  
+     permission.js下
#### const whiteList = ['/login']   白名单 不需要验证就可以进去登录页   
#####redirect 默认那一页
      获取token值
          const hasToken = getToken()   
			  if (hasToken) {
			    console.log('hasToken',hasToken);
			    if (to.path === '/login') {
	// if is logged in, redirect to the home page   redirect:"/dashboard" 默认页
			      // next({ path: '/' })
			      NProgress.done()       页面进度条关闭
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
			})

##### 登录以后的 图片头像 
+  import {getToken} from '@/utils/myAuth'    //navbar.js
+  getToken 为函数 所以为 getToken() 执行  
+  created(){
    this.getUser();
  },
+    methods: {
    getUser(){
      this.user = getToken() || {};
    },

#### 如何只写 一个 http://59.110.138.169  
+  export default {                          api/url.js中   /imgApi/admin/login/imgCode
    imgCode: '/imgApi/admin/login/imgCode'
}

+  '^/imgApi':{                               //让以  ^/imgApi  转换为  http://59.110.138.169 
        target:'http://59.110.138.169',      //会代替为 http://59.110.138.169/admin/student/list
        // target:'http://192.160.0.100',
        changeOrigin:true,
          pathRewrite: {
          '^/imgApi': '' // 替换api中的部分字符为另一个字符
        }

####  退出  
+先在 api/login.js 写 退出方法 
		 function doLogOut(data) {
		  return request({
		    url: '/admin/login/doLogOut',
		    method: 'get',
		    data
		  })
		}

+ src/logout/Navbar.vue   中
 
+ import loginApi from '@/api/login'     
+ import {removeToken} from '@/utils/myAuth'   引入删除localstorage的 东西
 	    methods: {
			logout() {
			      // 1.发送到服务器退出    服务器清除相应的 session
			      loginApi.doLogOut()
			        .then(res=>{
			        })

			      // 2.本地删除localstorage   的token
			      removeToken();

			      // 3. 强制跳转 到登录页 
			      this.$router.replace({name:'login'})  
			    }

+  loginApi.doLogOut  的 内容为      '@/api/login'
		 function doLogOut(data) {
		  return request({
		    url: '/admin/login/doLogOut',
		    method: 'get',
		    data
		  })
		}
+ '@/utils/myAuth'  删除 localstorage 的 token
		export function removeToken() {
		  localStorage.removeItem(TokenKey);
		}

#### api的分页   ele     
  xy/student/detail/index.vue  中 
+ 引入
   <el-pagination
          class="pagination"
          @size-change="handleSizeChange"           // pageSize    每页的条数 改变时会触发  
          @current-change="handleCurrentChange"     // currentPage  当前页    改变时会触发	
          :current-page="page.start"                // 开始的页数
          :page-sizes="[5,10,15]"                   // 选择每页显示 几条 
          :page-size="page.limit"                   // 每页的条数
          layout="total, sizes, prev, pager, next, jumper"
          :total="page.totalCount"                  //总条数
        ></el-pagination>
        >
+ created() {
    //初始化宿舍和班级信息
    this.getStudentList();    学生信息
  },
+ data  {
      return { 中
			 page: {
			        start: 1,      //当前页
			        limit: 5,      // 每页大小
			        totalCount: 0, //总数
			        totalPage: 0   // 总页数
			      },
			 }
		}
+  methods: {
     getStudentList() {   
       this.loading = true;        进来时显示  loading
      var { start, limit } = this.page;   //解构写法   让start为start   limit为limit

       StudentApi.getStudentList({        获取学生明细的 
        start,       start:start     让start为 1 
        limit,       limit:limit     让limit 为 上面的5
	  }).then(res => {

		        Object.assign(this.page, {     合并 到 page中去 让分页得以显示
		          limit: res.data.pageSize,         为每页显示几条
		          totalPage: res.data.totalPage,    总页数
		          totalCount: res.data.totalRow     总条数
		        });

		        this.studentList = res.data.list;
		        this.loading = false ;          加载完毕loading结束
		      });
		   },
     
 // 点击 123 页数 跳转到 123 页  
    handleCurrentChange(val) {
      //先改变page对象
      this.page.start = val 
      this.getStudentList()    点击的时候重新 获取信息 
    },

 //页码大小发生变化触发   点击每页多少条的时候 让每页显示多少条
    handleSizeChange(val) {
     // alert(val);
      this.page.limit = val ;
      this.getStudentList();
    },

#### 搜索 功能 上线
+ 先有个  通过班级列表进行 搜索的api     http://{{host}}/admin/xy/clazz/list     @/api/clazz
+ 再有个  通过宿舍列表进行 搜索的api     http://{{host}}/admin/xy/dorm/list      @/api/drom
 
+ 班级的	 // 引入封装好的axios
		import request from './request'
		
		//获取班级列表   的 api 请求
		function getClassList(data){
		  return request ({
		    url: '/admin/xy/clazz/list',  
		    method:'get',  
		    data  
		  })
		}
		
		export default {
		    getClassList,
		}
 + 宿舍的 // 引入封装好的axios
			import request from './request'
			
			//获取用户列表
			function getDormList(data){
			  return request ({
			    url: '/admin/xy/dorm/list',  
			    method:'get',  
			    data  
			  })
			}
			
			export default {
			  getDormList,
			}

+ import ClassApi from "@/api/clazz";     student/index 引入 上面的api请求   
+ import DormApi from "@/api/dorm";  
  
		 data{  
		        classList: [] ,
		        dormList:  []
		   }
+ 获取 班级 与 宿舍 列表信息
 
       methods: {
         getClassList() {                       
	      ClassApi.getClassList().then(res => {
	        this.classList = res.data.list;    
	      });                                  
	    },                                     
	    getDormList() {                        
	      DormApi.getDormList().then(res => {  
	        this.dormList = res.data.list;     
	      });                                  

+ 让input 变为可以下拉的选择的选择框 
 +班级的  

             <el-select v-model="searchForm.classId" clearable placeholder="请选择">  input显示的字
               <el-option
                  v-for="item in classList"      遍历
                  :key="item.id"                 
                  :label="item.className"        下拉显示的内容
                  :value="item.id"         
                ></el-option>
            </el-select>

 + 宿舍的 
  
        <el-select v-model="searchForm.dormId" clearable placeholder="请选择">
                <el-option
                  v-for="item in dormList"
                  :key="item.id"
                  :label="item.name"
                  :value="item.id"
                ></el-option>
         </el-select> 

	    data() {
	     return {
		      searchForm: {
		        classId: "",
		        dormId: ""
		      },

+ 开始methods   还原搜索框     封装成公共方法
    this.$options.data()  能获取  this.data  对象的原始数据    把data(){}  里面的信息全部获取到
   

    /**
	 *   还原vm中的  原始(data)数据 对象                 utils/index
	 */     
                        
			export function resetData(vm,key){
			  vm[key] =  vm.$options.data()[key];
			}

+ 引入 import { resetData } from "@/utils/index";    这个方法 

运用 就是一行代码

    methods:{
     doSearch() {
      // 1. 还原page的搜索条件
      // this.$options.data()能获取this.data对象的原始数据
      // console.log('==>',this.$options.data().page);
      // this.page = this.$options.data().page;
      resetData(this, "page");
      // 2. 添加搜索条件
      this.getStudentList();
    },

+ 搜索条件在请求学员数据的时候一起调用
 
       getStudentList() {
          //搜索的查询条件
         var searchObj = this.searchForm;       searchForm: {
                                                            name:    "" , 根据名字查询
													        classId: "" , 根据班级查询
													        dormId:  ""   根据宿舍查询
													      },
     //  排除没有值的内容
      var searchObj = _.pickBy(searchForm, item => item);

      StudentApi.getStudentList({
        start,
        limit,
        ...searchObj      解构加入 
      }).then(res => {
        Object.assign(this.page, {
          limit: res.data.pageSize,          
          totalPage: res.data.totalPage,  
          totalCount: res.data.totalRow    
        });
        this.studentList = res.data.list;
        this.loading = false;
      });

+  为了防止输入的内容为空 用lodash 加 webpack的方式  解决
先 cnpm install lodash --save 
+ 全局添加lodash 的方法       在 vue.config.js 中

 + 最上方需要先引入webpack         const webpack = ire('webpack')
  
						          configureWebpack: {  
									    plugins: [
									      new webpack.ProvidePlugin({
									        _:"lodash"   
									        })
									    ], }

            // 排除没有值的内容             
      searchObj = _.pickBy(this.searchForm, item => item);

#### 重置

+ 让 匹配的 id与name 为空  就会匹配到全部的数据 然后调用  this.getStudentList() 获取数据  resetData(this, "page")为第一页
   
  doOld(){ 
      this.searchForm = {
        name: '' ,
        classId: '',
        dormId: '' ,
      }
      resetData(this, "page");
      this.getStudentList() ;
    },

###    interceptor   拦截器

		const service = axios.create({           //service 是 axios的对象
			  withCredentials:false,
			  baseURL: process.env.BASE_API, // api的base_url
			  timeout: 8000 // request timeout
		})     
                                                              request
			service.interceptors.request.use(config => {   //在请求发出之前 做的事 request/rɪ'kwɛst/请求   向后台请求数据 
			  return config
			}, error => {
			  // Do something with request error
			  console.log(error) // for debug
			  Promise.reject(error)
			})                                   
                                                   response
		service.interceptors.response.use(      //在请求过来之后做的事  后台返回为                  										response /rɪ'spɑns/ 响应
		  // response => response,
		  /**
		   * 下面的注释为通过在response里，自定义code来标示请求状态
		   * 当code返回如下情况则说明权限有问题，登出并返回到登录页  
		   * 如想通过xmlhttprequest来状态码标识 逻辑可写在下面error中  
		   * 以下代码均为样例，请结合自生需求加以修改，若不需要，则可删除  
		   */
		  response => {              
		    const res = response.data            
		    if (res.tokenCode == 5000) {        //如果为 5000   删除token的值 跳转到首页
		      Message({
		        message: '请重新登录!',
		        type: 'error',
		        duration: 5 * 1000
		      })
+   表头需要引入    import {removeToken} from '@/utils/myAuth'
		      removeToken();                  //  删除 token的值
		      router.replace({name:'login'})  // 手动跳转到登录页
		      return Promise.reject('error')  
		    } else {
		      return res       正常返回res
		    }
		  },
		  error => {
		    console.log('err' + error) // for debug
		    return Promise.reject(error)
		  })
+   encodeURI('刘') 加密      decodeURI("%e5")  解密 

### 添加功能  

   添加功能 写出了 一个组件   
  
   组件引入 3 步
          <!-- 编辑页面 -->   
    <Detail :isEdit="isEdit" :classList="classList" :dormList='dormList' ref="edit"></Detail>

    import Detail from './detail/Detail' 
   
    components:{
	    Detail
	 },

#### 点击添加   让其调用子组件 
 
     <Detail :isEdit="isEdit" :classList="classList" :dormList='dormList' ref="edit"></Detail>

+  goAdd(){
      //调用子组件的方法                // ref=edit 
      this.$refs.edit.openDialog();    //  openDialog  为子组件的方法
    }

+ 子组件的方法
	   methods: {
		  openDialog() {
		    this.show = true;
	       },
       }

    <el-dialog
      :show-close="false"
      :title="titleCom"
      :visible.sync="show"      是否显示弹窗
      width="70%"
      @close="handleClose">
  
### 日历表 
            <el-col :span="8">
               <el-form-item label="入住日期">
                <el-date-picker                      
	                  value-format="yyyy-MM-dd"    //展示的样式2018-10-11用什么连                								 接就是什么样式
	                  v-model="form.dormStartTime" //是为了往form中添加一个属性
	                  type="date"
	                  placeholder="选择入住时间"
                ></el-date-picker>
               </el-form-item>
             </el-col>

### 往 弹出列表中添加 班级  宿舍 的信息   

     <Detail :isEdit="isEdit" :classList="classList" :dormList='dormList' ref="edit"></Detail>
  
      :classList="classList" :dormList='dormList'  
    
      getClassList() {
	      ClassApi.getClassList().then(res => {
	        this.classList = res.data.list;
	      });
     },
       getDormList() {
	      DormApi.getDormList().then(res => {
	        this.dormList = res.data.list;
	    });

+ 子组件中    接受
         props: {
		    classList: Array,
		    dormList: Array 
		  },

       <el-col :span="8">
              <el-form-item label="班级" prop="classId">
                <el-select v-model="form.classId" placeholder>
                  <el-option
                    v-for="item in classList"
                    :key="item.id"           
                    :label="item.className"  
                    :value="item.id"
                  ></el-option>
                </el-select>
              </el-form-item>
        </el-col>

###  城市列表 
       npm install element-china-area-data -S 

+     import { regionData } from 'element-china-area-data'
    
        data () {
	      return {
	        options: regionData,
	        selectedOptions: []
	      }
	    },

+ html 引入       
       <el-cascader
	       size="small"
	       :options="options"
	       v-model="selectedOptions"
	       @change="handleChange">
       </el-cascader>

+   就会有城市 数据 

+ 需要对城市数据进行转换为提交给后台  join() 方法用于把数组中的所有元素放入一个字符串。
    handleCityChange(value) {
        this.form.city = value.join(",");
    },
+ 后台想呈现在页面显示又必须转换为数组的形式  
+ 在获取学生数据的时候 同时对城市信息进行 转换 item.city = item.city.split(","); 
    StudentApi.getStudentList({
        start,
        limit,
        ...searchObj     
      }).then(res => {
        res.data.list.map(item => {
          if(item.city) {
            item.city = item.city.split(","); 
           // console.log( item.city);
            item.city = item.city.reduce((a,b) => {
                return a + "/" + CodeToText[b];
              },'').slice(1);
          }
        });

###   缴费信息 那一块        加到后台 的 不让修改   v-show='costCard' 刚开始为false

        <el-card shadow="never" class="form-card">
          <div slot="header">
            <span>交费信息</span>
            <el-button-group v-show="!costCard" class="cost-button-group">

              <el-button @click="costCard=true" type="text">添加费用记录+ 
              </el-button>
  
             </el-button-group>
          </div>
          <el-card class="cost-card" v-show="costCard" shadow="hover" style="margin-bottom:20px">
            <el-form :model="costForm" ref="costForm" label-width="80px">
              <el-row :gutter="20">
                <el-col :span="8">
                  <el-form-item label="类型">
                    <el-radio v-model="costForm.costType" label="0">学费</el-radio>
                    <el-radio v-model="costForm.costType" label="1">住宿费</el-radio>
                  </el-form-item>
                </el-col>
                <el-col :span="8">
                  <el-form-item label="金额">
                    <el-input type="number" :min="0" v-model="costForm.costValue" placeholder></el-input>
                  </el-form-item>
                </el-col>
                <el-col :span="8">
                  <el-form-item label="交费时间">
                    <el-date-picker
                      type="date"
                      value-format="yyyy-MM-dd"
                      v-model="costForm.costTime"
                      placeholder="选择日期时间"
                    ></el-date-picker>
                  </el-form-item>
                </el-col>
                <el-col :span="12">
                  <el-form-item label="备注">
                    <el-input
                      type="textarea"
                      :rows="2"
                      v-model="costForm.costBak"
                      maxlength="300"
                      show-word-limit
                      placeholder="请输入备注信息"
                    ></el-input>
                  </el-form-item>
                </el-col>
              </el-row>
              <el-row>
                <el-col :span="12" :offset="12" style="text-align:right;">
                  <el-button @click="handleCostCancel" style="margin-right:20px">取消</el-button>
                  <el-button @click="handleCostSave" type="primary">确定</el-button>
                </el-col>
              </el-row>
            </el-form>
          </el-card>

          <el-table :data="costList" border stripe>
            <el-table-column show-overflow-tooltip type="index" width="50"></el-table-column>
            <el-table-column show-overflow-tooltip prop="costType" label="类型" width="150">
              <template slot-scope="scope">{{scope.row.costType=='0'?'学费':'住宿费'}}</template>
            </el-table-column>
            <el-table-column show-overflow-tooltip prop="costValue" label="金额" width="150"></el-table-column>
            <el-table-column show-overflow-tooltip prop="costTime" label="时间" width="200"></el-table-column>
            <el-table-column show-overflow-tooltip prop="costBak" label="备注"></el-table-column>
            <el-table-column fixed="right" label="操作" width="100">
              <template v-if="!scope.row.id" slot-scope="scope">
                <el-button @click="delCostInfo(scope.row)" type="text" size="small">删除</el-button>
              </template>
            </el-table-column>
          </el-table>
        </el-card>

			data(){
			      costList: [], // 交费记录   需要展示的列表,包括以前提交过的数据对象  
                  costListNew: [], // 新增cost   需要提交的对象
			      costForm: {
			        costType: "0", //默认0 学费 , 1 住宿费
			        costTime: "",
			        costValue: 0,
			        costBak: ""
			      },
                   
			}
+ 点击确定按键  把信息 给push进下面的表单中去 需要clone到一个新的数组中去 不然在打开缴费的时候是同一个数组会在刚才的数组上进行修改   会对需要提交的对象 以及 已经提交过得对象重新创建 为二个新的对象
		 handleCostSave() {
		      // 关闭
		      this.costCard = false;
		      //clone一个对象 否则会被清空
		      // {           浅克隆   {
		      //   a:[1234]   ==>         a:[1234]
		      // }                    }
		      // 深克隆    实现了obj2对obj的深度克隆
		      // var obj2 = JSON.parse(JSON.stringify(obj))
		      var costInfo = _.cloneDeep(this.costForm);
		      //新增一个tempid 方便删除
		      costInfo.tempId = new Date().getTime();
		      this.costListNew.push(costInfo); // 需要提交的对象
		      this.costList.push(costInfo);    // 需要展示的列表,包括以前提交过的数据对象
		      // 情况clone的对象
		      resetData(this, "costForm");
		    },
+ 页面信息中显示的是  costList  的信息 
+ 验证表单解构的是 costListNew  的信息   要提交给后台他们想要的数据 
         // _size: 2
			// xyCostItems_0:{
			//   costType: 0,
			//   costTime: 2019-06-19 00:00:00,
			//   costValue: 1234234,
			//   costBak: asfdsdf,
			//   tempId: 1561513126653
			// },
			// xyCostItems_1:{
			//   costType: 1
			//   costTime: 2019-06-26 00:00:00,
			//   costValue: 200,
			//   costBak: 这是住宿费,
			//   tempId: 1561514289909
			// }

			export function handlePostObjArr(key,obj){
			  if(obj.length == 0 ) return {}
			  var rsObj = {
			    _size: obj.length
			  }
			  for(var i = 0 ; i < obj.length ; i ++){    当key是动态信息的时候 用[]
			    rsObj[key+'_'+i]=obj[i];   
			  }
			  return rsObj;  
			} 
+  验证表单解构的是  input 输入的信息是否 合规
  
      this.$refs.form.validate(valid => {
        if (valid) {
          api({
            xyUser: this.form,       [key]          obj
            ...handlePostObjArr("xyCostItems", this.costListNew) //xyCostItems 必须字段
          }).then(res => {

+ 删除临时添加的交费记录  以前交过的不准删除 
     
    delCostInfo(row) {
      //注意lodash的remove方法不是响应式的
      console.log(row);
      this.costList = this.costList.filter(item => item.tempId != row.tempId);
      this.costListNew = this.costListNew.filter(
        item => item.tempId != row.tempId
      );
    }
######      刷新父类里面的方法
            this.$parent.getStudentList();
#####   调用子组件的方法
        this.$refs.edit.openDialog(id);

##编辑,查看,删除,功能


#### 编辑  

+ 调用与添加的同一个弹窗   但是传出一个scope.row.id出来    调用

+ 的方法  在子组件中进行编辑信息

    goEdit(id) {
      //调用子组件的方法
      this.$refs.edit.openDialog(id);
    },
######  子组件中  通过api获取新的信息 改变form 与 costList 让其显示在页面信息中
 
    openDialog(id) {
      this.show = true;
      if (id) {
        studentApi.detailStudent({ id }).then(res => {
          console.log(res.data)
            this.form = _.cloneDeep(res.data)
        });
        studentApi.costListStudent({ userId: id }).then(res => {
          console.log(res)
          this.costList = res.data
        });
      }
    },

### 删除   id的传递需要用{}的形式 

    delEdit(id) {         
      if (id) {
        this.studentList = this.studentList.filter(item => item.id != id);
        StudentApi.delStudent({ id });
      }
       this.getStudentList();
    }


#  下拉框选择男女
           <el-form-item label="性别">
                <el-select v-model="form.sex" placeholder="选择性别">
                  <el-option
                    v-for="item in sexOption"
                    :key="item.value"
                    :label="item.label"
                    :value="item.value"
                  ></el-option>
                </el-select>
              </el-form-item>


		       form: {
		        name: "",
		        sex: "0",
		        tel: "",
		        city:'' 
		      },
		
		    sexOption: [
		        {
		          label: "男",
		          value: "0"
		        },
		        {
		          label: "女",
		          value: "1"
		        }
		      ],



## 1.this.$router.push()

描述：跳转到不同的url，但这个方法回向history栈添加一个记录，点击后退会返回到上一个页面。

+ 2.this.$router.replace()

描述：同样是跳转到指定的url，但是这个方法不会向history里面添加新的记录，点击返回，会跳转到上上一个页面。上一个记录是不存在的。

+ 3.this.$router.go(n)

相对于当前页面向前或向后跳转多少个页面,类似 window.history.go(n)。n可为正数可为负数。正数返回上一个页面



## 向一个对象数组里面添加新的属性 + 将一个对象数组数据拿出来变成另一个对象

     var arry= [{a:11,b:22,c:33,d:44},{a:11,b:0,c:0,d:44},{a:11,b:22,c:99,d:99}];
     var arry2=[];
     arry.map(((item, index)=> {
       arry2.push(Object.assign({},item,{mess1:item.c,mess2:item.d}))
     }))
      console.log(arry2);    



##  深克隆  浅克隆
  所有元素或属性完全复制，与原对象完全脱离，也就是说所有对新对象的修改都不会映射到原对象中

  浅克隆
原始类型为值传递，对象类型仍为引用传递

函数
  函数是对象类型，但函数是一等公民，函数克隆通过浅克隆即可实现。
  **原因：**函数克隆会在内存中单独开辟一块空间，互不影响。

针对数组实现深复制
用数组的方法concat一个空数组

	var a = [1,2,3];
	var b = [].concat (a);
	a和b是两个数组
	
针对除函数外的深克隆
将对象序列化在解析回来

	var obj = {a:1,b:2};
	var newObj = JSON.parse(JSON.stringify(obj));
	obj和newObj是两个对象
![](https://i.imgur.com/LykFf7b.png)


###  数据拼接转换

  var arr =['张三',90,110,330] ;
  var type = ['name','yuwen','shuxue','lizong'];

转换为对象形式   因为type 与arr 是var出来的为变量 要有 []

    function foo(arr,type){
        var user={
           [type[0]]:arr[0] ,
           [type[1]]:arr[1] ,
		   [type[2]]:arr[2] ,
		   [type[3]]:arr[3] ,
           } 
          return user ;          
        }
  
## 解决跨域问题

     代理另一个最重要的作用: 解决跨域问题
      // 浏览器同源策略: A ==>(ajax)  B 的资源  由于浏览器的安全策略 是不允许直接访问的
      //  产生的问题是如何解决跨域问题:
             1. jsonp(了解,不用了)
             2. cors  https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS
                    // a) 后台配置的
             3. webpack 代理  可以包装本地请求,使目标主机无法判断是否是跨域请求
                    // a) 打包后不可用   devServer: {} 开发环境中
             4. nginx 代理解决跨域 


### session  id 是由服务器生成的  request请求  response响应
+ 图片
 
   ![](https://i.imgur.com/97MFVwL.png)

   1 把session 储存到内存中 
   2 把sessionid通过responent对象返回给客户端,然后把sessionid储存到cookie中
   2 cookie存在于客服端里面 每次客户端登录 request请求都会带上cookie值

## 父子通信调用 

###  父到子   

        <MySearch :classList="classList" :dormList="dormList" @do-search="doSearch"></MySearch> 
+ 子组件引入      
         props: {
		    classList: Array,
		    dormList: Array
		  },
+ 直接使用 classList   dormList   信息

### 子到父  

	   <el-button size="small" type="primary" @click="doSearch">查询</el-button>
	
	   doSearch() {
	      //告诉外部你的信息this.searchForm
	      this.$emit("do-search", this.searchForm);
	    },
父页面执行方法 @click="doSearch"
      doSearch(from) {
      // 1. 还原page的搜索条件
      // this.$options.data()能获取this.data对象的原始数据
      // console.log('==>',this.$options.data().page);
      // this.page = this.$options.data().page;
      resetData(this, "page");
      // 2. 添加搜索条件
      this.getStudentList(from);
    },

 
  
   