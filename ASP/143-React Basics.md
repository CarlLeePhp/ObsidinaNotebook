## Create App
Create a react app with typescript template. `npx create-react-app my-app --template typescript --use npm` 

## useState and useEffect

```js
// function component
const [products, setProducts] = useState([{"name": "product1", price: 10}]);
useEffect(() => {
    // fetch data here
},[])

// class componet
// we cans set the state inside constructor
constructor (props){
    super(props);
    this.state = {
        products: [{"name": "product1", price: 10}]
    }
}

// We use a React Hook for load data before rendering
componetDidMount(){
    // fetch data here or call functions
}
```

## API CORS Setting
```c#
builder.Services.AddCors();

//...
// Order is important for below codes
app.UseHttpsRedirection(); // exist

app.UseCors(opt => 
{
    opt.AllowyAnyHeader().AllowAnyMethod().WithOrigins("http://localhost:3000");
});
```

## TypeScript Interface
Some online tools can be used for transforming JSON to TypeScript object. Search JSON to TypeScript by Google.

```js
export interface Category {
    id: number;
    description: string;
    optionalItem?: string;
};

// how to use it
const [products, setProducts] = useState<Product>();
```


## File and Folder Organization

- src
	- app
		- layout
		- models: types for TypeScript
	- features


Move app.tsx to src/layout/ folder.
Move index.css to src/layout/ folder. Rename it as style.css.
Deleted:
- log.svg

Stop at 28


## Material UI
```bash
npm install @mui/material @emotion/react @emotion/styled

# font
npm install @fontsource/roboto

# icons
npm install @mui/icons-material
```

Import it in your entry point: (index.tsx) for Fints.
```js
import '@fontsource/roboto/300.css';
import '@fontsource/roboto/400.css';
import '@fontsource/roboto/500.css';
import '@fontsource/roboto/700.css';
```

