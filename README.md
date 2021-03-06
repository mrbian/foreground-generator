#foreground-generator
前端开发脚手架生成器

## 前端脚手架说明
- 使用webpack-dev-server + hot-middleware实现内存中文件热加载
- 使用gulp实现自动化

- 初始化项目

```
/**
* 编译一遍src/js、src/css、src/scss 下面的css和js以及html，生成assets文件夹
* 启动app，webpack-dev-server在内存中再次编译一遍
* 此时webpack-dev-server在内存中的文件和assets文件夹下的文件一模一样
* 这样配置方便更改js和css文件的前缀
*/
npm start   
```

- 添加一个页面

```
/**
* 询问filename之后
* 自动生成[filename].js放在src/js下
* 自动生成[filename].scss 和 [filename].css 在src/scss 和 src/css下
* 自动生成[filename].html 在src/html下
* 编译后重启工程
*/ 
gulp add
```

- src/html 和 src/js下的文件是一一对应关系，比如，a.html的webpack入口文件就是a.js
- server/views 下的渲染实例只需要在文件开头加入如下路径配置，就可以引入所有在入口文件配置好的js和css了

```
<% extend "../../assets/home.html" %>
```
***这个路径是views文件夹内部相对于assets文件夹的，而不是html相对于assets文件夹的，这点要注意***

- 修改了入口文件的js后，整个页面会自动reload，不需要F5刷新

### 发布
有两种发布方式
- 一 、 静态文件形式发布
```
gulp pack 
```
压缩所有的资源文件同时打包出server/views一级目录下面的html，assets/html文件夹下面得到的都是已经经过ect编译后的html  
如果需要修改资源文件的前缀，只需要修改package.json下面的remoteServer.staticPrefix   

此时assets文件夹可以直接交给后端  
可以让后端以静态文件的形式发布  

- 二、 动态渲染发布
```
gulp pack
```
压缩后，通过server动态渲染上线


## 生成器说明
- 可以选择js框架使用angular1、angular2、react、vue
- 可以选择css框架使用amazeui还是bootstrap
- 可以选择js代码是使用ES6还是ES5
- 自动为文件头加入作者信息和创建日期

## 使用

```
npm install -g generator-foreground
mkdir test 
cd test
yo foreground
```

## 友情提示
- 使用Webstorm将templates文件夹mark成outproject，让webstorm自动的Inspection对templates文件夹下的文件失效
- React框架对bower的支持不好，请引入node_modules下面的React
- 前端所有全局通用变量如jquery,React都一定使用expose-loader给expose出来，否则在最后打包发布的时候会有问题
