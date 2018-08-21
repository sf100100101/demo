Vue脚手架中应用axios进行跨域请求
1.安装axios
 1.使用npm方法；
   	$ npm install axios
  2.使用 bower 方法
  	 $ bower install axios
   3.使用cdn
	<script src=“https://unpkg.com/axios/dist/axios.min.js”></script>

2.使用
1.这里以vue为例：在npm中安装axios之后，需要在main.js文件中引用package
 Import  axios from ‘axios’
然后全局绑定  Vue.prototype.$http=axios
 然后可以在.vue文件中使用$http来代替axios

2.在pakage.json文件中 增加- -open;
"scripts": {
    "dev": "webpack-dev-server --open --inline --progress --config build/webpack.dev.conf.js",
    "start": "npm run dev",
    "unit": "jest --config test/unit/jest.conf.js --coverage",
    "e2e": "node test/e2e/runner.js",
    "test": "npm run unit && npm run e2e",
    "lint": "eslint --ext .js,.vue src test/unit test/e2e/specs",
    "build": "node build/build.js"
  }

 
3.在.vue项目文件中基本应用：
   methods:{
    demo:function(u,p){
    this.$http.get(‘/api/yt_api/login/doLogin')   
  .then(function (response) {
    console.log(response);
    console.log(response.data.code);
    console.log(response.data.msg)
  })
  .catch(function (error) {
    console.log(error);
  });
   }
  }

 当调用demo方法时请求数据；

 3.解决跨域问题：
   在config/index.js文件中module.exports = {} 中增加

  proxyTable: {
      '/api': {
              target: 'http://121.41.130.58:9090/',//设置你调用的接口域名和端口号 别忘了加http
              changeOrigin: true,
              pathRewrite: {
                '^/api': ''//这里理解成用‘/api’代替target里面的地址，后面组件中我们掉接口时直接用api代替 比如我要调用'http://40.00.100.100:3002/user/add'，直接写‘/api/user/add’即可
              }
            }


    }



4.重启项目
停止原项目然后重新启动： npm run dev

完
