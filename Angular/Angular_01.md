## 0 参考

nodejs: https://nodejs.org/en

Angular: https://angularjs.org/

TryNewAngular: https://angular.io/

菜鸟教程: http://www.runoob.com/

这篇笔记记录，环境的搭建和相关工具的使用。下篇开始一点点学习 Angular 的基本内容。

## 1 环境准备

需要 node.js 和 npm。Linux 安装：

```shell
curl -sL https://deb.nodesource.com/setup_6.x | sudo E bash -
apt-get install nodejs
npm install -g @angular/cli
```

**关于淘宝镜像和 cnpm**

```shell
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
```

持久使用淘宝镜像

```shell
$ npm config set registry https://registry.npm.taobao.org
# 通过下面的方式验证是否成功
$ npm config get registry
# 或者
$ npm info express
```

临时使用淘宝镜像

```shell
$ npm --registry https://registry.npm.taobao.org install express
```

## 2 开始

创建一个应用 ```ng new my-app```。

启动应用 ```ng server --open```。

新建组件 ```ng generate component name```。

## 3 nodejs 和 npm 基本操作

安装模块 ```npm i <Module Name>```。

检查本地安装的包 ```npm ls --depth 0```

检查哪些包可以更新 ```npm outdated```

更新包 ```npm update```

卸载包 ```npm uninstall```
