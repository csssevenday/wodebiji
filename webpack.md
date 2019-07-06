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
+ 