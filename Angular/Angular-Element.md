### Starter

```javascript
npm i -S element-angular

// import packages
import { BrowserModule } from '@angular/platform-browser'
import { BrowserAnimationsModule } from '@angular/platform-browser/animations'
import { ElModule } from 'element-angular'

@NgModule({
    imports: [
        ElModule.forRoot(),
    ]
})

// css
@import "~element-angular/theme/index.css";
```



这里面有导航栏，可是这玩意不是响应式的！