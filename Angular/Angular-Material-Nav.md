#### Starter

```javascript
// npm
npm i @angular/material @angular/cdk @angular/animations

// Angular Devkit 6+
ng add @angular/material

// js
import {BrowserAnimationsModule} from '@angular/platform-browser/animations';
import {MatButtonModule, MatCheckboxModule} from '@angular/material';

@NgModule({
  ...
  imports: [
    BrowserAnimationsModule,
    MatButtonModule,
    MatCheckboxModule
  ],
  ...
})
export class PizzaPartyAppModule { }

// Include a theme
@import "~@angular/material/prebuilt-themes/indigo-pink.css";

// to use icons add in index.html
<link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
```

#### Install Schematics

##### Navigation schematic

```ng generate @angular/material:nav <component-name>```

#### Sidenav

```typescript
import { MatSidenavModule } from '@angular/material/sidenav';
```

mat-sidenav 中的 opened 属性控制是否隐藏，可以通过媒体查询来预设值，然后通过按钮来改变值。