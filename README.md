# nuxt2

> Nuxt.js project

## Build Setup

``` bash
# install dependencies
$ npm install # Or yarn install

# serve with hot reload at localhost:3000
$ npm run dev

# build for production and launch server
$ npm run build
$ npm start

# generate static project
$ npm run generate
```



Nuxt.js 是一个基于 Vue.js 的通用应用框架。 
		通过对客户端/服务端基础架构的抽象组织，Nuxt.js 主要关注的是应用的 UI渲染。SSR服务器
		SSR在服务端将vue渲染成html返回给浏览器。

优点：
1.对SEO友好。对单纯Vue的spa就很不友好，对于类似新闻的网站，搜索引擎无法抓取。
2.对于SPA的首屏打开速度会更加快速。

新闻、博客、电影

一、初始化项目  
vue init nuxt/starter

二、目录结构
assets: 静态资源目录  less,sass.图标不会放这里。
This directory contains your un-compiled assets such as LESS, SASS, or JavaScript.
middleware 中间件
plugins 插件
static 图片、图标
store  Vuex状态管理
.editorconfig vscode编写代码格式规则
.eslintrc.js  esList规则，代码规则
.gitignore 默认不上传文件  用generator生成的dist不会上传

nuxt.config.js 

build 扩展

package depencies生成环境  devDeprendencies 开发环境
script npm run -dev中dev都在其中

三、常用配置项

需求一： 修改IP和端口号
"config":{
    "nuxt":{
      "host": "127.0.0.1",
      "port": "1818"
    }
  },
  
  重启
  
需求二： 修改字体文件
1.在assets的css文件夹下新建normailze.css文件
2.在nuxt.config.js新建css对象
  css:['~assets/css/normailze.css'],
  
  直接匹配到当前文件，比较方便
  
  因为已经有css样式，所以可以
  
  
 需求三、设置配置项
  build: {
    loader:[
      {
        test: /\.(png|jpe?g|gif|svg)$/,
        loader: "url-loader",
        query:{
          limit: 1000,
          name:'img/[name].[hash].[ext]'
        }
      }
    ],
    /*
    ** Run ESLint on save
    */
    extend (config, { isDev, isClient }) {
	
	
四、路由配置和参数传递
Nuxt不需要我们去配置路由，她会自动配置路由。并且不建议使用<a>标签，最好使用
<nuxt-link></nuxt-link>标签。

  <ul>
      <li><nuxt-link :to="{name:'index'}">HOME</nuxt-link></li>
      <li><nuxt-link :to="{name:'about'}">ABOUT</nuxt-link></li>
      <li><nuxt-link :to="{name:'news',params:}">NEWS</nuxt-link></li>
    </ul>
	
传递参数
  <ul>
      <li><nuxt-link :to="{name:'index'}">HOME</nuxt-link></li>
      <li><nuxt-link :to="{name:'about'}">ABOUT</nuxt-link></li>
      <li><nuxt-link :to="{name:'news',params:{newsId: 3301}}">NEWS</nuxt-link></li>
    </ul>
	
	<div>
        <h2>NEWS</h2>
        <p>NewsID: {{$route.params.newsId}}</p>
        <ul>
            <li><a href="/">Home</a></li>
        </ul>
    </div>
	
五：动态路由
news/index.vue
 <div>
        <h2>new-content</h2>
        <p>newsId:{{$route.params.id}}</p>
        <ul>
            <li>
                <a href="/">home</a>
            </li>
        </ul>
    </div>

news/_id.vue
    <div>
        <h2>new-content</h2>
        <p>newsId:{{$route.params.id}}</p>
        <ul>
            <li>
                <a href="/">home</a>
            </li>
        </ul>
    </div>	
	
六、动画效果
 分为全局和局部
assets/css/main.ss
.page-enter-active, .page-leave-active {
    transition: opacity 2s;
}
.page-enter, .page-leave-active {
    opacity: 0;
}

局部

assets/css/main.css
.test-enter-active, .test-leave-active{
    transition: all 2s;
    font-size: 12px;
}

.text-enter, .test-leave-active{
    opacity: 0;
    font-size: 40px;
}

默认模板

默认模板(修改后需要重启)
/app.html  
<!DOCTYPE html>
<html lang="en">
<head>
    {{HEAD}}
</head>
<body>
    <p>JSPang.com 技术胖博客</p>
    {{APP}}
</body>
</html>



默认布局（修改后不需要重启，一般都是使用默认布局）
只能定义template的东西，不能定义head里面的东西
news/index.css
export default {
    transition:'test'
};

八、错误页面和个性Meta
/layouts/error.vue
<template>
    <div>
        <h2 v-if="error.statusCode == 404">404 你需要的页面没有找到</h2>
        <h2 v-else-if="error.statusCode == 500">500 服务错误</h2>
    </div>
</template>
<script>
export default {
    props:['error']
}
</script>


个性meta
news/index.vue
<template>
    <div>
        <h2>new-list</h2>
         <ul>
            <li>
                <a href="/">home</a>
                <a href="/news/123">new-1</a>
                <a href="/news/456">new-2</a>
            </li>
            <li><nuxt-link 
                :to="{name:'news-id',params:{id: 123,title:'lianghaihsia'}}">NEWS</nuxt-link></li>

        </ul>
    </div>
</template>

<script>
export default {
    transition:'test'
};
</script>

<style scoped>
</style>

news/_id.vue
<script>
    export default {
        // 参数校验
        validate({params}){
            return /^\d+$/.test(params.id);
        },
        data() {
            return {
                title: this.$route.params.title
            }
        },
        // 独立设置head信息
        head(){
            return {
                title:this.title,
                meta:[
                    {hid:'bbbbb',name:'news1',content:'this is news page '}
                ]
            }
        }
    }
</script>

查看源代码就能发现两个meta,需要覆盖，
将hid设置为“discription”即可

九、异步请求数据方法 asyncDAta
1.创建数据仓库
打开 myjson.com
{
  "name": "lianghaihsia",
  "age": 18,
  "hobby": "readin123123g"
}

2.
/asyncData.vue
<template>
   <div>
       <h1>姓名： {{info.name}}</h1>
       <h1>年龄： {{info.age}}</h1>
       <h1>兴趣： {{info.hobby}}</h1>
    </div> 
</template>
<script>
import axios from 'axios'
export default {
    data() {
        return {
            name: "Hello word"
        }
    },
    // 方法二
    async asyncData(){
       let {data} = await axios.get('https://api.myjson.com/bins/11gze0')
       return {info: data}
    }
    // 方法一
    // asyncData(){
    //     return axios.get('https://api.myjson.com/bins/11gze0')
    //             .then((res)=>{
    //                 return {info:res.data}
    //             })
    // }
}
</script>

十、静态资源文件和部署

npm run generate 
打包完了之后就是传统的Html文件。

/index.vue
<template>
  <div>
    <div class="diss">
      <!-- <img src="~static/timg.jpg" alt=""> -->
    </div>
    <ul>
      <li><nuxt-link :to="{name:'index'}">HOME</nuxt-link></li>
      <li><nuxt-link :to="{name:'about'}">ABOUT</nuxt-link></li>
      <li><nuxt-link :to="{name:'news',params:{newsId: 3301}}">NEWS</nuxt-link></li>
      <li><nuxt-link :to="{name:'asyncData'}">asyncData</nuxt-link></li>
    </ul>
  </div>
</template>

<script>
import AppLogo from '~/components/AppLogo.vue'

export default {
  components: {
    AppLogo
  }
}
</script>

<style>
.diss{
  width: 300px;
  height: 100px;
  background-image: url(~static/timg.jpg)
}
</style>

For detailed explanation on how things work, checkout the [Nuxt.js docs](https://github.com/nuxt/nuxt.js).

