# 富文本   
## 1 surmon-china/vue-quill-editor

> npm install vue-quill-editor --save
> 主要 cnpm install tui-editor@1.3 --save    引入 tui-editor文件夹  组件声明一下即可  
> 
####### quill  小解决图片问题 弹出一个 url填写连接 传图片
 
       var quill = new Quill('#editor', {
            theme: 'snow',
            modules: {
                toolbar: {
                    container: toolbarOptions,
                    handlers: {
                        image: imageHandler
                    }
                }
            },
        });

        function imageHandler() {
            var range = this.quill.getSelection();
            var value = prompt('What is the image URL');
            if(value){
                this.quill.insertEmbed(range.index, 'image', value, Quill.sources.USER);
            }
        }
 
+  实践  
    <quill-editor ref="quillEditor" :content="content"
                :options="editorOption"
                @change="onEditorChange($event)">
     </quill-editor>

+在页面渲染完以后
     mounted(){
	    //获取到了quill对象 
	    this.quill = this.$refs.quillEditor.quill;
	    console.log(this.quill)
	    //动态的修改了富文本的img的功能
	    this.quill.getModule('toolbar').addHandler('image', this.imageHandler)
     },
     
	   imageHandler(){
	      var range = this.quill.getSelection();
	      var value = prompt('What is the image URL');
	      if(value){
	          this.quill.insertEmbed(range.index, 'image', value);
	      }
	    },

##  2   mockdown
> 引入文件夹  
> components: {
    MarkdownEditor
  },

      <div class="mockFu">
          <Tinymce v-model="content" :id="'newsEditor'" v-show="ifshow==this.form.editStyle"></Tinymce>
          <MarkdownEditor ref="markdown" v-model="content" v-show="ifsow==this.form.editStyle"></MarkdownEditor>
        </div>



# input 聚焦 失焦 变换 不可编辑    
+ this.$set 等同于 vue.set    设置item中有一个新的属性   后来添加的属性
		  getUploadListCom() {
		      var res = this.uploadList.map(item => {
		        this.$set(item, "isSelect", false);
		        this.$set(item, "isEdit", false);
		        return item;
		      });
		      return res;
		    }
+ input 框
          <el-input
              type="text"
+ ref 起名为 o.id
              ref="o.id"          
              :disabled="!o.isEdit"
              v-model="o.title"
              @change="confirmTitle(o)"     变化的时候
            ></el-input>  
+ 点击 button的时候 input可以编辑
                  <el-button
                      @click="titleEdit(o,index)"
                      type="success"
                      size="samll"
                      icon="el-icon-edit"
                    ></el-button>

+ 点击编辑按钮的方法
		    titleEdit(o,index) {
		          // item.isEdit = false;    :disabled="!o.isEdit" 是否可以编辑 
		      this.materialList.map(item => {
		        item.isEdit = false;       isEdit 为false
		      }) ; 
		      o.isEdit = !o.isEdit;        为true  可编辑
           
+ 执行完毕后 聚焦
		      this.$nextTick(() => { 
		        this.$refs["o.id"][index].focus();    
		      });
		    },

+    input 变化的时候   按enter键位的时候
		    confirmTitle(o) {
		      this.uploadTitle(o);
		      o.isEdit = false;         变为true 不可 编辑
		    }, 

+  更新 title    使用api更新
		    uploadTitle(o) {
		      var { title, id } = { ...o };
		      var data = { title, id };
    	      materialApi.updateTitleList(data).then(res => {});
		    },

## 图片 ele 展示  用插槽
      <el-table-column  label="封面图片" width="150">
             <template slot-scope="scope">
               <img :src="scope.row.cover" width="130" height="180">
             </template> 
          </el-table-column>

##  富文本mockdown 查看信息显示为相同的 不会改变 解决方案 加:key   ="this.temid"  

     <div class="mockFu">
          <Tinymce :key= "this.temid" v-model="form.content1" :id="'newsEditor'" v-show="ifsow==this.form.type"></Tinymce>
          <MarkdownEditor :key= "'_'+this.temid" ref="markdown" v-model="form.content1" v-show="ifshow==this.form.type"></MarkdownEditor>
        </div>

     openDialog(id) {
      this.show = true;
      if (id) {
        newsApi.detailNewsList({ id }).then(res => {
          this.form = _.cloneDeep(res.data) ;
          this.temid = new Date().getTime() ;
          //console.log("123456",this.temid)
        });
      }
    },

### 本地上传封面

         <el-form-item label="本地上传封面" prop="cover">
                <el-upload
                  class="avatar-uploader"
                  action="/admin/xy/upload/uploadImg"
                  :show-file-list="false"
                  :on-success="handleAvatarSuccess"
                >
                  <img v-if="imageUrl" :src="imageUrl" class="avatar" />    显示图片
                  <i v-else class="el-icon-plus avatar-uploader-icon"></i>  
                </el-upload>
              </el-form-item>

+  图片上传成功的时候     让form对象中的cover 为  res.url 连接
         
		    handleAvatarSuccess(res, file) {
		      this.imageUrl = URL.createObjectURL(file.raw);
		      this.form.cover = res.url  
		    },   

######  正则校验http开头的 遍历修改图片为 http://59.110.138.169/media/123.jpg 

          var reg = /^http/i ;
          res.data.list.map(item => {
            if (!reg.test(item.cover)) {
              item.cover = this.test + item.cover ;
            }
            // return item ;
          });

##素材库上传图片  点击图片  选中状态
### 点击图片checkd 选中传出   通过v-model="o.statue"  选中了为true没选择为false   
      <img width="100%"  @click="o.statue=!o.statue"  height="240" :src="o.fileName" class="image" />

+ 添加  statue  属性
        res.data.list.map(item => {
            if (!reg.test(item.fileName)) {
              item.fileName = Url.host + "media/" + item.fileName;
              // console.log("1234546==>",item.fileName)
            }
            this.$set(item, "statue", false);
          });

          this.materialList = res.data.list;
      <el-checkbox v-model="o.statue" :label="o.fileName" :key="o.id" ></el-checkbox>

+  在点击确定的时候   过滤出选中的数组传给 父类  

	     submit(){
	         var res = this.materialList.filter(item=> item.statue == true)
	         this.$emit("updialog", res);   把res给父类组件 
	     },
+ 父类组件中 需要先有个方法 
 
	    <coverTail ref="covertail" @updialog='updialog'></coverTail>
	
	    updialog(res){
	       this.imageUrl = res[0].fileName ; 
	     },

#登录,不同角色,不同权限   
+ 路由里面设置导航守卫   meta: {roles:['editor'], title: '学生管理'} , //希望只能被admin访问
+ router里面
		    {
		     path: '/xy',
			    component: Layout,
			    redirect: '/xy/student',
			    name: 'xy',
			    meta: { title: '学员管理', icon: 'example' },
			    children: [
			      {
			        path: 'student',
			        name: 'student',
			        component: () => import('@/views/xy/student/index'),
			        meta: {roles:['admin'],title: '学生管理' } , //希望只能被admin访问
			      },
			      {
			        path: 'class',
			        name: 'class',
			        component: () => import('@/views/xy/class/index'),
			        meta: { title: '班级管理', icon: 'tree' }
			      }
			    ]
		     },

+ permission.js

			     //获取用户名
			      const hasGetUserInfo = hasToken.username;
			      if (hasGetUserInfo) {
			        //判断是否具有相关权限
			        // 如果to.meta.roles 有内容 则判断,没有则不是敏感信息 随便访问
			        if(to.meta.roles){            roles信息  在local storage 中  为字符串形式
			          // 这是路由要求验证的角色们 ['admin','editor']
			          var roles = to.meta.roles;
			          // 这是当前登陆用户的角色们 ['admin','vip']
			          var myRoles = hasToken.roles.split(',');
			          console.log('rolse',roles);
			          //什么情况下才能通过?
			          var commonRoles = _.intersection(roles,myRoles);
			          if(commonRoles.length>0){
			            next();
			          }else{
			            next('/404');
			          }
			
			        }else{
			          next()
			          NProgress.done()
			        }
			
			       
			
			      } else {
			        next(`/login`)
			        NProgress.done()
			      }
			    }