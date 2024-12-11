# Detailed React Course Cheatsheet

## 1. Start Here

- React: A JavaScript library for building user interfaces
- Key concepts:
  - Components: Reusable UI pieces
  - State: Data that changes over time
  - Props: Data passed between components
- Virtual DOM: React's efficient updating mechanism

## 2. App & JSX

- JSX: JavaScript XML, allows writing HTML-like code in JavaScript
- Basic syntax:

  ```jsx
  const element = <h1>Hello, world!</h1>;
  ```
  
- Expressions in JSX:

  ```jsx
  const name = 'John';
  const element = <h1>Hello, {name}</h1>;
  ```

- JSX represents objects:

  ```jsx
  const element = React.createElement('h1', null, 'Hello, world!');
  ```

## 3. Functional Components

- Create a functional component:

  ```jsx
  const MyComponent = () => {
    return <div>Hello from MyComponent</div>;
  };
  ```

- Use components:

  ```jsx
  const App = () => {
    return (
      <div>
        <MyComponent />
        <MyComponent />
      </div>
    );
  };
  ```

## 4. Applying CSS Styles

- Inline styles:

  ```jsx
  <div style={{color: 'red', fontSize: '14px'}}>Styled text</div>
  ```

- CSS modules:

  ```jsx
  import styles from './MyComponent.module.css';
  
  const MyComponent = () => {
    return <div className={styles.myClass}>Styled with CSS module</div>;
  };
  ```

- Styled-components (if used in the course):

  ```jsx
  import styled from 'styled-components';
  
  const StyledDiv = styled.div`
    color: blue;
    font-size: 16px;
  `;
  
  const MyComponent = () => {
    return <StyledDiv>Styled with styled-components</StyledDiv>;
  };
  ```

## 5. Click Events

- Basic onClick:

  ```jsx
  const handleClick = () => {
    console.log('Button clicked!');
  };
  
  return <button onClick={handleClick}>Click me</button>;
  ```

- With parameters:

  ```jsx
  const handleClick = (id) => {
    console.log(`Item ${id} clicked`);
  };
  
  return <button onClick={() => handleClick(1)}>Click Item 1</button>;
  ```

- Event object:

  ```jsx
  const handleClick = (e) => {
    console.log('Event:', e);
    e.preventDefault(); // Prevent default behavior
  };
  
  return <a href="#" onClick={handleClick}>Click me</a>;
  ```

## 6. useState Hook

- Basic usage:

  ```jsx
  import React, { useState } from 'react';
  
  const Counter = () => {
    const [count, setCount] = useState(0);
    
    return (
      <div>
        <p>Count: {count}</p>
        <button onClick={() => setCount(count + 1)}>Increment</button>
      </div>
    );
  };
  ```

- With objects:

  ```jsx
  const [user, setUser] = useState({ name: '', age: 0 });
  
  const updateName = (name) => {
    setUser(prevUser => ({ ...prevUser, name }));
  };
  ```

## 7. Lists & Keys

- Rendering lists:

  ```jsx
  const items = ['Apple', 'Banana', 'Orange'];
  
  return (
    <ul>
      {items.map((item, index) => (
        <li key={index}>{item}</li>
      ))}
    </ul>
  );
  ```

- Using object properties as keys:

  ```jsx
  const users = [
    { id: 1, name: 'John' },
    { id: 2, name: 'Jane' }
  ];
  
  return (
    <ul>
      {users.map(user => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
  ```

## 8. Props & Prop Drilling

- Passing props:

  ```jsx
  const Parent = () => {
    return <Child name="John" age={30} />;
  };
  
  const Child = (props) => {
    return <p>{props.name} is {props.age} years old.</p>;
  };
  ```

- Destructuring props:

  ```jsx
  const Child = ({ name, age }) => {
    return <p>{name} is {age} years old.</p>;
  };
  ```

- Prop drilling (passing props through multiple levels):

  ```jsx
  const GrandParent = () => {
    const data = "Hello from GrandParent";
    return <Parent data={data} />;
  };
  
  const Parent = ({ data }) => {
    return <Child data={data} />;
  };
  
  const Child = ({ data }) => {
    return <p>{data}</p>;
  };
  ```

## 9. Controlled Component Inputs

- Basic controlled input:

  ```jsx
  const [inputValue, setInputValue] = useState('');

  const handleChange = (e) => {
    setInputValue(e.target.value);
  };

  return <input value={inputValue} onChange={handleChange} />;
  ```

- Form with multiple inputs:

  ```jsx
  const [formData, setFormData] = useState({ username: '', password: '' });

  const handleChange = (e) => {
    const { name, value } = e.target;
    setFormData(prevData => (  {...prevData,[name]: value }  ) ) ;
  };

  return (
    <form>
      <input
        name="username"
        value={formData.username}
        onChange={handleChange}
      />
      <input
        name="password"
        type="password"
        value={formData.password}
        onChange={handleChange}
      />
    </form>
  );
  ```

## 10. Project Challenge

- Apply concepts learned in a real-world project
- Focus on component structure, state management, and props usage

## 11. useEffect Hook

- Basic usage:

  ```jsx
  import React, { useState, useEffect } from 'react';
  
  const MyComponent = () => {
    const [data, setData] = useState(null);
    
    useEffect(() => {
      // This runs after every render
      console.log('Component rendered');
    });
    
    useEffect(() => {
      // This runs only on mount
      console.log('Component mounted');
    }, []);
    
    useEffect(() => {
      // This runs when data changes
      console.log('Data changed:', data);
    }, [data]);
    
    return <div>My Component</div>;
  };
  ```

- Cleanup function:

  ```jsx
  useEffect(() => {
    const timer = setTimeout(() => {
      console.log('This will run after 1 second');
    }, 1000);
    
    return () => clearTimeout(timer);
  }, []);
  ```

## 12. JSON Server

- Setup:

  ```JSX
  npm install json-server
  ```

- Create a `db.json` file:

  ```json
  {
    "posts": [
      { "id": 1, "title": "json-server", "author": "typicode" }
    ]
  }
  ```

- Run JSON Server:

  ```JSX
  json-server --watch db.json --port 3500
  ```

## 13. Fetch API Data

- Basic GET request:

  ```jsx
  useEffect(() => {
    const fetchData = async () => {
      try {
        const response = await fetch('https://api.example.com/data');
        const data = await response.json();
        setData(data);
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    };
    
    fetchData();
  }, []);
  ```

## 14. CRUD Operations

- Create (POST):

  ```jsx
  const createPost = async (post) => {
    const response = await fetch('https://api.example.com/posts', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(post),
    })
    return await response.json();
  };
  ```

- Read (GET):

  ```jsx
  const getPosts = async () => {
    const response = await fetch('https://api.example.com/posts');
    return await response.json();
  };
  ```

- Update (PUT):

  ```jsx
  const updatePost = async (id, updatedPost) => {
    const response = await fetch(`https://api.example.com/posts/${id}`, {
      method: 'PUT',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(updatedPost),
    });
    return await response.json();
  };
  ```

- Delete (DELETE):

  ```jsx
  const deletePost = async (id) => {
    await fetch(`https://api.example.com/posts/${id}`, {
      method: 'DELETE',
    });
  };
  ```

## 15. Fetch Data Challenge

- Implement a component that fetches and displays data from an API
- Handle loading and error states
- Implement pagination or infinite scrolling if applicable

## 16. React Router

- Installation:

  ```JSX
  npm install react-router-dom
  ```

- Basic setup:

  ```jsx
  import { BrowserRouter, Routes, Route } from 'react-router-dom';
  
  function App() {
    return (
      <BrowserRouter>
        <Routes>
          <Route path="/" element={<Home />} />
          <Route path="/about" element={<About />} />
          <Route path="/users/:id" element={<User />} />
        </Routes>
      </BrowserRouter>
    );
  }
  ```

## 17. Router Hooks & Links

- useNavigate:

  ```jsx
  import { useNavigate } from 'react-router-dom';
  
  function MyComponent() {
    const navigate = useNavigate();
    
    const handleClick = () => {
      navigate('/about');
    };
    
    return <button onClick={handleClick}>Go to About</button>;
  }
  ```

- Link component:

  ```jsx
  import { Link } from 'react-router-dom';
  
  function Navigation() {
    return (
      <nav>
        <Link to="/">Home</Link>
        <Link to="/about">About</Link>
      </nav>
    );
  }
  ```

- useParams:

  ```jsx
  import { useParams } from 'react-router-dom';
  
  function User() {
    const { id } = useParams();
    return <div>User ID: {id}</div>;
  }
  ```

## 18. Flexbox Components

- Basic flexbox container:

  ```jsx
  const FlexContainer = styled.div`
    display: flex;
    justify-content: space-between;
    align-items: center;
  `;
  ```

- Flexbox item:

  ```jsx
  const FlexItem = styled.div`
    flex: 1;
    margin: 10px;
  `;
  ```

## 19. Axios API Requests

- Installation:

  ```JSX
  npm install axios
  ```

- Basic GET request:

  ```jsx
  import axios from 'axios';
  
  const fetchData = async () => {
    try {
      const response = await axios.get('https://api.example.com/data');
      setData(response.data);
    } catch (error) {
      console.error('Error fetching data:', error);
    }
  };
  ```

- POST request:

  ```jsx
  const createPost = async (post) => {
    try {
      const response = await axios.post('https://api.example.com/posts', post);
      return response.data;
    } catch (error) {
      console.error('Error creating post:', error);
    }
  };
  ```

## 20. Custom Hooks

- Example custom hook:

  ```jsx
  import { useState, useEffect } from 'react';
  
  const useFetch = (url) => {
    const [data, setData] = useState(null);
    const [loading, setLoading] = useState(true);
    const [error, setError] = useState(null);
  
    useEffect(() => {
      const fetchData = async () => {
        try {
          const response = await fetch(url);
          const json = await response.json();
          setData(json);
          setLoading(false);
        } catch (error) {
          setError(error);
          setLoading(false);
        }
      };
  
      fetchData();
    }, [url]);
  
    return { data, loading, error };
  };
  
  // Usage
  const MyComponent = () => {
    const { data, loading, error } = useFetch('https://api.example.com/data');
  
    if (loading) return <div>Loading...</div>;
    if (error) return <div>Error: {error.message}</div>;
    return <div>{/* Render data */}</div>;
  };
  ```

## 21. Context API & useContext Hook

- Create context:

  ```jsx
  import React from 'react';
  
  const MyContext = React.createContext();
  
  export default MyContext;
  ```

- Provide context:

  ```jsx
  import MyContext from './MyContext';
  
  const App = () => {
    const [value, setValue] = useState('Initial value');
  
    return (
      <MyContext.Provider value={{ value, setValue }}>
        <ChildComponent />
      </MyContext.Provider>
    );
  };
  ```

- Use context:

  ```jsx
  import React, { useContext } from 'react';
  import MyContext from './MyContext';
  
  const ChildComponent = () => {
    const { value, setValue } = useContext(MyContext);
  
    return (
      <div>
        <p>Value: {value}</p>
        <button onClick={() => setValue('New value')}>Update Value</button>
      </div>
    );
  };
  ```

## 22. Easy Peasy Redux

- Installation:

  ```JSX
  npm install easy-peasy
  ```

- Create store:

  ```jsx
  import { createStore, action } from 'easy-peasy';
  
  const store = createStore({
    todos: [],
    addTodo: action((state, payload) => {
      state.todos.push(payload);
    }),
  });
  
  export default store;
  ```

- Wrap app with StoreProvider:

  ```jsx
  import { StoreProvider } from 'easy-peasy';
  import store from './store';
  
  const App = () => (
    <StoreProvider store={store}>
      <YourApp />
    </StoreProvider>
  );
  ```

- Use in components:

  ```jsx
  import { useStoreState, useStoreActions } from 'easy-peasy';

  const TodoList = () => {
    const todos = useStoreState(state => state.todos);
    const addTodo = useStoreActions(actions => actions.addTodo);
  
    return (
      <div>
        {todos.map(todo => <div key={todo.id}>{todo.
