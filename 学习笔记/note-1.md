## 比较webpack和其他工具

  Gulp/Grunt是一种能够优化前端的开发流程的工具，而WebPack是一种模块化的解决方案(一切皆模块)

  Grunt和Gulp的工作方式是：在一个配置文件中，指明对某些文件进行类似编译，组合，压缩等任务的具体步骤，task自动替你完成这些任务。

  Webpack的工作方式是：把你的项目当做一个整体，通过一个给定的主文件（如：index.js）
  Webpack将从这个文件开始找到你的项目的所有依赖文件，使用loaders处理它们，最后打包为一个（或多个）浏览器可识别的JavaScript文件。
  
  全局安装 (不推荐)(注意：项目目录名不能使用webpack，否则在初始化的时候会报错)
  npm install -g webpack

    注意：安装完成直接使用webpack命令，可能会提示'不是命令...'，这时候需要查看一下webpack的版本，主要4.x版本和1.x/2.x/3.x有区别
    
    在webpack3中，webpack本身和它的CLI是在同一个包中，但在第4版中，将两者分开来以便更好地管理它们为了能在全局环境使用webpack-cli，最好全局安装webpack-cli，如果没有全局安装cli，只能进入路径node_modules/.bin/webpack 执行了
    
    总结：如果webpack-cli是局部安装的，想要使用webpack命令必须进入node_modules/.bin/webpack才能执行webpack命令
         如果是全局安装的webpack-cli，就不需要进入bin目录，webpack就能够寻找到它的命令路径了
 
 ## package.json文件的作用   
    package.json是一个标准的npm说明文件，里面包括当前项目的依赖模块，自定义的脚本任务等等。在终端中使用 npm init -y 命令可以自动创建这个package.json文件，如果不准备在npm中发布你的模块，输入 npm init -y 一路跳过即可
    这些准备工作就绪之后，就可以安装各种依赖包了，webpack vue vue-loader less-loader 等等， 直接输入 npm i [module-name]@版本号 [-g]
    
    如果是全局安装 webpack 可以直接运行 webpack --help
    如果是本地安装 webpack win用户需要额外指定其在node_modules中的地址 .\node_modules\.bin\ 然后再运行 webpack --help

    在命令行中输入命令需要代码类似于node_modules/.bin/webpack这样的路径其实是比较烦人的
    不过npm可以引导任务执行，对npm进行配置后可以在命令行中使用简单的npm start命令来替代上面略微繁琐的命令
    只要在package.json中对scripts对象进行相关设置
