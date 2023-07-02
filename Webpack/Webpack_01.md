### 在 Vue 课程中介绍了哪些功能

Webpack 是一个基于项目的前端构建工具。



### Webpack 4.x

全局安装 npm i -g webpack webpack-cli

初始化项目 npm init -y

项目根目录下创建文件夹 src, dist

需要一个配置文件：webpack.config.js

```javascript
module.exports = {
    mode: 'development'  // development, production
}
```



#### webpack-dev-server

```npm i webpack-dev-server -D```

然后修改 package.json

```json
"scripts": {
    "test": ....,
    "dev": "webpack-dev-server“
}
```

这样就可以用 ```npm run dev`` 来运行这个插件。



#### HTML-webpack-plugin

```npm i html-webpack-plugin -D``` 

在 webpack.config.js 中配置插件

```javascript
const path = require('path')
const HtmlWebPackPlugin = require('html-webpack-plugin')

const htmlPlugin = new HtmlWebPackPlugin ({
    template: path.join (__dirname, './src/index.html'), // src
    filename: 'index.html'  // target
})

module.exports = {
    mode: 'development',
    plugins: [
        htmlPlugin
    ]
}
```



#### 处理 CSS

```npm i style-loader css-loader -D```

配置 webpack.config.js

```javascri	
module.exports = {
    module: {
        rules: [
            { test: /\.css$/, use: ['style-loader', 'css-loader] },
        ]
    }
}
```





### Webpack 中使用 Vue

```npm i vue -S```

要使用 .vue 文件创建组建，安装 ```npm i vue-loader vue-template-compiler -D```

