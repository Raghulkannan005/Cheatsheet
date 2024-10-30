# TypeScript and React with TypeScript Course Cheatsheet

## 1. Start Here
- TypeScript: Superset of JavaScript with static typing
- Benefits: Catch errors early, better tooling support, enhanced code readability

## 2. Basic Types
```typescript
// Basic types
let isDone: boolean = false;
let decimal: number = 6;
let color: string = "blue";
let list: number[] = [1, 2, 3];
let x: [string, number] = ["hello", 10]; // Tuple

// Enum
enum Color {Red, Green, Blue}
let c: Color = Color.Green;

// Any
let notSure: any = 4;

// Void
function warnUser(): void {
    console.log("This is a warning message");
}

// Null and Undefined
let u: undefined = undefined;
let n: null = null;

// Never
function error(message: string): never {
    throw new Error(message);
}
```

## 3. Arrays & Objects
```typescript
// Array
let list: number[] = [1, 2, 3];
let list: Array<number> = [1, 2, 3];

// Object
let person: { name: string; age: number } = {
    name: "John",
    age: 30
};

// Interface for objects
interface Person {
    name: string;
    age: number;
}

let john: Person = {
    name: "John",
    age: 30
};
```

## 4. Functions
```typescript
// Function declaration
function add(x: number, y: number): number {
    return x + y;
}

// Arrow function
const multiply = (x: number, y: number): number => x * y;

// Optional and default parameters
function greet(name: string, greeting?: string): string {
    if (!greeting) {
        greeting = "Hello";
    }
    return `${greeting}, ${name}!`;
}

// Rest parameters
function sum(...numbers: number[]): number {
    return numbers.reduce((total, n) => total + n, 0);
}
```

## 5. Assertions
```typescript
// Type assertions
let someValue: any = "this is a string";
let strLength: number = (someValue as string).length;

// Non-null assertion
function liveDangerously(x?: number | null) {
    console.log(x!.toFixed()); // Assert that x is non-null
}
```

## 6. Classes
```typescript
class Animal {
    private name: string;
    
    constructor(name: string) {
        this.name = name;
    }
    
    public move(distanceInMeters: number = 0) {
        console.log(`${this.name} moved ${distanceInMeters}m.`);
    }
}

class Dog extends Animal {
    bark() {
        console.log('Woof! Woof!');
    }
}

const dog = new Dog("Rex");
dog.bark();
dog.move(10);
```

## 7. Index Signatures & keyof Assertions
```typescript
// Index signatures
interface StringArray {
    [index: number]: string;
}

let myArray: StringArray = ["Bob", "Fred"];

// keyof assertions
interface Person {
    name: string;
    age: number;
}

function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
    return obj[key];
}

let person: Person = { name: "John", age: 30 };
let name: string = getProperty(person, "name");
```

## 8. Generics
```typescript
// Generic function
function identity<T>(arg: T): T {
    return arg;
}

let output = identity<string>("myString");

// Generic interface
interface GenericIdentityFn<T> {
    (arg: T): T;
}

let myIdentity: GenericIdentityFn<number> = identity;

// Generic classes
class GenericNumber<T> {
    zeroValue: T;
    add: (x: T, y: T) => T;
}
```

## 9. Utility Types
```typescript
// Partial
interface Todo {
    title: string;
    description: string;
}

function updateTodo(todo: Todo, fieldsToUpdate: Partial<Todo>) {
    return { ...todo, ...fieldsToUpdate };
}

// Pick
type TodoPreview = Pick<Todo, "title">;

// Omit
type TodoInfo = Omit<Todo, "completed">;

// ReturnType
type T0 = ReturnType<() => string>;  // string
```

## 10. Vite.js + TypeScript
- Vite: Next-generation frontend tooling
- Setup: `npm create vite@latest my-vue-app -- --template react-ts`

## 11. TypeScript Project
- Implement a project using TypeScript concepts learned

## 12. React + TypeScript
```typescript
// Functional component with props
interface GreetingProps {
    name: string;
}

const Greeting: React.FC<GreetingProps> = ({ name }) => {
    return <h1>Hello, {name}!</h1>;
};

// Class component
interface CounterState {
    count: number;
}

class Counter extends React.Component<{}, CounterState> {
    state: CounterState = {
        count: 0
    };

    increment = () => {
        this.setState(prevState => ({
            count: prevState.count + 1
        }));
    };

    render() {
        return (
            <div>
                <p>Count: {this.state.count}</p>
                <button onClick={this.increment}>Increment</button>
            </div>
        );
    }
}
```

## 13. React Hooks + TypeScript
```typescript
// useState
const [count, setCount] = useState<number>(0);

// useEffect
useEffect(() => {
    document.title = `You clicked ${count} times`;
}, [count]);

// Custom hook
function useCounter(initialValue: number = 0) {
    const [count, setCount] = useState<number>(initialValue);
    const increment = () => setCount(prev => prev + 1);
    const decrement = () => setCount(prev => prev - 1);
    return { count, increment, decrement };
}
```

## 14. React useReducer + TypeScript
```typescript
type CounterState = { count: number };
type CounterAction = 
  | { type: 'increment' }
  | { type: 'decrement' }
  | { type: 'reset', payload: number };

const counterReducer = (state: CounterState, action: CounterAction): CounterState => {
    switch (action.type) {
        case 'increment':
            return { count: state.count + 1 };
        case 'decrement':
            return { count: state.count - 1 }; 
        case 'reset':
            return { count: action.payload };
        default:
            return state;
    }
};

function Counter() {
    const [state, dispatch] = useReducer(counterReducer, { count: 0 });

    return (
        <>
            Count: {state.count}
            <button onClick={() => dispatch({ type: 'increment' })}>+</button>
            <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
            <button onClick={() => dispatch({ type: 'reset', payload: 0 })}>Reset</button>
        </>
    );
}
```

## 15. React useContext + TypeScript
```typescript
interface ThemeContextType {
    theme: string;
    toggleTheme: () => void;
}

const ThemeContext = React.createContext<ThemeContextType | undefined>(undefined);

function ThemeProvider({ children }: { children: React.ReactNode }) {
    const [theme, setTheme] = useState<string>('light');
    const toggleTheme = () => {
        setTheme(prev => prev === 'light' ? 'dark' : 'light');
    };

    return (
        <ThemeContext.Provider value={{ theme, toggleTheme }}>
            {children}
        </ThemeContext.Provider>
    );
}

function useTheme() {
    const context = useContext(ThemeContext);
    if (context === undefined) {
        throw new Error('useTheme must be used within a ThemeProvider');
    }
    return context;
}

function ThemedButton() {
    const { theme, toggleTheme } = useTheme();
    return (
        <button onClick={toggleTheme} style={{ background: theme === 'light' ? '#fff' : '#000' }}>
            Toggle Theme
        </button>
    );
}
```

## 16 & 17. React + TypeScript Project
- Implement a full React project using TypeScript
- Apply concepts learned throughout the course
- Best practices:
  - Use interfaces for prop types
  - Leverage TypeScript's type inference when possible
  - Use union types for component states
  - Create custom hooks with proper typing
  - Use generics for reusable components and functions
