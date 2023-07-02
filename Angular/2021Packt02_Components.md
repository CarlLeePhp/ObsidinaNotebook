## 4. Pipe and Directive

#### ngFor

Besides just looping all the items in a collection, it is possible to keep track of other useful properties as well. Such a property can be used by adding another statement after the main template statement:

```html
<li *ngFor="let hero of heroes; property as variable"></li>
```

The ```variable``` is a local reference that we can use later in our template, and the ```property``` can have the following values:

- index: indicates the index of the item in the array, starting at 0 (number).
- first/last: indicates whether the current item is the first or last item of the array (boolean).
- even/odd indicates whether the index of the item in the array is even or odd (boolean).

```html
<ul>
    <li *ngFor="let hero of heroes; index as myIndex">
        {{myIdex+1}}. {{hero.name}}
    </li>
</ul>
```
