## npx package.json problem

![[1565930939928.png]]

Because the path to cache contains space. Check the config by:

![[1565931258306.png]]

The path to cache should be "D:\\Program Files\\nodejs\\node_cache". But from the first picture we can see it was cut to "Files\\nodejs\\node_cache". So we could go to the user configure file ```.npmrc```, change these to a new one without spaces. I use ```e:\Projects\nodejs\node_cache``` and ```e:\Projects\nodejs\node_global```.

## 3 nodejs 和 npm 基本操作

安装模块 ```npm i <Module Name>```。

检查本地安装的包 ```npm ls --depth 0```

检查哪些包可以更新 ```npm outdated```

更新包 ```npm update```

卸载包 ```npm uninstall```

检查哪些全局包可以更新：```npm outdated -g --depth=0```

更新全局包：```npm update -g```
