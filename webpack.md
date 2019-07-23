#webpack 安装步骤 学习  cnpm 与npm 不要混装

+ 全局安装 webpack   
  -- npm install --global webpack 

+ 新建文件夹 拖到编辑工具     npm init   生成一个 package.json 的文件
+ 编辑器里面安装 webpack版本    npm install --save-dev webpack
+ 以及需要以来的 cli            npm install --save-dev webpack-cli

+ 建立webpack.config.js文件夹 内容去 使用配置一个文件中 辅助粘贴 
+ 建立文件夹 |- /dist
		      |- index.html
		    |- /src
		      |- index.js      在创建一个 bundle 文件下   辅助粘贴 
+ 安装 lodash       npm install  lodash --save
+ 写css样式 的话引入 npm install --save-dev style-loader css-loader
+ index.js中引入   
     -- import './style.css' ; 
+ css写在  src 中  src 开发的东西写里面  
+ 并且 webpack.config.js中  要引入 固定样式   复制粘贴
+ 引入图片 把图片放在文件夹下    
     --npm install --save-dev file-loader 
+index.js中引入 
   --import Icon from './pp.png'
+ 打包 
  --npm run build 
+ 背景图片 直接在css中 写background-image:url("pp.jpg")

+ 字体  同样

## 管理输出     src\ 下的 js  为入口文件   入口(entry)
  src 下建立
   |- print.js 

+  下面按文档配置    可以把2个 入口的文件都给打包输出掉 

######设定 HtmlWebpackPlugin  能够自动更新检测你的更改 生成需要输出的东西      插件(plugins)
+  -- npm install --save-dev html-webpack-plugin
+  按文档配置    暂时只增加webpack.json中的东西 

#######清理dist 清理一些不必要的输出口 中的东西 
######升级了 要看英文文档
  --npm install clean-webpack-plugin --save-dev
+  webpack.json中 变为 const { CleanWebpackPlugin } = require('clean-webpack-plugin');

+ 引入图片的 webpack.json 的包  即可加入图片 


# webpack是一个打包模块化javascript的工具

+  WebPack可以看做是模块打包机：它做的事情是，分析你的项目结构，找到JavaScript模块以及其它的一些浏览器不能直接运行的拓展语言（Scss，TypeScript等），并将其打包为合适的格式以供浏览器使用。
+  
+  模块热更新是webpack的一个功能，他可以使得代码修改过后不用刷新浏览器就可以更新，是高级版的自动刷新浏览器。
+  
+  Gulp/Grunt是一种能够优化前端的开发流程的工具，而WebPack是一种模块化的解决方案，不过Webpack的优点使得Webpack在很多场景下可以替代Gulp/Grunt类的工具。               
+  
+  Tree-shaking可以用来剔除javascript中不用的死代码，它依赖静态的es6模块化语法，例如通过import 和export 导入导出，Tree-shaking最先在rollup中出现，webpack在2.0中将其引入，css中使用Tree-shaking需要引入Purify-CSS

+ 几个常见的loader 
		
		file-loader：把文件输出到一个文件夹中，在代码中通过相对 URL 去引用输出的文件
		url-loader：和 file-loader 类似，但是能在文件很小的情况下以 base64 的方式把文件内容注入到代码中去
		source-map-loader：加载额外的 Source Map 文件，以方便断点调试
		image-loader：加载并且压缩图片文件
		babel-loader：把 ES6 转换成 ES5
		css-loader：加载 CSS，支持模块化、压缩、文件导入等特性
		style-loader：把 CSS 代码注入到 JavaScript 中，通过 DOM 操作去加载 CSS。
		eslint-loader：通过 ESLint 检查 JavaScript 代码
		
+ 几个常见的plugin
		
		define-plugin：定义环境变量
		terser-webpack-plugin：通过TerserPlugin压缩ES6代码
		html-webpack-plugin 为html文件中引入的外部资源，可以生成创建html入口文件
		mini-css-extract-plugin：分离css文件
		clean-webpack-plugin：删除打包文件
		happypack：实现多线程加速编译

+		入口(entry)
+		
     		来指定一个入口起点,指示 webpack 用哪个模块,构建 内部依赖图 , 进入入口起点后，webpack 会找出有哪些模块和库是入口起点（直接和间接）依赖的。最后输出到 bundles 的文件中，

+		输出(output)
+		
		        告诉 webpack 在哪里输出它所创建的 bundles，以及如何命名这些文件
]
+		loader    
+		     loader 将所有类型的文件转换为 webpack 能处理的有效模块，然后你就可以利用 webpack 的打包能力，对它们进行处理。
+	 本质上，webpack loader 将所有类型的文件，转换为应用程序的依赖图（和最终的 bundle）可以直接引用的模块。     
+	     
 +	   常见的几个
          	file-loader：把文件输出到一个文件夹中，在代码中通过相对 URL 去引用输出的文件
			url-loader：和 file-loader 类似，但是能在文件很小的情况下以 base64 的方式把文件内容注入到代码中去
			source-map-loader：加载额外的 Source Map 文件，以方便断点调试
			image-loader：加载并且压缩图片文件
			babel-loader：把 ES6 转换成 ES5
			css-loader：加载 CSS，支持模块化、压缩、文件导入等特性
			style-loader：把 CSS 代码注入到 JavaScript 中，通过 DOM 操作去加载 CSS。
			eslint-loader：通过 ESLint 检查 JavaScript 代码

+		插件(plugins)  常见的几个
+     loader 被用于转换某些类型的模块，而插件则可以用于执行范围更广的任务。插件的范围包括，从打包优化和压缩，一直到重新定义环境中的变量。插件接口功能极其强大，可以用来处理各种各样的任务。
    
		        define-plugin：定义环境变量
				terser-webpack-plugin：通过TerserPlugin压缩ES6代码
				html-webpack-plugin 为html文件中引入的外部资源，可以生成创建html入口文件
				mini-css-extract-plugin：分离css文件
				clean-webpack-plugin：删除打包文件
				happypack：实现多线程加速编译

