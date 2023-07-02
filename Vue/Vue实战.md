## 开发工具和环境

#### Vue 开发者工具

Chrome 网上应用商店，Vue.js devtoos。在扩展设置中，启用 Allow access to file URLs。

#### 设置开发环境

```shell
npm uninstall vue-cli -g
npm install -g @vue/cli
vue --version
```

Visual Studio Code 开发扩展：vetur

安装后 vue 不能执行，可能是 nodejs 的路径设置不正确。用 ```npm root -g``` 查看当前设置的路径，把他们写到 windows path 里。



## 第 4 章 高级项目设置

**Create Project:** ```vue create hello-world```，书中的配置：Babel, stylus。

**CSS Pre-Processors**

```shell
# Sass
npm install -D sass-loader sass
# Less
npm intall -D less-loader less
# Stylus
npm install -D stylus-loader stylus
```



+ 路由模式 p115
+ 路由链接 p116