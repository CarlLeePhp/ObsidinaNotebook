### 参考

https://reactjs.org/



### 1. Local Development Evironment

```shell
# install cli
npm install -g create-react-app
create-react-app my-app

cd my-app
npm start
```



### 2. Rendering an Element into the DOM

```jsx
const element = <h1>Hello, world</h1>;
ReactDOM.render(element, document.getElementById('root'))
```



```jsx
function tick(){
    const element = (
    	<div>
        	<h1>Hello, world!</h1>
            <h2>It is {new Date().toLocaleTimeString()}.</h2>
        </div>
    );
    ReactDOM.render(element, document.getElementById('root'))
}

setInterval(tick, 1000);
```



### 3. Components and Props

#### 3.1 Function and Class Components

```jsx
function Welcome(props) {
    return <h1>Hello, {props.name}</h1>;
}

class Welcome extends React.Component {
    render(){
        return <h1>Hello, {this.props.name}</h1>
    }
}

const element = <Welcome name="Sara" />;
ReactDOM.render(
	element,
    document.getElementById('root')
);
```

**Composing Components**

**Extracting Components**

**Props are Read-Only**



### 4. State and Lifecycle





### 5. Handling Events



