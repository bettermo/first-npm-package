# webpackdemo

> 发布npm包，上传图片组件玩玩

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
```

### 安装

```
npm install webpackdemoluolei
```

### 使用

- 对vant-upload二次封装，用前需要安装vant
- helloworld随便取的名称，可自行修改，实际上是个上传插件
```
import HelloWorld from 'webpackdemoluolei'
import 'webpackdemoluolei/dist/app.css'
Vue.use(HelloWorld)

<template>
   <hello-world></hello-world>
</template>
```
