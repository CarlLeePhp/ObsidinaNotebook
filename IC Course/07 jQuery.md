## jQuery
1. JSON to object


#### JSON to object
Refer: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse
```js
const json = '{"result":true, "count":42}';
const obj = JSON.parse(json);

console.log(obj.count);
// Expected output: 42

console.log(obj.result);
// Expected output: true
```

jQuery did it for us?
```js
$.get("api/StaffTypesAPI/", function (data) {
    console.log(typeof(data))
});
// output is object
```
https://www.sitepoint.com/ajaxjquery-getjson-simple-example/

JS map, join.


## Vue.js
1. Moved html code from JS.
2. Update data rather than html elements. It is easier.

## React

Refer: W3School React

```js
<script crossorigin src="https://unpkg.com/react@18/umd/react.development.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
```


