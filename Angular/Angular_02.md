## 概述

我希望通过这篇笔记，学习关于表单、组件和模板的相关内容。关注如何在它们之间传递变量。



### Forms

Angular provides two difference approaches to handling user input through forms: reactive and template-driven.

+ Reactive forms are more robust: they are more scalable, reusable, and testable. If forms are a key part of your application use reactive forms.
+ Template-driven forms are useful for adding a simple form to an app, such as an email list signup form. They are easy to add to an app, but they do not scale as well as reactive forms.



### Components & Templates

Showing an array property with *ngFor

```html
<li *ngFor="let hero of heroes">
	{{ hero }}
</li>
```





#### Template Syntax

The "script" element is forbidden in template syntax.

Interpolation ( {{ ... }} )



#### Two way bind for input

```html
<input [(ngModel)]="selectedHero.name">
```



#### Class binding

The Angular class binding makes it easy to add and remove a CSS class conditionally. Just add [class.some-css-class]="some-condition" to be element you want to style.



#### Transport to child component

In the father component's template: ```<app-child [for-child] = "from-father"></app-child>```





### Angular 硬绑 Bootstrap

直接把 Bootstrap、jQuery 这些东西放到 asset 文件夹下。