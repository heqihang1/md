```bash
  "scripts": {"start": "craco start",}
```

安装
```bash
   npm install @craco/craco --save
   npm install http-proxy-middleware
```
src下创建文件 setupProxy.js
```js
    const { createProxyMiddleware } = require('http-proxy-middleware')
    const target = 'http://192.168.0.0:3000';
    module.exports = function (app) {
        app.use(
            '/api',
            createProxyMiddleware({
                target : target,
                changeOrigin : true,  // 设置跨域请求
                // PathRewrite : {
                //     '^/api' : '' // 将/api 变为 ''
                // }
            })
        );
    }
```
src下创建文件 craco.config.js
```bash
  安装 npm install craco-less
```
```js
const CracoLessPlugin = require("craco-less");
const path = require('path')
module.exports = {
  webpack: {
    alias: {
      '@': path.join(__dirname, 'src')
    }
  },
  plugins: [
    {
      plugin: CracoLessPlugin,
      options: {
        lessLoaderOptions: {
          lessOptions: {
            modifyVars: { "@primary-color": "#1DA57A" }, // 主题颜色
            javascriptEnabled: true
          }
        }
      }
    }
  ],
  babel: {
    plugins: [["@babel/plugin-proposal-decorators", { legacy: true }]]
  }
}
```
