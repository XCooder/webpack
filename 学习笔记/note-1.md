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
         
## webpack的命令
  webpack #最基本的启动webpack命令
  webpack --progress --colors   让编译的输出内容带有 进度 和 颜色
  webpack -w #提供watch方法，实时进行打包更新 再修改文件的时候，就不需要再输入命令编译了
  webpack -p #对打包后的文件进行压缩
  webpack -d #提供SourceMaps，方便调试
  webpack --colors #输出结果带彩色，比如：会用红色显示耗时较长的步骤
  webpack --profile #输出性能数据，可以看到每一步的耗时
  webpack --display-modules #默认情况下 node_modules 下的模块会被隐藏，加上这个参数可以显示这些被隐藏的模块
         
## Webpack的两个最核心的原理:
  1. 一切皆模块
    正如js文件可以是一个“模块（module）”一样，其他的（如css、image或html）文件也可视作模块。
    因此，你可以require('myJSfile.js')亦可以require('myCSSfile.css')。这意味着我们可以将事务（业务）分割成更小的易于管理的片段，从而达到重复利用等的目的。

  2. 按需加载
    传统的模块打包工具（module bundlers）最终将所有的模块编译生成一个庞大的bundle.js文件。
    但是在真实的app里边，“bundle.js”文件可能有10M到15M之大可能会导致应用一直处于加载中状态。因此Webpack使用许多特性来分割代码然后生成多个“bundle”文件，而且异步加载部分代码以实现按需加载。
 
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

  dependencies 字段指定了项目运行所依赖的模块 npm i xxx --save 表示将该模块写入dependencies属性 简写成 -S
  devDependencies 指定项目开发所需要的模块 npm i xxx --save-dev 表示将该模块写入devDependencies属性 简写成 -D
  
## 什么是code splitting？

  在打包时通常会生成一个大的bundle.js(或者index)文件，这样所有的模块都会打包到这个bundle.js文件中，最终生成的文件往往比较大，code splitting就是指将文件分割为块(chunk)，webpack使我们可以定义一些分割点(split point)，根据这些分割点对文件进行分块，并实现按需加载。
  
    ★chunk就是打包后的代码块的意思，实际上就是输出的js文件，可能包含多个模块；chunkname就是打包后代码的名字

### code splitting的意义？
  1.第三方类库单独打包。由于第三方类库的内容基本不会改变，可以将其与业务代码分离出来，这样就可以将类库代码缓存在客户端，减少请求。

  2.按需加载。webpack支持定义分割点，通过require.ensure进行按需加载。

  3.通用模块单独打包。在代码中可能会有一些通用模块，比如弹窗、分页、通用的方法等等。其他业务代码模块常常会有引用这些通用模块。若按照2中做，则会造成通用模块重复打包，这时可以将通用模块单独打包出来。

    //在plugins中配置
    plugins: [
        new webpack.optimize.CommonsChunkPlugin("vendor", "vendor.bundle.js"),
    ]
    CommonsChunkPlugin是内置插件，直接使用就可以，提供两个参数：
      第一个参数为对应的chunk名（chunk指文件块，对应entry中的属性名）
      第二个参数为生成的文件名。

    这个插件做了两件事：
    将vendor配置的模块（jquery,bootstrap）打包到vendor.bundle.js中。
    将index中存在的jquery, bootstrap模块从文件中移除。这样index中则只留下纯净的业务代码。
  
 ## webpack中loader和plugin的区别
  loader用于加载某些资源文件到webpack，因为webpack本身只能打包commonjs规范的js文件，对于其他资源例如 css，图片，或者其他的语法集，比如 jsx，es6， coffee，是没有办法加载的，这就需要对应的loader将资源转化，加载进来，从字面意思也能看出，loader是用于加载的，它作用于一个个文件上
  
    例如：css-loader 遍历所有require的css文件，输出文件内容 
          style-loader 将css内容输出到页面的style标签中
          
    // loader: 'style-loader!css-loader!less-loader'  先使用css-loader之后使用style-loader
    // loader: ['style-loader', 'css-loader', 'less-loader']
          
    webpack的loader的配置是从右往左(从下往上)

  plugin用于扩展webpack的功能，它直接作用于 webpack，主要是扩展了它的功能。当然loader也是变相的扩展了webpack，但只专注于转化文件（transform）这一个领域，而plugin的功能更加的丰富，而不仅局限于资源的加载。
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 

    
参考：http://javascript.ruanyifeng.com/nodejs/npm.html
