
基于Vue2.0+Vuex+Axios+NodeJs+Express+MySQL实现京东移动web商城
##前端架构
- 页面结构(H5,CSS3,原生JS)
- 框架(基于Vue脚手架:vue-cli)进行搭建
- 数据请求处理框架(Axios)
- Vue-Router进行路由处理
- Vue-LazyLoad进行图片赖加载

##服务端架构
- 选用NodeJs进行后台开发
- Express中间件进行服务的配置，路由、请求的处理
- Mysql中间件处理与数据库的"通信"
- Body-Parser中间件进行前端请求参数的获取

##数据库选取
- 采用MySQL进行相关数据库的设计与实现

## 目录结构
.
├── README.md           
├── libs               		// 后台常用工具模块的封装，比如格式化事件、MD5加密等
├── route              		// 后台接口的编写目录
├── service                	// 服务层
│   ├── server.js           // 后台服务文件
├── build 		            // webpack配置文件
├── index.html         		// 首页入口文件
├── package.json       		// 项目配置文件
├── src                		// 生产目录
│   ├── assets         		// 静态文件目录 css js 和图片资源
│   ├── components     		// 各种Vue组件
│   ├── views     		    // 页面视图组件
│   ├── router     		    // 路由配置文件
│   ├── store          		// vuex状态管理器
│   ├── App.vue        		// 项目中全局Vue
│   ├── main.js        		// 项目入口文件
│   └── utils               // 自定义数据包




# vue-m-jd

> A Vue.js project about jd mobile simple web

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report

# run unit tests
npm run unit

# run e2e tests
npm run e2e

# run all tests
npm test
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
#   v u e - m - j d 
 
 