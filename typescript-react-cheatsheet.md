# TypeScript and React with TypeScript Course Cheatsheet

## 1. Start Here

- TypeScript: Superset of JavaScript with static typing
- Benefits: Catch errors early, better tooling support, enhanced code readability

## 2. Basic Types

```typescript
// Basic types
let isDone: boolean = false; // Boolean type
let decimal: number = 6; // Number type
let color: string = "blue"; // String type
let list: number[] = [1, 2, 3]; // Array of numbers
let x: [string, number] = ["hello", 10]; // Tuple with a string and a number

// Enum
enum Color {Red, Green, Blue} // Enum with values Red, Green, and Blue
let c: Color = Color.Green; // Variable of type Color, assigned the value Green

// Any
let notSure: any = 4; // Variable of type any, can hold any value

// Void
function warnUser(): void { // Function that returns nothing (void)
    console.log("This is a warning message"); // Logs a warning message
}

// Null and Undefined
let u: undefined = undefined; // Variable of type undefined
let n: null = null; // Variable of type null

// Never
function error(message: string): never { // Function that never returns (throws an error)
    throw new Error(message); // Throws an error with the provided message
}
```

## 3. Arrays & Objects

```typescript
// Array
let list: number[] = [1, 2, 3]; // Array of numbers
let list: Array<number> = [1, 2, 3]; // Array of numbers using generic array type

// Object
let person: { name: string; age: number } = { // Object with properties name (string) and age (number)
    name: "John", // Name property set to "John"
    age: 30 // Age property set to 30
};

// Interface for objects
interface Person { // Interface defining the structure of a Person object
    name: string; // Name property of type string
    age: number; // Age property of type number
}

let john: Person = { // Variable of type Person
    name: "John", // Name property set to "John"
    age: 30 // Age property set to 30
};
```

## 4. Functions

```typescript
// Function declaration
function add(x: number, y: number): number { // Function that takes two numbers and returns a number
    return x + y; // Returns the sum of x and y
}

// Arrow function
const multiply = (x: number, y: number): number => x * y; // Arrow function that multiplies two numbers

// Optional and default parameters
function greet(name: string, greeting?: string): string { // Function with an optional parameter
    if (!greeting) { // If greeting is not provided
        greeting = "Hello"; // Default to "Hello"
    }
    return `${greeting}, ${name}!`; // Return the greeting message
}

// Rest parameters
function sum(...numbers: number[]): number { // Function that takes any number of arguments
    return numbers.reduce((total, n) => total + n, 0); // Returns the sum of all arguments
}
```

## 5. Assertions

```typescript
// Type assertions 
let someValue: any = "this is a string"; // Variable of type any
let strLength: number = (someValue as string).length; // Type assertion to treat someValue as a string

// Non-null assertion
function liveDangerously(x?: number | null) { // Function that takes an optional number or null
    console.log(x!.toFixed()); // Assert that x is non-null and call toFixed
}
```

## 6. Classes

```typescript
class Animal { // Class definition
    private name: string; // Private property

    constructor(name: string) { // Constructor
        this.name = name; // Initialize name property
    }

    public move(distanceInMeters: number = 0) { // Public method with a default parameter
        console.log(`${this.name} moved ${distanceInMeters}m.`); // Log the movement
    }
}

class Dog extends Animal { // Class that extends Animal
    bark() { // Method specific to Dog
        console.log('Woof! Woof!'); // Log a bark
    }
}

const dog = new Dog("Rex"); // Create a new Dog instance
dog.bark(); // Call the bark method
dog.move(10); // Call the move method with a distance
```

## 7. Index Signatures & keyof Assertions

```typescript
// Index signatures
interface StringArray { // Interface for an array of strings
    [index: number]: string; // Index signature
}

let myArray: StringArray = ["Bob", "Fred"]; // Array of strings

// keyof assertions
interface Person { // Interface for a Person
    name: string; // Name property
    age: number; // Age property
}

function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] { // Function to get a property value
    return obj[key]; // Return the property value
}

let person: Person = { name: "John", age: 30 }; // Person object
let name: string = getProperty(person, "name"); // Get the name property
```

## 8. Generics

```typescript
// Generic function
function identity<T>(arg: T): T { // Function with a generic type
    return arg; // Return the argument
}

let output = identity<string>("myString"); // Call the function with a string

// Generic interface
interface GenericIdentityFn<T> { // Interface with a generic type
    (arg: T): T; // Function signature
}

let myIdentity: GenericIdentityFn<number> = identity; // Assign the function to the interface

// Generic classes
class GenericNumber<T> { // Class with a generic type
    zeroValue: T; // Property of type T
    add: (x: T, y: T) => T; // Method that takes two arguments of type T and returns a T
}
```

## 9. Utility Types

```typescript
// Partial
interface Todo { // Interface for a Todo item
    title: string; // Title property
    description: string; // Description property
}

function updateTodo(todo: Todo, fieldsToUpdate: Partial<Todo>) { // Function to update a Todo item
    return { ...todo, ...fieldsToUpdate }; // Return the updated Todo item
}

// Pick
type TodoPreview = Pick<Todo, "title">; // Type that picks the title property from Todo

// Omit
type TodoInfo = Omit<Todo, "completed">; // Type that omits the completed property from Todo

// ReturnType
type T0 = ReturnType<() => string>;  // Type that represents the return type of a function
```

## 10. Vite.js + TypeScript

- Vite: Next-generation frontend tooling
- Setup: `npm create vite@latest my-vue-app -- --template react-ts`

## 11. TypeScript Project

- Implement a project using TypeScript concepts learned

## 12. React + TypeScript

```typescript
// Functional component with props
interface GreetingProps { // Interface for component props
    name: string; // Name property
}

const Greeting: React.FC<GreetingProps> = ({ name }) => { // Functional component
    return <h1>Hello, {name}!</h1>; // Return a greeting message
};

// Class component
interface CounterState { // Interface for component state
    count: number; // Count property
}

class Counter extends React.Component<{}, CounterState> { // Class component
    state: CounterState = { // Initial state
        count: 0 // Count set to 0
    };

    increment = () => { // Method to increment the count
        this.setState(prevState => ({ // Update the state
            count: prevState.count + 1 // Increment the count
        }));
    };

    render() { // Render method
        return ( // Return the component UI
            <div>
                <p>Count: {this.state.count}</p> // Display the count
                <button onClick={this.increment}>Increment</button> // Button to increment the count
            </div>
        );
    }
}
```

## 13. React Hooks + TypeScript

```typescript
// useState
const [count, setCount] = useState<number>(0); // useState hook with a number type

// useEffect
useEffect(() => { // useEffect hook
    document.title = `You clicked ${count} times`; // Update the document title
}, [count]); // Dependency array

// Custom hook
function useCounter(initialValue: number = 0) { // Custom hook with an initial value
    const [count, setCount] = useState<number>(initialValue); // useState hook
    const increment = () => setCount(prev => prev + 1); // Increment function
    const decrement = () => setCount(prev => prev - 1); // Decrement function
    return { count, increment, decrement }; // Return the state and functions
}
```

## 14. React useReducer + TypeScript

```typescript
type CounterState = { count: number }; // Type for the state
type CounterAction = // Type for the actions
  | { type: 'increment' }
  | { type: 'decrement' }
  | { type: 'reset', payload: number };

const counterReducer = (state: CounterState, action: CounterAction): CounterState => { // Reducer function
    switch (action.type) { // Switch on the action type
        case 'increment': // Increment case
            return { count: state.count + 1 }; // Increment the count
        case 'decrement': // Decrement case
            return { count: state.count - 1 }; // Decrement the count
        case 'reset': // Reset case
            return { count: action.payload }; // Reset the count
        default: // Default case
            return state; // Return the current state
    }
};

function Counter() { // Counter component
    const [state, dispatch] = useReducer(counterReducer, { count: 0 }); // useReducer hook

    return ( // Return the component UI
        <>
            Count: {state.count} // Display the count
            <button onClick={() => dispatch({ type: 'increment' })}>+</button> // Button to increment the count
            <button onClick={() => dispatch({ type: 'decrement' })}>-</button> // Button to decrement the count
            <button onClick={() => dispatch({ type: 'reset', payload: 0 })}>Reset</button> // Button to reset the count
        </>
    );
}
```

## 15. React useContext + TypeScript

```typescript
interface ThemeContextType { // Interface for the context
    theme: string; // Theme property
    toggleTheme: () => void; // Function to toggle the theme
}

const ThemeContext = React.createContext<ThemeContextType | undefined>(undefined); // Create the context

function ThemeProvider({ children }: { children: React.ReactNode }) { // Theme provider component
    const [theme, setTheme] = useState<string>('light'); // useState hook for the theme
    const toggleTheme = () => { // Function to toggle the theme
        setTheme(prev => prev === 'light' ? 'dark' : 'light'); // Toggle between light and dark
    };

    return ( // Return the provider
        <ThemeContext.Provider value={{ theme, toggleTheme }}> // Provide the context value
            {children} // Render the children
        </ThemeContext.Provider>
    );
}

function useTheme() { // Custom hook to use the theme context
    const context = useContext(ThemeContext); // Get the context value
    if (context === undefined) { // If the context is undefined
        throw new Error('useTheme must be used within a ThemeProvider'); // Throw an error
    }
    return context; // Return the context value
}

function ThemedButton() { // Themed button component
    const { theme, toggleTheme } = useTheme(); // Use the custom hook
    return ( // Return the button
        <button onClick={toggleTheme} style={{ background: theme === 'light' ? '#fff' : '#000' }}> // Set the background color
            Toggle Theme // Button text
        </button>
    );
}
```
