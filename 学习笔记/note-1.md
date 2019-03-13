## 比较webpack和其他工具

  Gulp/Grunt是一种能够优化前端的开发流程的工具，而WebPack是一种模块化的解决方案(一切皆模块)

  Grunt和Gulp的工作方式是：在一个配置文件中，指明对某些文件进行类似编译，组合，压缩等任务的具体步骤，task自动替你完成这些任务。

  Webpack的工作方式是：把你的项目当做一个整体，通过一个给定的主文件（如：index.js）
  Webpack将从这个文件开始找到你的项目的所有依赖文件，使用loaders处理它们，最后打包为一个（或多个）浏览器可识别的JavaScript文件。
  
  全局安装 (不推荐)(注意：项目目录名不能使用webpack，否则在初始化的时候会报错)
  npm install -g webpack

    ★注意：安装完成直接使用webpack命令，可能会提示'不是命令...'，这时候需要查看一下webpack的版本
    
      在webpack3中，webpack本身和它的CLI是在同一个包中，但在第4版中，将两者分开来以便更好地管理它们
    
    总结：如果webpack-cli是局部安装的，想要使用webpack命令必须进入node_modules/.bin/webpack才能执行webpack命令
         如果是全局安装的webpack-cli，就不需要进入bin目录，webpack就能够寻找到它的命令路径了
 
 ## package.json文件的作用   
  package.json是一个标准的npm说明文件，里面包括当前项目的依赖模块，自定义的脚本任务等等
  所以在拷贝项目的时候，node_modules文件夹就不需要了（一般很大），只要有package.json文件，直接使用 npm -i 安装依赖模块即可
  
  在终端中使用 npm init -y 命令可以自动创建这个package.json文件，如果不准备在npm中发布你的模块，输入 npm init -y 即可
  这些准备工作就绪之后，就可以安装各种依赖包了，webpack vue vue-loader less-loader 等等， 直接输入 npm i [module-name]@版本号 [-g]
  
  package.json中的script会按照一定顺序寻找命令对应位置，本地的node_modules/.bin路径就在这个寻找清单中，所以无论是全局还是局部安装的Webpack，都不需要写前面那指明详细的路径了
  
  npm的start命令是一个特殊的脚本名称，其特殊性表现在，在命令行中使用npm start就可以执行其对应的命令。如果对应的此脚本名称不是start，想要在命令行中运行时，需要这样用npm run {script name}，如npm run build
    
  ## 安装依赖模块参数的区别

    npm install 默认安装package.json中的所有模块
    npm install --dependencies 只安装dependencies中的内容
    npm install --devDependencies 只安装devDependencies中的内容

    dependencies       字段指定了项目运行所依赖的模块   npm i xxx --save 表示将该模块写入dependencies属性        也可以简写成 -S
    devDependencies    指定项目开发所需要的模块         npm i xxx --save-dev 表示将该模块写入dependencies属性    也可以简写成 -D
  
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 

    
参考：http://javascript.ruanyifeng.com/nodejs/npm.html
