#### Install

jquery, popper.js

bootstrap, ngx-bootstrap

#### Angular 中使用 jquery

在 angular.json 中配置：

```json
"scripts": [
    "node_modules/jquery/dist/jquery.min.js"
]
```

在组件的 ts 文件中引入和使用

```typescript
import * as $ from 'jquery';

export class AppComponent {
    public ngOnInit(): void {
        $('li:odd').css('backgroundColor', 'blue')
    }
}
```

#### Navbar without js

在不使用 bootstrap.js 时，导航栏是响应式的，但是下拉菜单这些不能实现。

整个 Navbar 的代码样本：

```html
<nav class="navbar navbar-expand-md navbar-dark bg-dark">
  <a class="navbar-brand" href="#">Expand at md</a>
  <button class="navbar-toggler" type="button" (click)="isCollapsed = !isCollapsed"
  [attr.aria-expanded]="!isCollapsed">
    <span class="navbar-toggler-icon"></span>
  </button>

  <div class="collapse navbar-collapse" [collapse]="isCollapsed" >
      <ul class="navbar-nav mr-auto">
          <li class="nav-item active">
            <a class="nav-link" href="#">Home</a>
          </li>
        <li class="nav-item dropdown" [class.show]="isShow">
            <button type="button" class="btn btn-link nav-link dropdown-toggle" href="#" [attr.aria-expanded]="!isShow" (click)="isShow = !isShow">Dropdown</button>
            <div class="dropdown-menu" [class.show]="isShow">
                  <a class="dropdown-item" href="#">Action</a>
                  <a class="dropdown-item" href="#">Another action</a>
                  <a class="dropdown-item" href="#">Something else here</a>
            </div>
          </li>
      </ul>
  </div>
```

**下拉菜单部分：**

1. 用一个布尔变量记录菜单是否打开，比如 isShow；
2. 链接改成按钮，伪装成链接。<button type="button" class="btn btn-link ... "。
3. 按钮点击切换布尔变量。

按钮的 id，aria-haspopup，data-toggle 和下拉菜单的 aria-labelledby 属性可以去掉。

```html
<li class="nav-item dropdown" [class.show]="isShow">
        <button type="button" class="btn btn-link nav-link dropdown-toggle" href="#" [attr.aria-expanded]="!isShow" (click)="isShow = !isShow">Dropdown</button>
        <div class="dropdown-menu" [class.show]="isShow">
          <a class="dropdown-item" href="#">Action</a>
          <a class="dropdown-item" href="#">Another action</a>
          <a class="dropdown-item" href="#">Something else here</a>
        </div>
      </li>
```

**手机菜单按钮**

1. 用一个布尔值记录是否展开，并关联到 aria-expanded 属性上；
2. 绑定点击事件；
3. id 可以删掉

```html
<button class="navbar-toggler" type="button" (click)="isCollapsed = !isCollapsed"
  [attr.aria-expanded]="!isCollapsed">
    <span class="navbar-toggler-icon"></span>
  </button>


  <div class="collapse navbar-collapse" [collapse]="isCollapsed" >
```
