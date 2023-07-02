### Prepare

```javascript
// install
npm install -g @vue/cli

// creating a project
vue create hello-world
...
cd hello-world

// install plugins
vue add @vue/eslint

// Run
npm run serve
```



#### VS Code 插件

Vetur 和 Vue 2 Snippets



#### Vue-component

单文件组件包括：

+ template
+ script
+ style

```vue
<template>
	<div>
        <p>{{ message }}</p>
        <input v-model="message" />
    </div>
</template>

<script>
export default {
    data(){
        return {
            message: 'Hello world',
        }
    },
}
</script>

<style>
    p {
        color: grey;
    }
</style>
```





### Vue-router

```javascript
npm install --save vue-router

// main.js
import VueRouter from 'vue-router'

Vue.use(VueRouter)

var router = new VueRouter({
    routes: [
        { path: '/home', componet: }
    ];
});

new Vue({
    render: h=> h(App),
    router
}).$mount('#app')

// App.vue
<router-view></router-view>
```



路由分离

```javascript
// router.js
import VueRouter from 'vue-router'

import Home from "./components/Home.vue"
import Contact from "./components/Contact.vue"

var router = new VueRouter({
    routes: [
        { path: '/', redirect: '/home' },
        { path: '/home', component: Home,
         children: [
             { path: 'contact', component: Contact } // it is for #/home/contact
         ]}
    ]
})

export default router

// main.js

import router from './router.js'

```



### With Bootstrap

```javascript
npm i bootstrap
npm i bootstrap-vue

// Regiser it in app entry point:
import Vue from 'vue'
import BootstrapVue from 'bootstrap-vue'

Vue.use(BootstrapVue);

// And import Bootstrap and Bootstrap-Vue css files:
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'
```



### With Element

```javascript
vue add element // 以下貌似不用手动配置
// in main.js:
import Vue from 'vue';
import ElementUI from 'element-ui';
import 'element-ui/li/theme-chalk/index.css';
import App from './App.vue';

Vue.use(ElementUI);

new Vue({
    el:'#app',
    render: h => h(App)
});
```





