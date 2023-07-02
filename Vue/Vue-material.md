#### Installation

```javascript
npm install vue-material --save

// Roboto Font and Icons
<link rel="stylesheet" href="//fonts.googleapis.com/css?family=Roboto:400,500,700,400italic|Material+Icons">
```



#### Import Component

```javascript
// main.js
import { MdButton, MdContent, MdTabs } from 'vue-material/dist/components'
import 'vue-material/dist/vue-material.min.css'
import 'vue-material/dist/theme/default.css'

Vue.use(MdButton)
Vue.use(MdContent)
Vue.use(MdTabs)

// Full Bundle
import VueMaterial from 'vue-material'
import 'vue-material/dist/vue-material.min.css'

Vue.us(VueMaterial)
```

