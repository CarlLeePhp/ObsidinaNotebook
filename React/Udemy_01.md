## Section 1

+ React Developer Tools (Chrome)
+ Redux DevTools (Chrome)
+ ES7 React / Redux / GraphQL / React-Native snippets
+ Bracket Pair Colorizer
+ Auto Rename Tag
+ Prettier - Code formatter

Others

+ npm

## Section 2

#### Create a project

```shell
npm i create-react-app -g
create-react-app app-name
// or use npx
npx create-react-app app-name

// no other dependency
```



#### Clean up and prepare

Under src folder: App.test.js, index.css, logo.svg, serviceWorker.js

```javascript
// index.js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(<App />, document.getElementById('root'));

// App.js
import React from 'react';
import './App.css';

function App() {
  return (
    <div className="App">
      <h1>Welcome to react!</h1>
    </div>
  );
}

export default App;

```



#### Class Style

```jsx
import React, { Component } from 'react';

class App extends Component {
    render(){
        return ( // cannot return more than one parent element
            <Fragment className='App'>  // Fragment will not render
            	<Navbar />
            </Fragment>
        );
    }
}
```



#### Expressions & Conditionals

```jsx
import React, { Component } from 'react';
import PropTypes from 'prop-types';


export class Navbar extends Component {
    static defaultProps = {
        title: 'Github Finder',
        icon: 'fab fa-github'
    };  // set the defaultProps

    static propTypes = {
        title: PropTypes.string.isRequired,
        icon: PropTypes.string.isRequired
    }  // verify the type of props
    render() {
        return (
            <nav className='navbar bg-primary'>
                <h1>
                    <i className={this.props.icon} /> {this.props.title}
                </h1>
            </nav>
        )
    }
}

export default Navbar
```



## Section 3

```rce``` for Class based React Component.

Some points for these section:

+ Set the state for a component.
+ Repeat something in array. ```.map```



#### Repeat items in array:

```jsx
render() {
    return (
        <div style={userStyle}>
            {this.state.users.map(user =>(
                <UserItem key={user.id} user={user} />
            ))}
        </div>
    )
}
```

Get the props from parent

```jsx
const {avatar_url, login, html_url} = this.props.user;
```



#### ICONS

Get the resource from any icon supplier, and put the link into index.html

```html
<script src="https://kit.fontawesome.com/ea630270ea.js"></script>
```



#### Class Based Props

```javascript
// Where use it
<Navbar title="Github Finder"/>
// In the component
<i className='fab fa-github' /> {this.props.title}
```



The default props and prop types are defined in the class as a method.

```javascript
// out of the class
import PropTypes from 'prop-types';

// in the class
static defaultProps = {
    title: 'Github Finder',
    icon: 'fab fab-github'
};

static propTypes = {
    title: PropTypes.string.isRequired,
    icon: PropTypes.string.isRequired,
};
```



#### Component States

```javascript
    state = {
        id: 'id',
        login: 'mojombo',
        avatar_url: 'https://avatars0.githubusercontent.com/u/1?v=4',
        html_url: 'https://github.com/mojombo'
    };

    render() {
        const {login, avatar_url, html_url} = this.state;
        return (
            <div className="card text-center">
                <img src={avatar_url} alt="" className="round-img" style={{ width: '60px'}} />
                <h3>{login}</h3>
                <div>
                    <a href={html_url} className="btn btn-dark btn-sm my-1">
                        More
                    </a>
                </div>
            </div>
        )
    };
```



#### Functional Components

As there is no state for these components, so there is no reason for using class components.

Default props and prop types should be out of the function.

```javascript
Navbar.defaultProps = {
    title: 'Github Finder',
    icon: 'fab fab-github'
};

Navbar.propTypes = {
    title: PropTypes.string.isRequired,
    icon: PropTypes.string.isRequired,
};
```

**racf** for create a functional component.

#### Requests & Update State

Install axios.

```shell
npm i axios
```

Use axios

```javascript
async componentDidMount(){
    const res = await axios.get('https://api.github.com/users');
    console.log(res.data);
}
```

change the state: ```this.setState({ alert: { msg: msg, type: type }})```

#### Environment Variables

Create a file called ```.env.local``` under root folder, and make sure it is in the ```.gitignore``` file.

How to use the environment variables:

```javascript
const res = await axios.get(`https://api.github.com/users?client_id=${process.env.REACT_APP_GITHUB_CLIENT_ID}&client_secret=${process.env.REACT_APP_GITHUB_CLIENT_SECRET}`);
    
```



## Section 4

#### 双向绑定

```jsx
// 双向绑定
state = {
    text: ''
};
onChange = (e) => {
    // this.setState({text: e.target.value});
    this.setState({[e.target.name]: e.target.value});
}

<input type='text' name='text' value={ this.state.text } onChange={ this.onChange } />
```

#### Pass Up

```jsx
// in search component
onSubmit = (e) => {
    e.preventDefault();
    this.props.searchUsers(this.state.text);
    this.setState({text: ''});
}
<form onSubmit={this.onSubmit}></form>

// in its parent
searchUsers = (text) => {
    console.log(text);
}
<Search searchUsers={this.searchUsers} />
```





## Section 5

