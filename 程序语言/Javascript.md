#### 对象数组排序

页面部分

```html
<table class="table table-striped">
    <thead>
        <tr>
            <th scope="col"><a href="#" @click="sortBy('id')">ID</a></th>
            <th v-bind:class="{'d-none': isHideName}" scope="col"><a href="#" @click="sortBy('name')">NAME</a></th>
            <th v-bind:class="{'d-none': isHidePrice}" scope="col"><a href="#" @click="sortBy('price')">PRICE</a></th>
        </tr>
    </thead>
    <tbody>
        <tr v-for="fruit in fruits" :key=fruit.id>
            <td >{{ fruit.id }}</td>
            <td v-bind:class="{'d-none': isHideName}">{{ fruit.name }}</td>
            <td v-bind:class="{'d-none': isHidePrice}">{{ fruit.price }}</td>
        </tr>
    </tbody>
</table>
```

Vue 部分

```javascript
var app=new Vue({
    el: '#app',
    data: {
        isHideName: false,
        isHidePrice: false,
        toggle: false,
        fruits: [
            {id: 0, name: "Apple", price: 3.40},
            {id: 1, name: "Pear", price: 2.40},
            {id: 2, name: "Orange", price: 1.40},
            {id: 3, name: "Banana", price: 3.60}
        ]
    },
    methods: {
        sortBy: function(sortKey){
            this.toggle = !this.toggle;
            if(this.toggle){
                this.fruits.sort(function(a, b){
                    return a[sortKey].localeCompare(b[sortKey]);
                })
            } else {
                this.fruits.sort(function(a, b){
                    return b[sortKey].localeCompare(a[sortKey]);
                })
            }
        }
    }
})
```

