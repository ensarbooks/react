# 1. Getting Started with React

Getting started with React involves setting up your development environment and creating your first React application. React is a JavaScript library for building user interfaces, and the recommended way to start a new project is to use an integrated toolchain. Modern toolchains handle bundling, transpiling, and development server setup for you, making it easier to get up and running quickly. The React team suggests using **Create React App** for single-page apps or Next.js for server-rendered apps ([Create a New React App – React](https://legacy.reactjs.org/docs/create-a-new-react-app.html#:~:text=The%20React%20team%20primarily%20recommends,these%20solutions))  In this chapter, we’ll focus on Create React App to scaffold a React project.

### Setting up the Environment

1. **Install Node.js and npm:** React development requires Node.js (which comes with npm). Ensure you have Node.js (version 14 or above) and npm installed on your system ([Create a New React App – React](https://legacy.reactjs.org/docs/create-a-new-react-app.html#:~:text=It%20sets%20up%20your%20development,To%20create%20a%20project%2C%20run))  You can verify the installation by running `node -v` and `npm -v` in your terminal.
2. **Create a New React App:** Use the **Create React App** tool to generate a new project structure. You can do this with a single npx command:  
   ```bash
   npx create-react-app my-app
   cd my-app
   npm start
   ```  
   This will scaffold a new React application in the `my-app` directory and start the development server ([Create a New React App – React](https://legacy.reactjs.org/docs/create-a-new-react-app.html#:~:text=It%20sets%20up%20your%20development,To%20create%20a%20project%2C%20run))  Running `npm start` launches a local dev server (usually at **http://localhost:3000**) with hot reloading.
3. **Project Structure:** After creation, you'll have a project structure with essential files: an entry point `index.js`, a root component `App.js`, and configuration for build tools. Create React App sets up everything using **Webpack** and **Babel** behind the scenes (no manual config needed) ([Create a New React App – React](https://legacy.reactjs.org/docs/create-a-new-react-app.html#:~:text=Create%20React%20App%20doesn%E2%80%99t%20handle,to%20know%20anything%20about%20them))  You can open the project in your editor to explore the files.

When the dev server starts, a browser window opens with the React welcome screen, confirming that React is installed and running. At this point, you can edit `src/App.js`, save, and see updates live in the browser, thanks to the development server’s hot-reloading feature ([How To Install React on Windows, macOS, and Linux - Kinsta®](https://kinsta.com/knowledgebase/install-react/#:~:text=npm%20start)) 

### Your First Component

Once setup is complete, try creating a simple component to verify things are working. Open `App.js` and modify it to render a greeting:

```jsx
function App() {
  return <h1>Hello, React!</h1>;
}
```

Save the file, and the browser should auto-reload to show **“Hello, React!”**. Congratulations – you have a running React app! From here, you can start building out the application by adding more components and features. As you proceed, remember that Create React App supports all modern JS features and optimizes the app for production when you run `npm run build`. It provides a great starting point with a lot of best practices configured for you ([Create a New React App – React](https://legacy.reactjs.org/docs/create-a-new-react-app.html#:~:text=It%20sets%20up%20your%20development,To%20create%20a%20project%2C%20run)) 

**Best Practices & Tips:** During setup, use the latest LTS version of Node.js for stability. Keep your React and Create React App versions up to date for the best features and fixes. Also, note that Create React App is ideal for learning and simple deployments; for larger apps or server-side rendering, consider frameworks like Next.js which come with routing and SSR built-in ([Create a New React App – React](https://legacy.reactjs.org/docs/create-a-new-react-app.html#:~:text=,oriented%20website%2C%20try%20Gatsby))  Next, we'll dive into the fundamentals of React development by exploring components and JSX.

**Sources:** Create React App documentation ([Create a New React App – React](https://legacy.reactjs.org/docs/create-a-new-react-app.html#:~:text=It%20sets%20up%20your%20development,To%20create%20a%20project%2C%20run)) 
---

# 2. Components and JSX

React’s core building blocks are **components** and its syntax extension **JSX**. In this chapter, we’ll explain what components are, how JSX works, and how to use them together to build UIs. React embraces a component-based architecture: each piece of your UI is defined as a component, which can be reused and composed to form complex interfaces ([Components and Props – React](https://legacy.reactjs.org/docs/components-and-props.html#:~:text=Components%20let%20you%20split%20the,detailed%20component%20API%20reference%20here)) 

### Understanding JSX

JSX (JavaScript XML) is a syntax extension for JavaScript that looks similar to HTML. It allows you to write markup directly within JavaScript, which React then transforms into native DOM operations. For example: 

```jsx
const element = <h1>Hello, world!</h1>;
``` 

This JSX snippet is **not** a string or raw HTML; it gets compiled to a `React.createElement` call behind the scenes. JSX makes writing UI easier by letting you mix HTML-like syntax with JavaScript. We **highly recommend using JSX** to describe your UI, as it’s more intuitive and powerful (you can embed JS expressions, reference variables, etc.) ([Introducing JSX – React](https://legacy.reactjs.org/docs/introducing-jsx.html#:~:text=This%20funny%20tag%20syntax%20is,neither%20a%20string%20nor%20HTML))  JSX produces React “elements,” which are the building blocks of React’s virtual DOM ([Introducing JSX – React](https://legacy.reactjs.org/docs/introducing-jsx.html#:~:text=It%20is%20called%20JSX%2C%20and,the%20full%20power%20of%20JavaScript))  Key points about JSX:

- **It’s an Extension:** JSX isn’t valid JavaScript by itself – your build tool (like Babel) transforms it into `React.createElement` calls. For example, `<h1>Hello</h1>` becomes `React.createElement('h1', null, 'Hello')`.
- **Embedding JavaScript:** You can embed any JavaScript expression in JSX by using curly braces `{ }`. For instance:  
  ```jsx
  const name = 'Alice';
  const greeting = <h2>Hello, {name}!</h2>;
  ```  
  Here, `{name}` gets evaluated and inserted into the JSX output ([Introducing JSX – React](https://legacy.reactjs.org/docs/introducing-jsx.html#:~:text=Embedding%20Expressions%20in%20JSX)) 
- **Attributes & Props:** JSX uses camelCase for attributes (e.g., `onClick` instead of `onclick`, `className` instead of `class`). You can pass values (including variables or results of expressions) as props to components in JSX.

JSX might remind you of a template language, but it comes with the **full power of JavaScript** – you can use loops, conditionals, and all JS features inside curly braces. It also helps React show more useful error messages by pinpointing issues in your markup. Remember, though, that **JSX is optional** – you could use plain JS `React.createElement` calls – but most developers prefer JSX for its readability ([Introducing JSX – React](https://legacy.reactjs.org/docs/introducing-jsx.html#:~:text=React%20doesn%E2%80%99t%20require%20using%20JSX%2C,useful%20error%20and%20warning%20messages)) 

### Creating Components

A **component** in React is essentially a reusable piece of UI, defined as a JavaScript function or class. Components allow you to break the UI into independent, reusable parts and think about each in isolation ([Components and Props – React](https://legacy.reactjs.org/docs/components-and-props.html#:~:text=Components%20let%20you%20split%20the,detailed%20component%20API%20reference%20here))  There are two main ways to define a React component:

- **Function Components:** The simplest way, using a JavaScript function.  
- **Class Components:** An older approach, using ES6 classes.

**Function Component Example:**  
```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```  
This is a valid React component because it accepts an argument (`props`) and returns JSX that describes what to render ([Components and Props – React](https://legacy.reactjs.org/docs/components-and-props.html#:~:text=The%20simplest%20way%20to%20define,to%20write%20a%20JavaScript%20function))  You can use this component in JSX as `<Welcome name="Alice" />`, passing a `name` prop.

**Class Component Example:**  
```jsx
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```  
This class extends `React.Component` and implements a `render()` method that returns JSX. Functionally, it’s equivalent to the function component above ([Components and Props – React](https://legacy.reactjs.org/docs/components-and-props.html#:~:text=You%20can%20also%20use%20an,class%20to%20define%20a%20component))  In modern React, function components with Hooks are more common, but you may encounter class components in older codebases.

When React sees an element like `<Welcome name="Sara" />`, it will **call your component** (`Welcome`) with the props `{name: 'Sara'}`. The component returns a React element (in this case `<h1>Hello, Sara</h1>`), and React efficiently updates the DOM to match that output ([Components and Props – React](https://legacy.reactjs.org/docs/components-and-props.html#:~:text=const%20element%20%3D%20%3CWelcome%20name%3D,))  ([Components and Props – React](https://legacy.reactjs.org/docs/components-and-props.html#:~:text=Let%E2%80%99s%20recap%20what%20happens%20in,this%20example))  **Props** are the inputs to components – they are passed in like function arguments. A component must never modify its own props; they should be treated as read-only. If you need interactive or changing data, that’s what **state** is for (covered in the next chapter).

**Key things about components:**

- Always start component names with a capital letter. React treats lowercase tags as DOM elements, and capitalized ones as user-defined components ([Components and Props – React](https://legacy.reactjs.org/docs/components-and-props.html#:~:text=,For)) 
- Components can be composed: a component can use (render) other components inside it, enabling complex UIs built from simple building blocks.
- Components can have **children**: props can include special `props.children` for any nested JSX inside the component tag.

By using components and JSX, you can structure your app into small, testable pieces. For example, you might have an `App` component that renders a `<Header />`, a `<Sidebar />`, and a `<Content />` component. Each of those might render other components, and so on, forming a tree. JSX makes it straightforward to visualize this structure in your code. Next, we’ll see how components manage data through state and props, and handle user events.

**Sources:** Introducing JSX (React docs) ([Introducing JSX – React](https://legacy.reactjs.org/docs/introducing-jsx.html#:~:text=This%20funny%20tag%20syntax%20is,neither%20a%20string%20nor%20HTML))  Components and Props (React docs) ([Components and Props – React](https://legacy.reactjs.org/docs/components-and-props.html#:~:text=Components%20let%20you%20split%20the,detailed%20component%20API%20reference%20here))  ([Components and Props – React](https://legacy.reactjs.org/docs/components-and-props.html#:~:text=The%20simplest%20way%20to%20define,to%20write%20a%20JavaScript%20function)) 
---

# 3. State, Props, and Event Handling

Components by themselves are useful, but they become powerful when they can hold and manage data (state), receive inputs (props), and respond to user interactions (events). In this chapter, we cover **state vs. props**, how to update state, and how to handle events like clicks and form submissions in React.

### Props vs. State

- **Props:** (short for “properties”) are inputs to a component, passed from a parent component. Props are **read-only** in the child; a component cannot change its own props. They are similar to function arguments. For example, `<Welcome name="Alice" />` passes a prop `name` with value `"Alice"` to the `Welcome` component.
- **State:** represents data that is local to a component and can change over time. State is managed *within* the component (unlike props which come from outside). When a component’s state changes, the component re-renders to reflect those changes.

A key difference is that **state is internal and mutable**, while **props are external and immutable (from the component’s perspective)**. State allows components to track information that may change due to user input, network responses, etc. For example, a form component might have state for the current input value. React provides APIs (like the `useState` Hook or `this.setState` in class components) to manage state updates.

**Important:** *“State is similar to props, but it is private and fully controlled by the component.”* ([State and Lifecycle – React](https://legacy.reactjs.org/docs/state-and-lifecycle.html#:~:text=To%20implement%20this%2C%20we%20need,component)) Unlike props which are passed in, state is owned by the component itself. This means you use state for data that a component can change, and use props to pass data **into** child components.

In a class component, you initialize state by setting `this.state` in the constructor, and update it with `this.setState()`. In a function component, you initialize state with the `useState` Hook and get a setter function to update it. We’ll explore Hooks in a later chapter; for now, just understand that updating state triggers a re-render of the component.

### Updating State Correctly

To modify state, never mutate it directly. For example, avoid `this.state.count = 1` to change a value – this won’t re-render the component. Instead, use `setState` (class) or the state updater from `useState` (function). React’s state updates may be asynchronous and batched, so relying on immediate state changes is a common pitfall. Always use the provided setter to ensure React knows about the change.

For instance, in a class: 
```js
// Wrong - direct mutation
this.state.value = newValue; 

// Right - use setState
this.setState({ value: newValue });
``` 

And in a function:
```jsx
const [value, setValue] = useState(0);
// ...
setValue(newValue);
```

React will merge state updates and schedule a re-render. If new state depends on the old state, use the functional form of setState or updater function (`setValue(prev => ...)`) to get the correct previous value.

### Handling Events in React

Handling events in React elements is very similar to handling DOM events, with a few syntax differences:

- React event handler props are **camelCase** (e.g., `onClick` rather than `onclick`).
- You pass a **function** as the event handler, rather than a string of code as in HTML. For example:  
  ```jsx
  <button onClick={handleSave}>Save</button>
  ```  
  Here `handleSave` is a function defined in your component, not a string. In HTML you might do `<button onclick="handleSave()">`, but in JSX it’s `{handleSave}` (no quotes) ([Handling Events – React](https://legacy.reactjs.org/docs/handling-events.html#:~:text=Handling%20events%20with%20React%20elements,There%20are%20some%20syntax%20differences)) 
- Event objects in React are **SyntheticEvents**, which are cross-browser wrapper events. They work largely the same as native events and have the same properties (`preventDefault()`, `stopPropagation()`, etc.).

**Example – Handling a Click:**  
```jsx
function MyComponent() {
  function handleClick(event) {
    console.log('Button clicked!');
  }
  return <button onClick={handleClick}>Click Me</button>;
}
```  
When the button is clicked, `handleClick` is called. React passes the event object as `event` (you can also omit the param if not needed). 

If you want to prevent the default browser behavior (for example, a form submission reloading the page), call `event.preventDefault()` inside your handler. For instance, in a form submit handler:  
```jsx
function handleSubmit(e) {
  e.preventDefault(); // Prevent page reload
  // handle form data...
}
```  
In React, you **must** call `preventDefault()` to stop default behaviors; returning `false` from the handler will **not** work as it might in plain HTML/JS ([Handling Events – React](https://legacy.reactjs.org/docs/handling-events.html#:~:text=Another%20difference%20is%20that%20you,of%20submitting%2C%20you%20can%20write)) 

**Common Event Handling Patterns:**

- **Passing Arguments:** To pass extra data to an event handler, you can use an inline arrow function. E.g., `<button onClick={() => deleteItem(id)}>Delete</button>`. This ensures `deleteItem` is called with `id` when clicked.
- **This Binding (for class components):** In class components, event handler methods often need to be bound to `this`. You can do this in the constructor: `this.handleClick = this.handleClick.bind(this)`, or use class fields / arrow functions to avoid manual binding. Forgetting to bind is a common source of errors (the function loses the correct `this` context). With function components and Hooks, this isn’t an issue since there’s no `this`.

**Example – Toggle Component (Class):**  
```jsx
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = { isOn: true };
    this.handleClick = this.handleClick.bind(this);
  }
  handleClick() {
    this.setState(prevState => ({ isOn: !prevState.isOn }));
  }
  render() {
    return (
      <button onClick={this.handleClick}>
        {this.state.isOn ? 'ON' : 'OFF'}
      </button>
    );
  }
}
```  
Here we bind `handleClick` in the constructor so that it can use `this.setState` correctly when invoked. Clicking the button toggles the text between “ON” and “OFF” by updating state ([Handling Events – React](https://legacy.reactjs.org/docs/handling-events.html#:~:text=class%20Toggle%20extends%20React.Component%20,isToggleOn%3A%20true))  ([Handling Events – React](https://legacy.reactjs.org/docs/handling-events.html#:~:text=handleClick%28%29%20,button%3E%20%29%3B)) 

**Props and Data Flow:** Props are how parent components convey data to children. For example, a parent could handle an event and then pass a new prop to a child to reflect a change. Props can be any type: strings, numbers, objects, or even functions (callback props). A common pattern is passing a function from parent to child as a prop so the child can notify the parent of some event (e.g., a child component calls `props.onSave()` when a save button is clicked, and the parent handles it).

**Summary:** Use **props** for input data to components, and use **state** for data that a component manages itself. Update state with the provided methods to trigger re-renders. Handle events by defining functions and attaching them to JSX with camelCase event props. React’s event system will ensure your handlers are called with SyntheticEvents which are consistent across browsers. With state, props, and event handling in hand, you can create interactive components that respond to user input and update the UI accordingly.

**Sources:** React State vs Props ([State and Lifecycle – React](https://legacy.reactjs.org/docs/state-and-lifecycle.html#:~:text=To%20implement%20this%2C%20we%20need,component))  Handling Events (React docs) ([Handling Events – React](https://legacy.reactjs.org/docs/handling-events.html#:~:text=Handling%20events%20with%20React%20elements,There%20are%20some%20syntax%20differences)) 
---

# 4. React Performance Optimization

As your React application grows, you may need to optimize performance to keep the UI snappy. React is fast by default thanks to its virtual DOM and diffing algorithm, but there are strategies to further improve performance in specific scenarios. In this chapter, we’ll discuss techniques like avoiding unnecessary re-renders, using `React.memo`, `useMemo`/`useCallback` Hooks, virtualization for long lists, and code-splitting. We’ll also touch on profiling tools to help find bottlenecks.

### Understanding Re-renders and Reconciliation

React re-renders a component when its state or props change. After rendering, it **reconciles** the new output with the previous output and updates the DOM minimally. If a parent re-renders, by default all its children do too (though React skips DOM updates for parts that haven’t changed). Unnecessary re-renders can impact performance, especially if the component tree is large or rendering is expensive.

**shouldComponentUpdate and PureComponent (Class Components):** In class components, you can override the `shouldComponentUpdate(nextProps, nextState)` lifecycle method to control whether a component updates. By default, it returns `true` (update on every state/prop change). If you know a component doesn’t need to update under certain conditions (e.g., props didn’t actually change), returning `false` can skip a re-render for that component and its children ([Optimizing Performance – React](https://legacy.reactjs.org/docs/optimizing-performance.html#:~:text=Even%20though%20React%20only%20updates,React%20to%20perform%20the%20update))  ([Optimizing Performance – React](https://legacy.reactjs.org/docs/optimizing-performance.html#:~:text=If%20you%20know%20that%20in,on%20this%20component%20and%20below))  Implementing `shouldComponentUpdate` manually involves comparing current props/state to next props/state. React provides `React.PureComponent` as a base class that implements a **shallow comparison** of props and state, effectively providing a `shouldComponentUpdate` for you ([Optimizing Performance – React](https://legacy.reactjs.org/docs/optimizing-performance.html#:~:text=If%20you%20know%20that%20in,on%20this%20component%20and%20below))  If your component extends PureComponent, it will automatically skip re-renders if props and state are the same (by shallow equality). Be cautious: PureComponent does a shallow compare, so if you mutate objects/arrays in state, it may not detect changes correctly. Always update state immutably to benefit from PureComponent.

**React.memo (Function Components):** For function components, you can wrap them with `React.memo` to get a similar behavior. `React.memo(Component)` returns a new component that memoizes the result – it will do a shallow prop comparison and only re-render the wrapped component if props change. This is great for pure components that render the same output given the same props. If you need a custom comparison (deeper compare or skipping certain props), `React.memo` accepts a second argument to provide your own comparison function.

### Using useMemo and useCallback

React Hooks provide additional tools to optimize expensive calculations or to prevent unnecessary re-rendering of child components:

- **useMemo:** `const memoizedValue = useMemo(fn, [deps])` will run `fn` and memoize its result, recomputing only when the dependencies `[deps]` change. This is useful for expensive computations or generating derived data so that you don’t recompute on every render unnecessarily. Example: computing a filtered list or expensive math – wrap it in useMemo to reuse the last result until inputs change.
- **useCallback:** `const memoizedCallback = useCallback(fn, [deps])` returns a memoized version of a callback function that only changes if the dependencies change. This is useful to avoid re-creating functions every render, which can be important when passing callbacks to optimized child components (like a `React.memo` child that might otherwise re-render because a new prop function is passed each time). Essentially, **useCallback caches a function** definition, and **useMemo caches a value**. 

Using these hooks can improve performance by avoiding recalculations or re-renders. However, **don’t overuse them** – they themselves add a bit of complexity. Use them when a particular operation is proven to be a bottleneck or when working with large data sets. *“These hooks allow you to cache data or functions, preventing unnecessary re-renders and improving the overall performance of your application.”* ([Optimizing React Components: A Guide to useCallback and useMemo - DEV Community](https://dev.to/dickinsontiwari/optimizing-react-components-a-guide-to-usecallback-and-usememo-3mgk#:~:text=In%20the%20world%20of%20React%2C,illustrate%20when%20to%20use%20each)) 
**Example:** Suppose you have a list component that renders a big list of items and a filter input. You compute the filtered list inside the component. Without useMemo, each keystroke in an unrelated part of the app could trigger a re-render and recompute the filtering. By wrapping the filter logic in `useMemo` with `[searchTerm, items]` as deps, the filtered result will only recompute when the search term or items actually change, not on every render. Similarly, if you pass an `onClickItem` handler to each list item component, wrapping that handler definition in `useCallback` (with dependencies like item id if needed) will avoid redefining the function on every parent render, which helps if those item components are `React.memo`-ed.

### Virtualize Long Lists

If your app needs to display **very long lists or tables** (hundreds or thousands of items), rendering them all to the DOM can be slow. Instead, use **windowing/virtualization** to render only what’s visible. Libraries like **react-window** and **react-virtualized** allow you to render a small subset of list items at a time (for example, only the items within or near the scroll viewport) ([Optimizing Performance – React](https://legacy.reactjs.org/docs/optimizing-performance.html#:~:text=Virtualize%20Long%20Lists))  ([Optimizing Performance – React](https://legacy.reactjs.org/docs/optimizing-performance.html#:~:text=react,your%20application%E2%80%99s%20specific%20use%20case))  As the user scrolls, the library reuses and swaps out elements, dramatically reducing the DOM node count and rendering work. This technique can vastly improve performance for large lists by **avoiding rendering off-screen content**.

Popular choices for list virtualization:
- **react-window** – lightweight, great for simple fixed-size lists and grids ([Optimizing Performance – React](https://legacy.reactjs.org/docs/optimizing-performance.html#:~:text=react,your%20application%E2%80%99s%20specific%20use%20case)) 
- **react-virtualized** – older library with more features for tables, etc. ([Optimizing Performance – React](https://legacy.reactjs.org/docs/optimizing-performance.html#:~:text=react,your%20application%E2%80%99s%20specific%20use%20case)) 

By virtualizing, you trade a bit of scrolling complexity for a big performance win when dealing with large datasets.

### Code-Splitting (Lazy Loading)

Code-splitting is about improving the **initial load performance**. Instead of loading your entire app JavaScript bundle at once, you split the code into chunks and lazy-load parts of the app on demand (for example, load admin dashboard code only when the user navigates to `/admin`). In React, you can achieve this with `React.lazy()` and `<Suspense>` for component-level splitting ([Code splitting with React.lazy and Suspense | Articles - web.dev](https://web.dev/articles/code-splitting-suspense#:~:text=The%20React,it%20along%20with%20Suspense))  or use a routing library that supports dynamic imports.

Example using React lazy and Suspense:
```jsx
const SettingsPage = React.lazy(() => import('./SettingsPage'));

<Router>
  <Route path="/settings" element={
    <Suspense fallback={<div>Loading...</div>}>
      <SettingsPage />
    </Suspense>
  } />
</Router>
```
Here, the SettingsPage component code will be loaded only when the user navigates to the /settings route. This reduces the initial bundle size, speeding up load for users who may never visit certain parts of the app. Just remember to wrap lazy components with `<Suspense>` and provide a fallback UI (like a loading spinner) while the chunk loads.

### Avoiding Common Performance Pitfalls

- **Avoid Heavy Computation in Render:** Don’t perform expensive calculations or data transformations directly in your component’s render function without memoization. If you have to, use `useMemo` or compute outside of render.
- **Optimize Reconciliation:** Try to minimize unnecessary re-renders. Use `React.memo`/PureComponent for components that often receive the same props. However, only do this for components that re-render frequently or are expensive to render – over-optimizing can add overhead.
- **Immutable Data:** Update state immutably (return new objects/arrays instead of mutating) so that comparisons (like PureComponent’s shallow compare) work correctly. This also helps avoid subtle bugs and makes tracking changes easier.
- **Use the Production Build:** Always test performance in the production build of React. Development mode includes extra checks and warnings that make it slower. Running `npm run build` gives you an optimized production bundle (with things like minified code and removed propType checks) which can significantly improve performance.

### Profiling and Analyzing Performance

React Developer Tools includes a **Profiler** that helps measure rendering performance. In your browser’s React DevTools, there’s a “Profiler” tab where you can record interactions and see what components rendered and how long they took. This helps identify slow components or unnecessary renders. *“An overview of the Profiler can be found in the blog post "Introducing the React Profiler".* ([Optimizing Performance – React](https://legacy.reactjs.org/docs/optimizing-performance.html#:~:text=Profiling%20Components%20with%20the%20DevTools,Profiler)) Using the Profiler, you might discover, for example, that a component re-rendered 10 times when it only needed to once – leading you to apply `React.memo` or adjust your state structure.

Additionally, analyze bundle size with tools like Webpack Bundle Analyzer to see if code-splitting is needed, and use browser devtools performance timeline to spot layout or paint issues (though React generally manages DOM updates efficiently).

**In summary**, focus on **render optimization** (skip work when not needed) and **load optimization** (don’t load what isn’t needed yet). Techniques like memoization, list virtualization, and code splitting, combined with proper profiling, will help your React apps remain fast as they scale. Always measure first – identify hot spots – and then apply these optimizations as necessary for a smooth user experience.

**Sources:** Avoiding unnecessary re-renders with PureComponent ([Optimizing Performance – React](https://legacy.reactjs.org/docs/optimizing-performance.html#:~:text=If%20you%20know%20that%20in,on%20this%20component%20and%20below))  useCallback and useMemo for caching values/functions ([Optimizing React Components: A Guide to useCallback and useMemo - DEV Community](https://dev.to/dickinsontiwari/optimizing-react-components-a-guide-to-usecallback-and-usememo-3mgk#:~:text=In%20the%20world%20of%20React%2C,illustrate%20when%20to%20use%20each)) 
---

# 5. Advanced React Components

Beyond the basics of components and props, React provides advanced capabilities and patterns for building more complex components. In this chapter, we’ll explore some advanced component concepts: **Fragments**, **Portals**, and other patterns that can help structure large applications. We’ll also mention controlled vs uncontrolled components (commonly encountered when dealing with forms, though forms are covered in depth later).

### Fragments: Grouping Child Elements

Normally, a React component’s render method (or function component) must return a single parent element. But what if you need to return multiple sibling elements without an extra wrapper node (like an unnecessary `<div>`)? **Fragments** let you group a list of children without adding an extra DOM node ([Fragments – React](https://legacy.reactjs.org/docs/fragments.html#:~:text=A%20common%20pattern%20in%20React,extra%20nodes%20to%20the%20DOM))  A fragment is basically an “invisible” container.

You can use fragments in two ways:

- **Explicit `<React.Fragment>` tags:**  
  ```jsx
  return (
    <React.Fragment>
      <ChildA />
      <ChildB />
      <ChildC />
    </React.Fragment>
  );
  ```  
  This will render ChildA, ChildB, ChildC as siblings in the DOM with no wrapper `<div>` around them.

- **Shorthand syntax:** `<>...</>` which is syntactic sugar for React.Fragment. Example:  
  ```jsx
  return (
    <>
      <li>Item 1</li>
      <li>Item 2</li>
    </>
  );
  ```  
  This is especially handy in list components – you can return an array of `<li>` elements without an extra enclosing element. Just note that the shorthand `<>` cannot take any attributes or keys. If you need to assign a key to a Fragment (when mapping a list of fragments), use the long form `<React.Fragment key={...}>`.

**When to use Fragments:** Anytime you would otherwise have to return multiple elements and don’t want to clutter the DOM. A common case is a table row component that needs to return multiple `<td>` cells – those `<td>`s must be wrapped in a single `<tr>` or fragment. Using a `<div>` would break the table structure, but a fragment works perfectly. Fragments help keep the DOM clean and avoid unnecessary wrappers.

### Portals: Rendering Outside the Parent DOM Hierarchy

React normally renders components within the DOM tree of their parent. **Portals** provide a way to render a component’s children into a different place in the DOM, outside of its regular parent hierarchy ([Portals – React](https://legacy.reactjs.org/docs/portals.html#:~:text=Portals%20provide%20a%20first,hierarchy%20of%20the%20parent%20component))  This is useful for cases like modals, tooltips, or dropdown menus that need to visually “break out” of overflow or z-index boundaries.

To create a portal, React provides `ReactDOM.createPortal(child, container)`. The first argument is any renderable React element (often a component or JSX tree), and the second is a DOM node to render into (e.g., a DOM element that exists outside your root div, such as a sibling div with id `modal-root`). For example:

```jsx
// In your HTML:
// <div id="app-root"></div>
// <div id="modal-root"></div>

// In React:
return ReactDOM.createPortal(
  <div className="modal">{props.children}</div>,
  document.getElementById('modal-root')
);
```

This would render the modal’s JSX into the DOM node with `id="modal-root"`, regardless of where this component is in the React component tree. **Portals** allow you to maintain the same React tree (context, event bubbling, etc., still work as if the component were inline) while actually mounting the node elsewhere in the DOM ([Portals – React](https://legacy.reactjs.org/docs/portals.html#:~:text=Even%20though%20a%20portal%20can,position%20in%20the%20DOM%20tree))  ([Portals – React](https://legacy.reactjs.org/docs/portals.html#:~:text=%3Cbody%3E%20%3Cdiv%20id%3D%22app,html)) 

**Typical use cases for portals:** Modals and dialogs (so they aren’t constrained by parent styles like overflow hidden), dropdown menus that might escape a bounding container, tooltips that need to overlay other content. Essentially, any time you need a component to render at the *body* level (or another external node) for styling or positioning reasons.

React Portals still let events bubble up through the React tree as usual. That means a click inside a portal can still be caught by an onClick on an ancestor component *in React’s hierarchy*, even though in the DOM it’s separate ([Portals – React](https://legacy.reactjs.org/docs/portals.html#:~:text=Even%20though%20a%20portal%20can,position%20in%20the%20DOM%20tree))  This is a nice feature – you don't lose interactivity or context by using portals.

To implement a portal, you often create a separate component (e.g., `<Modal>` component) that uses `createPortal` in its render. The rest of your app can simply render `<Modal>...</Modal>` and the internals of Modal take care of portal logic.

### Controlled vs Uncontrolled Components (Brief)

When dealing with form inputs (text fields, checkboxes, etc.), there are two approaches:

- **Controlled Components:** The form input’s value is controlled by React state. You supply the value via a prop and handle changes with an onChange handler that updates state. The React state is the “single source of truth” for the input value ([Forms – React](https://legacy.reactjs.org/docs/forms.html#:~:text=We%20can%20combine%20the%20two,is%20called%20a%20%E2%80%9Ccontrolled%20component%E2%80%9D))  For example, `<input type="text" value={text} onChange={e => setText(e.target.value)} />`. This way, every time the input changes, you update state, and the input always reflects the state. Controlled components give you instant access to user input in React and make things like validation easier, but require writing those onChange handlers.
- **Uncontrolled Components:** The form input maintains its own internal state (like normal HTML). You use a ref to get the value when needed instead of on each keystroke. For example, `<input type="text" ref={inputRef} />` and later `inputRef.current.value` to get the current value ([Uncontrolled Components – React](https://legacy.reactjs.org/docs/uncontrolled-components.html#:~:text=In%20most%20cases%2C%20we%20recommend,handled%20by%20the%20DOM%20itself))  ([Uncontrolled Components – React](https://legacy.reactjs.org/docs/uncontrolled-components.html#:~:text=To%20write%20an%20uncontrolled%20component%2C,form%20values%20from%20the%20DOM))  This is more similar to traditional HTML form usage (or using document.getElementById in vanilla JS). Uncontrolled components can be simpler for basic use cases or integrating with non-React code, but you have less immediate control over the form data.

In most cases, **React recommends controlled components** for forms ([Uncontrolled Components – React](https://legacy.reactjs.org/docs/uncontrolled-components.html#:~:text=In%20most%20cases%2C%20we%20recommend,handled%20by%20the%20DOM%20itself)) because they integrate better with React’s way of doing things (state drives UI). You can also mix approaches – for example, use uncontrolled inputs but still use React state for certain parts – but that can lead to complexity or warnings (like switching from uncontrolled to controlled mid-lifecycle, which React will warn about). If you do start with an uncontrolled input but later give it a `value` prop, you might encounter a warning about a component changing from uncontrolled to controlled.

We’ll cover forms in more depth in a later chapter, but remember: controlled inputs give you more power (at the cost of more code), uncontrolled can be quicker but are less flexible. You can choose per use case.

### Other Advanced Patterns

Some other advanced component patterns and features in React include:

- **Higher-Order Components (HOC):** (Discussed in chapter 9) – functions that take a component and return a new component with added behavior.
- **Render Props:** A component that takes a function as a prop and uses it to determine what to render. This pattern has become less common with Hooks available, but you may see it in older libraries.
- **Context:** (Discussed in chapter 9) – provides a way to pass data through the component tree without prop-drilling.
- **Error Boundaries:** (Covered in chapter 16) – special components to catch JavaScript errors in the UI.
- **Refs & Forwarding Refs:** (Covered in chapter 18) – allow direct access to DOM elements or child component instances for imperative actions.

By leveraging fragments and portals, you can manage layout and overlay concerns cleanly. Controlled vs uncontrolled inputs give you flexibility in handling form elements. And patterns like context or HOCs allow sharing logic or data in sophisticated ways. Mastering these advanced techniques will enable you to build robust, scalable React components that handle a variety of real-world requirements.

**Sources:** React Fragments ([Fragments – React](https://legacy.reactjs.org/docs/fragments.html#:~:text=A%20common%20pattern%20in%20React,extra%20nodes%20to%20the%20DOM))  React Portals ([Portals – React](https://legacy.reactjs.org/docs/portals.html#:~:text=Portals%20provide%20a%20first,hierarchy%20of%20the%20parent%20component))  ([Portals – React](https://legacy.reactjs.org/docs/portals.html#:~:text=A%20typical%20use%20case%20for,example%2C%20dialogs%2C%20hovercards%2C%20and%20tooltips)) 
---

# 6. Styling in React

Styling is an important aspect of building React applications. React doesn’t enforce a single way to style components – instead, you have a variety of options, from traditional CSS files to modern CSS-in-JS solutions. In this chapter, we’ll cover different styling techniques: **CSS stylesheets, CSS Modules, inline styles, and styled-components**, as well as tips for using each effectively.

### Traditional CSS and className

The simplest way to style React components is much like plain HTML/CSS:

- Write CSS in a stylesheet (e.g., `App.css`).
- Import that stylesheet in your component file (if using Create React App or a similar setup, you can do `import './App.css';` at the top of your component file).
- Use the `className` prop on JSX elements to apply CSS classes (note: in JSX it’s `className` instead of `class` attribute) ([DOM Elements – React](https://legacy.reactjs.org/docs/dom-elements.html#:~:text=className)) 

Example:  
```css
/* App.css */
.title {
  color: blue;
  text-align: center;
}
```
```jsx
// App.js
import './App.css';
function App() {
  return <h1 className="title">Hello World</h1>;
}
```  
This will render an `<h1>` with the class "title", styled according to your CSS. This approach keeps styling separate in CSS files and works well, especially for global styles or themes.

One challenge in large apps is **class name collisions** – if you use generic class names, styles might accidentally overlap. That’s where CSS Modules can help.

### CSS Modules: Scoped CSS

**CSS Modules** allow you to write CSS that is scoped to a specific component. You create CSS files with a `.module.css` extension and import them as an object in your component. The class names in the CSS file will be transformed into unique identifiers.

For example, `Button.module.css`:
```css
.primaryButton {
  background-color: green;
  color: white;
}
```
In your `Button.jsx` component:
```jsx
import styles from './Button.module.css';
function Button(props) {
  return <button className={styles.primaryButton}>{props.label}</button>;
}
```
Here, `styles.primaryButton` might be transformed to something like `"Button_primaryButton__abc123"` behind the scenes. The result is that the `.primaryButton` styles apply only to this component’s elements, and you won’t accidentally clobber or be clobbered by other `.primaryButton` styles elsewhere. In short, **CSS Modules generate unique class names**, ensuring local scope ([Styling in React: 6 ways to style React apps - LogRocket Blog](https://blog.logrocket.com/styling-react-6-ways-style-react-apps/#:~:text=Styling%20React%20components%20with%20CSS,Modules))  This solves the cascade/global scope issues of CSS by default and makes styling more modular.

Most build setups (Create React App, etc.) support CSS Modules out of the box for filenames ending in `.module.css`.

**Pros:** Encapsulation of styles, no naming conflicts, still writes CSS normally.  
**Cons:** Slightly more setup (need to import styles object), and if you need to define global styles (like a body background), you’d use a normal CSS file or other method for that.

### Inline Styles and the style Prop

React supports styling elements via the `style` prop, which accepts a JavaScript object of CSS properties. This is similar to the old `element.style` in DOM, but in React you pass an object:

```jsx
<div style={{ color: 'red', backgroundColor: 'black' }}>Hello</div>
```

A few things to note for inline styles in React:
- CSS property names are **camelCased** (backgroundColor, fontWeight, marginTop, etc.) instead of kebab-case, because the style prop is a JS object ([javascript - Adding style attribute in react - Stack Overflow](https://stackoverflow.com/questions/56632250/adding-style-attribute-in-react#:~:text=It%27s%20not%20%60font,need%20to%20use%20camelCase%20notation))  ([javascript - Adding style attribute in react - Stack Overflow](https://stackoverflow.com/questions/56632250/adding-style-attribute-in-react#:~:text=,rather%20than%20a%20CSS%20string)) 
- Values are usually strings (e.g., `'10px'`, `'bold'`) or numbers (which are assumed to be px if it’s a unit property). For example, `{ width: 100 }` is treated as 100px. If you need a percentage or other unit, use a string like `'50%'`.
- Certain properties like `--custom-variable` (CSS custom properties) won’t work via the style object because of the syntax; you might use className and external CSS for those.

**When to use inline styles:** For dynamic styling that is computed in JavaScript, or for applying styles conditionally without having to create lots of CSS classes. It’s also convenient for quick prototyping. However, inline styles do not support pseudo-classes like `:hover` or media queries, and excessive use can make your components hard to maintain (mixing too much style logic in with render logic).

Keep in mind that inline styles are not automatically vendor-prefixed. Most common properties are fine in modern browsers, but if you need prefixes, consider using a library or sticking to CSS files where your build can handle prefixes.

**Example:**  
```jsx
<button style={{ opacity: props.disabled ? 0.5 : 1 }}>
  {props.label}
</button>
```  
This will render the button with 50% opacity if disabled, otherwise fully opaque, without needing separate CSS classes for disabled state.

One more thing: *“The style attribute accepts a JavaScript object with camelCased properties rather than a CSS string.”* ([javascript - Adding style attribute in react - Stack Overflow](https://stackoverflow.com/questions/56632250/adding-style-attribute-in-react#:~:text=,rather%20than%20a%20CSS%20string)) – This means `<div style="text-align: center">` (string) won’t work, you must do `<div style={{ textAlign: 'center' }}>`. If you find yourself constructing style objects heavily, you might consider CSS-in-JS libraries for more features.

### CSS-in-JS with Styled Components

A popular approach in React is using **CSS-in-JS** libraries, which allow you to write CSS styles inside your JavaScript, often scoped to components. One of the most popular is **Styled-Components**.

Styled-Components lets you define a styled component by using ES6 template literals. For example:
```jsx
import styled from 'styled-components';

const FancyButton = styled.button`
  background: ${props => props.primary ? "palevioletred" : "white"};
  color: ${props => props.primary ? "white" : "palevioletred"};
  font-size: 1em;
  margin: 0.5em;
  padding: 0.5em 1em;
  border: 2px solid palevioletred;
  border-radius: 3px;
`;
```
Now `FancyButton` is a React component you can use: `<FancyButton primary>Click me</FancyButton>`. Styled-Components generates unique class names for these styles and injects them into the DOM. It allows you to write actual CSS (including pseudo-selectors, media queries, nesting, etc.) within your JS, and even to interpolate props into the styles (as seen with `props.primary` above).

With styled-components, you are “creating a normal React component with styles attached to it” ([Styling in React: 6 ways to style React apps - LogRocket Blog](https://blog.logrocket.com/styling-react-6-ways-style-react-apps/#:~:text=With%20styled,CSS%20%E2%80%94%20like%20media%20queries))  This removes the mapping between styles and components – you define a styled component and use it directly, rather than applying classes manually. It can make components very self-contained. It also encourages the DRY principle by letting you create small, styled components that you reuse (like a <Button> that can have variants via props).

**Pros:** Fully dynamic styling with access to React props, no class name collisions, co-locate styles with components, can remove a lot of separate CSS files.  
**Cons:** Adds a runtime overhead (though minor in most cases), and styles are generated via JavaScript which can affect performance slightly if overused. Also, learning the tagged template literal syntax is an extra step.

Another popular CSS-in-JS library is **Emotion**, which is similar to styled-components and even supports a similar API. React also has other libraries like JSS, or even frameworks like Material-UI that have their own styling solution.

### Other Styling Options

- **Sass or Less:** You can use Sass (SCSS) with React by configuring your build or using CRA’s support (CRA supports Sass out of the box if you install sass). Sass allows nesting, variables, and mixins which can make writing CSS more powerful.
- **Utility CSS frameworks:** e.g., Tailwind CSS – instead of writing custom CSS, you apply utility classes (like `bg-blue-500 text-center p-4`) directly on elements. Tailwind can be integrated with React (it’s just CSS classes) and can speed up styling if you prefer that approach.
- **UI Component Libraries:** (like Material-UI, Bootstrap, Chakra UI, etc.) They come with their own styles/components. Using them often means you use their components or classes to achieve a certain design, rather than writing a lot of CSS yourself.

### Best Practices and Pitfalls

- **Avoid Global Scope Pollution:** If using plain CSS, be mindful of selectors that could match unintended elements. Consider naming conventions (BEM, etc.) or CSS Modules to scope styles.
- **Choosing an Approach:** Use what makes sense for the project. For a small app or one with a strict design system, a single CSS file or CSS Modules might suffice. For large apps where components are distributed or theming is complex, CSS-in-JS might offer more flexibility.
- **Performance:** Too many style recalculations (e.g., dynamically changing inline styles every render) can cause layout thrashing. Use them wisely and measure if needed. Also, styled-components dynamically inject CSS; this is fine for most cases but extremely frequent remounting of styled components could add overhead.
- **Theming:** Libraries like styled-components and Emotion support theming (via Context) out of the box. If you need a light/dark theme, they can be quite handy. Alternatively, CSS variables with plain CSS can implement theming as well.

**In summary**, React gives you the freedom to style how you prefer: whether it’s traditional CSS (with classes and maybe CSS Modules for safety) or CSS-in-JS for a component-oriented approach. Many teams adopt a combination: basic layout via global CSS or a framework, and fine-tuned component styles via CSS Modules or styled-components. What’s important is consistency and maintainability – choose a strategy that your team is comfortable with and stick to it.

**Sources:** React inline style usage ([javascript - Adding style attribute in react - Stack Overflow](https://stackoverflow.com/questions/56632250/adding-style-attribute-in-react#:~:text=,rather%20than%20a%20CSS%20string))  CSS Modules overview ([Styling in React: 6 ways to style React apps - LogRocket Blog](https://blog.logrocket.com/styling-react-6-ways-style-react-apps/#:~:text=Styling%20React%20components%20with%20CSS,Modules))  styled-components introduction ([Styling in React: 6 ways to style React apps - LogRocket Blog](https://blog.logrocket.com/styling-react-6-ways-style-react-apps/#:~:text=Styling%20with%20styled)) 
---

# 7. Debugging and Error Handling

No matter how skilled you are, you’ll encounter bugs and errors in development. Being able to debug effectively and handle errors gracefully is crucial. In this chapter, we’ll discuss techniques for debugging React applications and strategies for error handling in the UI.

### Using React Developer Tools

The **React Developer Tools** browser extension is an essential debugging aid. It lets you inspect the React component tree, props, and state in your application. Once installed (available for Chrome, Firefox, etc.), you get a new “⚛️ Components” tab in your devtools. Here’s how it helps:

- **Component Hierarchy:** You can browse your app’s component tree, similar to how you would the DOM, but in terms of React components. Selecting a component shows its props and state on the right panel ([The 2023 guide to React debugging · Raygun Blog](https://raygun.com/blog/react-debugging-guide/#:~:text=React%20Developer%20Tools%20adds%20two,tabs%20to%20your%20Chrome%20DevTools)) 
- **Props/State Inspection:** You can see current prop values and state values of any selected component in real time. This is extremely useful to verify that state is updating as expected or props are being passed correctly.
- **Editing props/state:** In development, React DevTools even allows you to tweak props or state on the fly to test UI changes.
- **Profiler:** As mentioned in the performance chapter, React DevTools also has a **Profiler** tab where you can record interactions and see what components rendered and for how long.

It’s important to note that React Developer Tools is **not a replacement for** standard Chrome DevTools, but complementary ([The 2023 guide to React debugging · Raygun Blog](https://raygun.com/blog/react-debugging-guide/#:~:text=Note%20that%20React%20Developer%20Tools,the%20individual%20HTML%2C%20CSS%2C%20and))  The regular Elements tab shows you DOM nodes and styles, whereas React DevTools shows the React components and their data. Use them together: for example, if a component isn’t updating, check in React DevTools if its props/state changed; if a UI style looks off, inspect the DOM and CSS in Elements.

Also, remember to have the extension enabled and note that it doesn’t run in incognito mode by default (you can allow it in extension settings) ([The 2023 guide to React debugging · Raygun Blog](https://raygun.com/blog/react-debugging-guide/#:~:text=match%20at%20L338%20Since%20React,and%20profile%20the%20performance%20issues)) 

### Logging and Breakpoints

Sometimes the old-fashioned approach works: inserting `console.log` statements in your code to trace values. For instance, logging in a component’s render or useEffect to see if it’s running when you expect. Make sure to remove or disable verbose logging in production or it could clutter the console and potentially expose internals.

Using the browser’s debugger is even more powerful:
- In Chrome/Firefox, you can put a `debugger;` statement in your code or set breakpoints in the Sources panel. This lets you pause execution at certain lines (for example, inside an event handler or useEffect) and inspect variables in that context.
- You can also step through code to see how state updates propagate.

When debugging React, remember that the code you wrote (JSX, etc.) is transformed. In development mode, source maps usually let you breakpoint in your original source files. Use those source-mapped files for a friendlier debugging experience.

### Common Issues and How to Investigate

**1. Nothing is Rendering / Blank Screen:**  
If your React app loads but you see a blank page or missing component:
   - Check the browser console for errors. A runtime JS error (like trying to access undefined) can break the rendering. The console will usually show an error and stack trace.
   - Use React DevTools: do you see your components in the tree? If not, maybe React wasn’t initialized (check `ReactDOM.render` or root creation).
   - Ensure you don’t have a mismatched HTML structure (like returning an array of elements without a Fragment).
   - Look for typos in component import/export. A blank screen could mean a component didn’t render due to a bad import path (the console may have a module not found error in that case).

**2. Component Not Updating:**  
If you expect a component to re-render on some state/prop change but it isn’t:
   - Verify the state is actually changing. `console.log` the state value before and after the supposed update. Remember that state updates are async; logging immediately after a `setState` might show the old value.
   - Check if you accidentally mutated state directly instead of using the updater, which might not trigger re-render.
   - Ensure parent component is passing new props. In React DevTools, watch the prop as the app runs through the interaction.
   - If using `React.memo` or PureComponent, maybe the component is skipping renders incorrectly (e.g., props changes not detected due to shallow compare). In that case, confirm that you’re not mutating objects in props.

**3. “Each child in a list should have a unique key” Warning:**  
This is a common warning when rendering lists. React is telling you that when you do `{items.map(item => <ItemComponent {...} />)}`, you need to give each element a `key` prop. The solution: provide a stable unique key (often `item.id`). This warning is important – not providing keys can lead to inefficient or incorrect re-renders when list items change order. Make sure keys are unique and stable. (Avoid using array index as key except for static lists, because if items reorder or are inserted, it can cause issues).

**4. “Cannot update a component while rendering another component” Warning:**  
This usually means you are calling a state update (or dispatch) in a component’s render function, or in the wrong place in the lifecycle. For example, modifying state during rendering is not allowed. The fix is to move that state update into a useEffect or an event handler, depending on what you intended.

**5. Network errors / data not showing:**  
If your component is supposed to show data from an API but nothing appears:
   - Open the Network tab in DevTools, see if the request was made, and if it succeeded. If not, check the endpoint and any error response.
   - If the data is in the response but not in your UI, check your state update logic after the fetch (are you updating state with the fetched data?).
   - Also verify that the component that fetches data is actually mounted (maybe the route isn’t matching, etc.).

**6. Styling issues:**  
If a component looks wrong:
   - Use Elements tab to inspect the CSS and see if a class is missing or overridden.
   - Remember that in React, `className` must be used; if you accidentally wrote `class=` in JSX, it will be ignored (no error, just no style). Likewise, `onclick` instead of `onClick` or other attribute case issues can cause things not to work.
   - If using CSS Modules, ensure you imported the module and applied the class from the object (and that the CSS file name is correctly ending in `.module.css`).

### Handling Errors Gracefully

Bugs aside, sometimes errors happen due to factors beyond your code’s control (like a network failure, or an exception thrown in a deeply nested component). React’s concept of **Error Boundaries** (covered in Chapter 16) allows you to catch exceptions in the rendering phase and display a fallback UI instead of breaking the whole app. For example, you might wrap your app or specific parts in an error boundary component that catches errors and shows a message like “Something went wrong.”

Error boundaries catch **rendering errors** in child components. They do not catch errors in event handlers (you should handle those in try/catch or logic in the handler itself). They also don’t catch errors in async code (like setTimeout callbacks or event callbacks – again handle those manually). But for rendering errors (like a component throwing in its render because of an undefined prop, etc.), they prevent the entire React component tree from unmounting due to an uncaught exception. Instead, just that sub-tree is replaced with a fallback UI. This leads to a more resilient app.

Another aspect of error handling is dealing with promises or async operations in components. If a fetch fails, you should update state to reflect an error (e.g., set `error` state and show an error message UI). Always consider the loading and error states when fetching data or performing asynchronous tasks in React. It results in a better user experience than just nothing happening or the UI stuck.

### Monitoring and Logging

In production, you won’t have React DevTools or console logs. If your app is large, consider using error monitoring services (like Sentry, LogRocket, etc.) which can capture exceptions and user sessions. This can be invaluable for catching errors that slip through and understanding what users did to trigger them.

At minimum, you might implement a global error boundary at the app level that logs the error (using `console.error` or sending to a server) and shows a user-friendly message. For example, catching an error and showing “Oops, something went wrong. Please try again later.”

**Summary:** Use the right tools – React DevTools for component state/prop inspection ([The 2023 guide to React debugging · Raygun Blog](https://raygun.com/blog/react-debugging-guide/#:~:text=2))  browser devtools for network and DOM. Leverage console and breakpoints to trace logic. Fix the common issues by reading warnings (React’s warnings are there to help!). And implement error boundaries or try/catch around sensitive code to handle errors gracefully. Debugging is an iterative process: make a hypothesis, test it (by logging or breakpoints), and narrow down the cause. With practice, you’ll get faster at pinpointing issues in React apps.

**Sources:** React Developer Tools usage ([The 2023 guide to React debugging · Raygun Blog](https://raygun.com/blog/react-debugging-guide/#:~:text=2))  Error boundaries definition ([Error handling in React best practices - Stack Overflow](https://stackoverflow.com/questions/36897434/error-handling-in-react-best-practices#:~:text=Error%20boundaries%20are%20React%20components,and%20display%20a%20fallback%20UI)) 
---

# 8. Introduction to Hooks

Hooks are one of the biggest advancements in React, introduced in React 16.8. They allow function components to use state and other React features without writing a class. This chapter will introduce Hooks, covering the basics of **useState** and **useEffect**, and the rules you must follow when using Hooks.

### What are Hooks and Why Use Them?

**Hooks** are special functions that let you “hook into” React’s features. Prior to Hooks, if you needed state or lifecycle in a component, you had to use a class component. Hooks enabled those capabilities in functional components, leading to simpler code and reusability of stateful logic.

> “Hooks are a new addition in React 16.8. They let you use state and other React features without writing a class.” ([Introducing Hooks – React](https://legacy.reactjs.org/docs/hooks-intro.html#:~:text=Hooks%20are%20a%20new%20addition,features%20without%20writing%20a%20class)) 
Hooks solve some problems that were hard with classes:
- Reusing logic was cumbersome (HOCs or render props were used; Hooks make it easier to share logic by simple functions).
- Classes can be verbose and confuse `this` binding and lifecycle methods. Hooks provide a more direct way to manage component state and side effects.
- They allow splitting one component’s logic into smaller functions (e.g., separating an effect for subscription from one for form handling) rather than forcing all in lifecycle methods.

**Important:** Hooks do **not** replace your knowledge of React concepts (state, props, context, refs, lifecycle), but provide a more direct API to use them ([Introducing Hooks – React](https://legacy.reactjs.org/docs/hooks-intro.html#:~:text=Hooks%20don%E2%80%99t%20replace%20your%20knowledge,powerful%20way%20to%20combine%20them))  You can gradually adopt Hooks in parts of your app—no need to rewrite everything at once (they’re 100% opt-in and backward-compatible).

### useState: Adding State to Function Components

The `useState` Hook lets you add state to a function component. It returns an array of two values: the current state and a function to update it.

**Basic usage:**  
```js
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);  // initialize state to 0

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

Here:
- We call `useState(0)` to declare a state variable `count`, initialized to 0. React preserves this state between re-renders of the component.
- We get back `count` (current value) and `setCount` (a function to update it). We can call `setCount(newValue)` to schedule a state update.
- When the button is clicked, we call `setCount(count + 1)`. React knows this component’s state changed, so it re-renders `Counter` with the new count.
- The UI updates to show the new count.

Each call to `useState` gives you a separate piece of state. You can use multiple useState calls in one component to manage different state variables (e.g., `const [name, setName] = useState('');` for an input field, etc.).

**Rules for Hooks:** There are two main rules you **must** follow when using Hooks ([Rules of Hooks – React](https://legacy.reactjs.org/docs/hooks-rules.html#:~:text=Hooks%20are%20JavaScript%20functions%2C%20but,to%20enforce%20these%20rules%20automatically))  ([Rules of Hooks – React](https://legacy.reactjs.org/docs/hooks-rules.html#:~:text=Only%20Call%20Hooks%20from%20React,Functions)) 
1. **Only call Hooks at the top level.** Don’t call Hooks inside loops, conditions, or nested functions. Always use them at the top level of your React function so that Hooks are called in the same order each render. This rule ensures React can associate the Hook state with the correct component and in the correct order.
2. **Only call Hooks from React function components (or custom Hooks).** Don’t call Hooks from regular JS functions. Hooks are meant to be used in React components (or other Hooks). This means you can use Hooks in functional components or make your own “custom Hook” (which is simply a function that itself calls Hooks). You **can’t** use Hooks in class components, nor can you call them in non-React JS logic.

React’s linter plugin can help enforce these rules to avoid mistakes ([Rules of Hooks – React](https://legacy.reactjs.org/docs/hooks-rules.html#:~:text=Hooks%20are%20JavaScript%20functions%2C%20but,to%20enforce%20these%20rules%20automatically))  If you break them, you might see errors or inconsistent behavior.

### useEffect: Side Effects in Function Components

The `useEffect` Hook lets you perform side effects in function components – things like data fetching, subscriptions, or manually changing the DOM – which were typically done in lifecycle methods (`componentDidMount`, `componentDidUpdate`, `componentWillUnmount`) in classes. `useEffect` unifies those: by default, it runs after every render (like componentDidUpdate), but you can control it to mimic other lifecycle phases.

**Basic usage:**  
```jsx
import React, { useState, useEffect } from 'react';

function DocumentTitleChanger(props) {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `Clicked ${count} times`;
  });
  
  // ...
}
```
This effect sets the page title every time the component renders (after render). By default, useEffect runs after the first render and after every update. You can think of it as a combination of componentDidMount and componentDidUpdate (and it can also cover componentWillUnmount as we’ll see).

**Controlling when useEffect runs:** Often, you don’t want an effect to run on every update. You can provide a dependency array as the second argument to `useEffect(effect, [dep1, dep2, ...])`. The effect will only re-run if one of the dependencies has changed between renders. If you pass an empty array `[]`, the effect runs only once after the first render (and cleanup on unmount), mimicking componentDidMount ([AJAX and APIs – React](https://legacy.reactjs.org/docs/faq-ajax.html#:~:text=%2F%2F%20Note%3A%20the%20empty%20deps,.then%28res%20%3D%3E%20res.json))  For example:
```jsx
useEffect(() => {
  // fetch data when component mounts
  fetchData();
}, []); // empty array means run once
```
If you return a function from the effect, that function is treated as a cleanup (like componentWillUnmount) for things like unsubscribing or clearing timers:
```jsx
useEffect(() => {
  const subscription = API.subscribe(data => setData(data));
  return () => {
    // cleanup on unmount
    subscription.unsubscribe();
  };
}, []);
```

**Important:** *“The useEffect Hook allows you to perform side effects in your components. Some examples of side effects are: fetching data, directly updating the DOM, timers.”* ([Anshtripathi079/react_hooks - GitHub](https://github.com/Anshtripathi079/react_hooks#:~:text=The%20useEffect%20Hook%20allows%20you,directly%20updating%20the%20DOM%2C))  It’s crucial to call `useEffect` for any logic that **needs to happen as a result of rendering** or on certain state/prop changes, especially if it involves I/O or global state. This keeps your component’s main body pure and focused on returning JSX.

Think of useEffect’s dependencies as telling React when it needs to re-run the effect. If you use state values or props inside the effect, you should list them as dependencies, otherwise stale values might be used (React’s ESLint plugin will warn you about missing dependencies). There’s a nuance: sometimes you might intentionally omit a dependency (or use an empty array) to avoid continuous re-fetching, but then you have to ensure the effect logic doesn’t need the up-to-date value or you handle it accordingly.

### Other Basic Hooks

- **useContext:** Allows you to access a React context value directly in a component without needing a `<Context.Consumer>`. This simplifies consuming context (like theme or user data provided via Context API).
- **useReducer:** A more advanced hook for managing state with a reducer function (similar to Redux style state management), useful when you have complex state logic or multiple sub-values.
- **useRef:** Lets you have a mutable value that persists across renders (often used to reference DOM elements or store previous values).
- **useLayoutEffect:** Like useEffect but runs earlier (after DOM mutations but before painting). Rarely needed unless you need to measure DOM layout.

We’ll cover some of these in later chapters, but know that useState and useEffect are the two most commonly used Hooks.

### Custom Hooks

One of the powerful aspects of Hooks is the ability to create **custom Hooks** – essentially functions that call Hooks to encapsulate some reusable logic. A custom Hook is just a JavaScript function whose name starts with “use” (by convention) and that may call other hooks. For example, you could create `useWindowWidth` that subscribes to window resize events and provides the current width, and use that in multiple components. By extracting that logic into a custom Hook, you avoid duplicating code and make your components cleaner. Custom Hooks allow sharing logic *without* the wrapper hell of HOCs or render props.

### Hooks Caveats and Best Practices

- Always abide by the Hook rules mentioned. Violating them can lead to bugs that are hard to debug.
- Hooks can call other Hooks (e.g., a custom Hook using useState and useEffect). As long as the rules are followed at the top level of *those Hooks*, it works.
- Manage dependencies carefully in useEffect to avoid infinite loops (if you update state inside an effect that is also a dependency of that effect, you can create a loop).
- Hooks don’t magically do everything for you – they just provide the primitives. You still design how state flows in your app, when to break into smaller components, how to handle data fetching, etc. But they often simplify the implementation.

To wrap up: Hooks have become the standard for writing new React components because they make code more concise and logical. Class components are still supported, but you’ll find Hooks lead to fewer lines of code and easier sharing of functionality. Now that we have Hooks, we can revisit many patterns (state management, context, etc.) with a fresh approach.

**Sources:** React Hooks intro ([Introducing Hooks – React](https://legacy.reactjs.org/docs/hooks-intro.html#:~:text=Hooks%20are%20a%20new%20addition,features%20without%20writing%20a%20class))  useEffect for side effects ([Anshtripathi079/react_hooks - GitHub](https://github.com/Anshtripathi079/react_hooks#:~:text=The%20useEffect%20Hook%20allows%20you,directly%20updating%20the%20DOM%2C))  Rules of Hooks ([Rules of Hooks – React](https://legacy.reactjs.org/docs/hooks-rules.html#:~:text=Only%20Call%20Hooks%20at%20the,Top%20Level))  ([Rules of Hooks – React](https://legacy.reactjs.org/docs/hooks-rules.html#:~:text=Only%20Call%20Hooks%20from%20React,Functions)) 
---

# 9. Higher Order Components and Context API

As applications grow, patterns for sharing code and passing data through the component tree become important. Two concepts that address these in React are **Higher-Order Components (HOCs)** and the **Context API**. In this chapter, we’ll explain HOCs as a pattern for reusing component logic, and how Context provides a way to pass data deeply without prop drilling.

### Higher-Order Components (HOCs)

A **Higher-Order Component** is an advanced React pattern for reusing component logic. Conceptually, an HOC is **a function that takes a component and returns a new component** ([Higher-Order Components – React](https://legacy.reactjs.org/docs/higher-order-components.html#:~:text=Concretely%2C%20a%20higher,and%20returns%20a%20new%20component))  The returned component typically wraps the original component and adds some extra props or functionality to it.

It’s similar to how higher-order functions work (functions taking/returning functions). For components, you might have an HOC that provides a certain prop or handles a concern like logging, error handling, data fetching, etc., so that multiple components can be “enhanced” with that logic without repeating it.

**Example scenario:** Suppose you have several components that need to know if the user is authenticated and if not, redirect to login. You could write an HOC `withAuthProtection` that wraps a component and handles that logic:

```jsx
function withAuthProtection(WrappedComponent) {
  return function ProtectedComponent(props) {
    if (!isAuthenticated()) {
      return <Redirect to="/login" />;
    }
    return <WrappedComponent {...props} />;
  };
}
```

Then use it: `export default withAuthProtection(DashboardPage);` Now `DashboardPage` will be protected by that auth check. The HOC returns a new component (`ProtectedComponent`) that renders either a redirect or the original component.

Another example: **react-redux** library’s `connect` function is a famous HOC. You do `connect(mapStateToProps, ...)(MyComponent)` and it returns a new component that is subscribed to the Redux store, passing state and dispatch as props to `MyComponent`. The HOC spares each component from writing subscription logic individually.

**Characteristics of HOCs:**
- They are not part of the React API per se, but a pattern emerging from compositional nature of React ([Higher-Order Components – React](https://legacy.reactjs.org/docs/higher-order-components.html#:~:text=A%20higher,emerges%20from%20React%E2%80%99s%20compositional%20nature)) 
- A HOC should pass through props that it doesn’t specifically handle. Always spread `{...props}` to the wrapped component so that it receives the props it expects.
- HOCs often add props. For example, an HOC might inject a `currentUser` prop after fetching user data, so the wrapped component can use it.
- You can stack multiple HOCs. e.g., `withRouter(withAuthProtection(MyComponent))` – though excessive HOC wrapping can become hard to follow (the “wrapper hell”).

**Use Cases for HOCs:** Reusing cross-cutting concerns (logging, error boundaries, theming), injecting global data (like from context or Redux), or abstracting boilerplate (like form handling logic that many form components share). Before Hooks, HOCs and Render Props were primary ways to reuse logic. Hooks have made some HOC use cases simpler (you can use a custom Hook instead of an HOC in many cases now).

One thing to be cautious about: HOCs create new components, which can interfere with refs or static methods on the wrapped components. React now provides tools like `React.forwardRef` to assist passing refs through HOCs. But in general, be aware that debugging stack traces might show the HOC wrapper names, etc. It’s often helpful to set a displayName for your HOC for easier debugging.

**Summing up HOCs:** It’s “a component transforms another component.” Think of it as: `EnhancedComponent = higherOrderComponent(WrappedComponent) ([Higher-Order Components – React](https://legacy.reactjs.org/docs/higher-order-components.html#:~:text=Concretely%2C%20a%20higher,and%20returns%20a%20new%20component)) . The enhanced component can do something before rendering the wrapped one, or render something conditionally instead. It’s a powerful pattern for code reuse in React’s component model.

### Context API

The **Context API** in React provides a way to share values between components **without having to pass props through every level** of the tree ([Context – React](https://legacy.reactjs.org/docs/context.html#:~:text=Context%20provides%20a%20way%20to,down%20manually%20at%20every%20level))  Normally, data is passed parent -> child via props, which can become cumbersome if a deeply nested component needs data from far up (you’d have to pass it through many intermediate components that don’t actually use it, known as “prop drilling”).

With Context, you can create a context and provide a value at a high level, and any descendant component can consume that value directly.

**Creating Context:**  
```jsx
const ThemeContext = React.createContext('light');
```
This creates a context object with default value `'light'`.

**Providing Context:**  
```jsx
<ThemeContext.Provider value="dark">
  <App />
</ThemeContext.Provider>
```  
Usually, you place a Provider high in the app (e.g., around your `<App />` or specific subtree). All components under this provider can access the `value` provided (“dark” here) without explicit props. You can have multiple context providers for different concerns (e.g., ThemeContext, AuthContext, etc.).

**Consuming Context:** There are two ways:
- Older: `<ThemeContext.Consumer>{ value => /* render something using value */ }</ThemeContext.Consumer>` (render prop pattern).
- Modern (with Hooks): `const theme = useContext(ThemeContext);` inside a function component. This Hook gives you the nearest current context value.

For class components, there’s also `static contextType = ThemeContext` or `<MyComponent contextType={ThemeContext}>`, but with Hooks available, useContext is simplest for function components.

**Example:** If you have a ThemeContext, a deeply nested component can do:
```jsx
function Button() {
  const theme = useContext(ThemeContext);
  return <button className={`button-${theme}`}>Click me</button>;
}
```
If a parent provider gives value `"dark"`, this will render with class "button-dark". If no provider is up the tree, it uses the default `'light'`.

**When to use Context:** When many components need to access the same “global” data. Common examples: current authenticated user, theme (light/dark mode), language locale, or a router object. Context is great for these because you avoid threading the data through every component in between. The official docs: *“Context provides a way to pass data through the component tree without having to pass props down manually at every level.”* ([Context – React](https://legacy.reactjs.org/docs/context.html#:~:text=Context%20provides%20a%20way%20to,down%20manually%20at%20every%20level)) 
**Drawbacks of Context:** If misused for every little thing, you can make components less reusable. Context ties components to a specific shared environment. Also, context updates will re-render all consuming components, so don’t put extremely frequently changing data in context (like a rapidly updating value) without consideration; it could harm performance. For most apps, context use is fine (e.g., theme doesn’t change often, user info changes on login/logout only, etc.). 

**Context vs Props:** Context doesn’t replace props. Use props for individual component configuration and passing data that is specific. Use Context for global concerns or data that is truly shared by many.

**Combining with Hooks:** We often define custom Hooks to use context easily. For example:
```jsx
const AuthContext = React.createContext();
const useAuth = () => useContext(AuthContext);
```
Now any component can `const auth = useAuth();` to get auth info, making it very ergonomic.

Finally, context and HOCs can combine: e.g., `withTheme` HOC could internally use ThemeContext to inject a `theme` prop into a component. But with Hooks, that pattern is less needed—components can directly use context.

### HOCs vs Render Props vs Hooks

These were three patterns to share code. HOCs wrap components, Render Props pass a function to decide what to render, Hooks allow sharing logic by extracting it to custom Hooks. In modern React, Hooks is typically the first choice for new code, with context to avoid prop drilling. HOCs are still used especially in many libraries (you’ll see them in older code or certain patterns), and Context remains as the built-in way to share data easily.

**Summary:** Higher-Order Components are a pattern to add reusable behavior to components by wrapping them, used heavily in pre-Hook days (and still for some use cases). The Context API is a built-in mechanism to avoid prop drilling by **providing** values high up and **consuming** them deep down without intermediate propagation ([Context – React](https://legacy.reactjs.org/docs/context.html#:~:text=Context%20provides%20a%20way%20to,down%20manually%20at%20every%20level))  Together, these tools help manage complexity as apps grow: HOCs for logic reuse and Context for global data sharing.

**Sources:** HOC definition ([Higher-Order Components – React](https://legacy.reactjs.org/docs/higher-order-components.html#:~:text=Concretely%2C%20a%20higher,and%20returns%20a%20new%20component))  ([Higher-Order Components – React](https://legacy.reactjs.org/docs/higher-order-components.html#:~:text=HOCs%20are%20common%20in%20third,Redux%E2%80%99s%20connect%20and%20Relay%E2%80%99s%20createFragmentContainer))  Context purpose ([Context – React](https://legacy.reactjs.org/docs/context.html#:~:text=Context%20provides%20a%20way%20to,down%20manually%20at%20every%20level)) 
---

# 10. HTTP Requests and Forms in React

Most React apps involve interacting with APIs and handling user input through forms. In this chapter, we’ll cover how to perform HTTP requests (e.g., fetching data or sending data to a server) and how to manage forms in React, including basic form input handling and submission.

### Making HTTP Requests (AJAX) in React

React itself doesn’t have a built-in AJAX library – you can use any method (Fetch API, Axios, etc.) to fetch or send data. The key considerations are *when* and *where* to fetch data in a React component’s lifecycle.

**When to fetch data:** Usually you fetch data in a component when it mounts. For function components, that means inside a `useEffect` with an empty dependency array (so it runs once on mount). For class components, it’s done in `componentDidMount`. This ensures data is loaded after the initial render. Fetching in event handlers is also common (e.g., on form submit or on button click).

**Using useEffect for data fetch:**  
```jsx
function UsersList() {
  const [users, setUsers] = useState([]);
  useEffect(() => {
    fetch('/api/users')
      .then(res => res.json())
      .then(data => setUsers(data.users))
      .catch(err => console.error('Failed to fetch users', err));
  }, []); // empty deps: run once on mount

  // ...
}
```
This pattern is typical: initiate fetch, update state when data arrives, handle errors appropriately (maybe set an error state and show a message). React will re-render with the data once `setUsers` updates state.

**With async/await:** Alternatively, 
```jsx
useEffect(() => {
  async function fetchUsers() {
    try {
      const res = await fetch('/api/users');
      const data = await res.json();
      setUsers(data.users);
    } catch (err) {
      console.error(err);
    }
  }
  fetchUsers();
}, []);
```

**Axios example (in class component):**  
```jsx
componentDidMount() {
  axios.get('/api/users')
    .then(response => {
      this.setState({ users: response.data.users });
    })
    .catch(error => { /* handle error */ });
}
```  
The principle is the same. The official recommendation: *“You should populate data with AJAX calls in the componentDidMount lifecycle method.”* ([AJAX and APIs – React](https://legacy.reactjs.org/docs/faq-ajax.html#:~:text=Where%20in%20the%20component%20lifecycle,I%20make%20an%20AJAX%20call)) for class components, or the equivalent with Hooks (useEffect on mount). This ensures you have a chance to update state with fetched data after the component is rendered the first time ([AJAX and APIs – React](https://legacy.reactjs.org/docs/faq-ajax.html#:~:text=You%20should%20populate%20data%20with,when%20the%20data%20is%20retrieved)) 

**Why not fetch in constructor or render?** Fetching in render can cause infinite loops or repeated requests (render runs often). In constructor, it might be too early (especially in strict mode or if server-side rendering, you want it after first mount on client). The `componentDidMount/useEffect` approach is safe: it runs only on client-side after initial mount, where you can perform side effects like network requests.

**Updating based on new props:** If a component needs to refetch when a prop changes (say, a `<UserProfile userId={id}>` that should load new data when userId prop changes), you would include that prop in the useEffect dependency array or use `componentDidUpdate` in a class to trigger a fetch when the prop changes.

**Cleaning up:** If using fetch, often no cleanup is needed (except maybe aborting fetch if the component unmounts early to avoid setting state after unmount). With subscriptions (like WebSockets or others), useEffect cleanup function or componentWillUnmount should unsubscribe.

**Where to store data:** Usually in component state (with useState or this.setState). If the data is needed globally, you might use context or a global store, but for local component usage, state is fine.

### Forms in React – Controlled Components

Forms in React are ubiquitous – login forms, search bars, etc. Handling forms typically means making the form elements **controlled components** (React state tracks the input value) or using refs for uncontrolled. We’ll focus on controlled forms as they integrate well with React’s data flow.

**Basic controlled input:**  
```jsx
function NameForm() {
  const [name, setName] = useState('');
  return (
    <form onSubmit={e => { e.preventDefault(); alert(name); }}>
      <label>
        Name: <input type="text" value={name} onChange={e => setName(e.target.value)} />
      </label>
      <button type="submit">Submit</button>
    </form>
  );
}
```
In this example:
- The input’s `value` is bound to the state variable `name`. So the displayed value is always up-to-date with React state.
- The `onChange` handler updates the state with `setName(e.target.value)` on each keystroke. This makes the React state the “single source of truth” for the input’s value ([Forms – React](https://legacy.reactjs.org/docs/forms.html#:~:text=We%20can%20combine%20the%20two,is%20called%20a%20%E2%80%9Ccontrolled%20component%E2%80%9D)) 
- On submit (form’s onSubmit), we call `e.preventDefault()` to stop the page reload (HTML forms submit causing page navigation by default). Instead, we handle the data (here just alerting it, but normally you’d send it somewhere or update global state).

Using this approach, you can easily validate or manipulate input as user types, or have multiple inputs controlled by different state variables. It’s a bit more code than letting the DOM manage it, but it gives you fine control.

**Textarea and Select:** They work similarly, but note in JSX:
```jsx
<textarea value={text} onChange={...} />  // no children, unlike HTML <textarea>value</textarea>
<select value={selectedOption} onChange={...}>
  <option value="A">Option A</option>
  ...
</select>
```
For select with multiple, the value could be an array of selected values.

**Checkbox and radio:** Use `checked` attribute instead of value:
```jsx
<input type="checkbox" checked={isChecked} onChange={e => setChecked(e.target.checked)} />
```
Likewise for radio (each radio in a group gets a checked prop based on some state).

**Uncontrolled forms:** Alternatively, you can use refs to get form values on submit (uncontrolled components) ([Uncontrolled Components – React](https://legacy.reactjs.org/docs/uncontrolled-components.html#:~:text=In%20most%20cases%2C%20we%20recommend,handled%20by%20the%20DOM%20itself))  For example:
```jsx
const inputRef = useRef();
<input type="text" ref={inputRef} />
// on submit:
const value = inputRef.current.value;
```
But you then manage less through React, which can be fine for simple cases or integrating with non-React code, but you lose the immediate sync with state. React docs: *“In most cases, we recommend using controlled components to implement forms… The alternative is uncontrolled components, where form data is handled by the DOM itself.”* ([Uncontrolled Components – React](https://legacy.reactjs.org/docs/uncontrolled-components.html#:~:text=In%20most%20cases%2C%20we%20recommend,handled%20by%20the%20DOM%20itself))  Uncontrolled might be easier when you have very simple forms or migrating old code.

### Handling Form Submission

When the user submits a form (presses Enter or clicks a submit button), you likely want to:
- Prevent the default full page refresh (`e.preventDefault()` in the submit handler) ([Handling Events – React](https://legacy.reactjs.org/docs/handling-events.html#:~:text=Another%20difference%20is%20that%20you,of%20submitting%2C%20you%20can%20write)) 
- Gather the form data (from state if controlled, or from refs/`new FormData(e.target)` if uncontrolled).
- Possibly validate the data.
- Send it somewhere: either update state in your app (like logging in setting user context) or send an HTTP POST/PUT request to a server.

React doesn’t provide a built-in form helper for submitting; you handle it in your function. If using controlled components, you already have the latest values in state, so you can use those. If using uncontrolled with refs, you retrieve their `.current.value`.

**Example – Controlled Login Form:**
```jsx
function LoginForm() {
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');
  const [error, setError] = useState(null);

  function handleSubmit(e) {
    e.preventDefault();
    // Basic validation
    if (!email || !password) {
      setError("Email and password are required");
      return;
    }
    // Perform login (pseudo-code)
    loginApi(email, password)
      .then(user => { /* handle success, perhaps lift state to parent or context */ })
      .catch(err => setError("Login failed: " + err.message));
  }

  return (
    <form onSubmit={handleSubmit}>
      {error && <p className="error">{error}</p>}
      <label>
        Email: <input value={email} onChange={e => setEmail(e.target.value)} />
      </label>
      <label>
        Password: <input type="password" value={password} onChange={e => setPassword(e.target.value)} />
      </label>
      <button type="submit">Login</button>
    </form>
  );
}
```
Here we manage state for each input and handle errors. This is a typical controlled form approach. We prevent default submission and use our own logic to decide what to do with the data.

### Combining Forms and HTTP

Often, a form submission triggers an HTTP request (like login, signup, search query to server, etc.). You can use the techniques above together:
- On submit, gather input from state.
- Use fetch/axios to send a request with that data.
- Handle the promise to give feedback or update the UI (e.g., on success, navigate to another page or clear the form; on error, show an error message).

**Example – Search Form that fetches results:**
```jsx
function Search() {
  const [query, setQuery] = useState('');
  const [results, setResults] = useState(null);
  const [loading, setLoading] = useState(false);

  function handleSubmit(e) {
    e.preventDefault();
    setLoading(true);
    fetch(`/api/search?q=${encodeURIComponent(query)}`)
      .then(res => res.json())
      .then(data => setResults(data))
      .catch(err => console.error(err))
      .finally(() => setLoading(false));
  }

  return (
    <div>
      <form onSubmit={handleSubmit}>
        <input value={query} onChange={e => setQuery(e.target.value)} placeholder="Search..." />
        <button type="submit" disabled={loading}>Search</button>
      </form>
      {loading && <p>Searching...</p>}
      {results && <SearchResults data={results} />}
    </div>
  );
}
```
This ties it together: a controlled input for query, on submit it starts a fetch, and we use state to show loading and then results.

### Best Practices for Forms and HTTP in React

- **Keep state minimal:** Only keep what you need in React state. For example, for forms, you might not need to keep every field’s raw errors in state if they can be derived, but sometimes you will for showing messages.
- **Debounce frequent requests:** If you have a search that fires on every keystroke, consider debouncing the fetch call (or using useEffect with a timeout) so you’re not hitting the server excessively.
- **Loading and Error States:** Manage these in state to provide feedback. A common pattern is a `status` state that can be `"idle"`, `"loading"`, `"error"`, `"success"`, etc., and maybe an `errorMessage`. This way the UI can react accordingly.
- **Don’t forget keys on lists:** If your HTTP request returns an array that you render, ensure you add a `key` prop to list items (like we warned earlier).
- **Security:** Never trust form inputs blindly. If sending to a server, do server-side validation as well. React is just UI; real security should be on the backend.

By following these patterns – using useEffect for initial data loads ([AJAX and APIs – React](https://legacy.reactjs.org/docs/faq-ajax.html#:~:text=Where%20in%20the%20component%20lifecycle,I%20make%20an%20AJAX%20call))  controlling form inputs with state, and preventing default form behavior to plug in your own logic – you can handle most scenarios of forms and network in React. As apps grow, you might introduce more structure (like state management libraries or data fetching libraries), but these fundamentals remain the same.

**Sources:** Official recommendation on data fetching timing ([AJAX and APIs – React](https://legacy.reactjs.org/docs/faq-ajax.html#:~:text=Where%20in%20the%20component%20lifecycle,I%20make%20an%20AJAX%20call))  Controlled form concept ([Forms – React](https://legacy.reactjs.org/docs/forms.html#:~:text=We%20can%20combine%20the%20two,is%20called%20a%20%E2%80%9Ccontrolled%20component%E2%80%9D)) 
---

# 11. React Router and Forms

Single-page applications often require client-side routing to navigate between different “pages” or views without a full server reload. **React Router** is the de facto standard library for routing in React. In this chapter, we’ll introduce React Router and how to handle forms/navigation together (like submitting forms and navigating, or using forms within routed components).

### React Router Basics

**React Router** enables navigation among views of various components in a React application, mimicking multi-page behavior in a single-page app. It uses components to define routes and links.

To use React Router (v6 as of this writing):
1. Install it: `npm install react-router-dom`.
2. At your app’s root, wrap it with a router component (typically `<BrowserRouter>` for web):
   ```jsx
   import { BrowserRouter } from 'react-router-dom';
   ReactDOM.render(
     <BrowserRouter>
       <App />
     </BrowserRouter>,
     document.getElementById('root')
   );
   ```
3. Define routes inside your app. In v6, you use `<Routes>` and `<Route>` components:
   ```jsx
   import { Routes, Route, Link, NavLink } from 'react-router-dom';

   function App() {
     return (
       <div>
         <nav>
           <Link to="/">Home</Link>
           <Link to="/about">About</Link>
         </nav>
         <Routes>
           <Route path="/" element={<HomePage />} />
           <Route path="/about" element={<AboutPage />} />
           <Route path="/users/:id" element={<UserProfile />} />
           <Route path="*" element={<NotFoundPage />} />
         </Routes>
       </div>
     );
   }
   ```
   Here:
   - `<Routes>` is a container for route definitions.
   - Each `<Route>` has a `path` and an `element` (the component to render when the URL matches the path). For example, path “/about” renders `<AboutPage />`.
   - A path with `:id` denotes a URL param (like `/users/123`). Inside `UserProfile`, you can access that param via hooks (e.g., `useParams()` from React Router).
   - The last route path="*" is a wildcard catch-all for unmatched routes, rendering a NotFound component (optional but good UX).
   - The `<Link>` components create navigational links that, when clicked, update the URL **without reloading the page**, and React Router will render the matching route component. Think of `Link` as an `<a>` tag that does client-side navigation. Use `to` prop instead of `href`.

Using React Router, you get a declarative way to define navigation. When a user clicks a `Link` or programmatically navigates (with `useNavigate()` hook, which can replace history.push), the router updates the URL and displays the corresponding component.

**Navigation and forms:** If you have a form (say a search form) that upon submit should navigate to a results page, you would:
- Prevent default submission.
- Use the router to navigate to a new route, possibly including query params or state.

For example, using `useNavigate`:
```jsx
import { useNavigate } from 'react-router-dom';
function SearchForm() {
  const navigate = useNavigate();
  const [query, setQuery] = useState('');
  const handleSubmit = e => {
    e.preventDefault();
    navigate(`/search?query=${encodeURIComponent(query)}`);
  };
  return (
    <form onSubmit={handleSubmit}>
      <input value={query} onChange={e => setQuery(e.target.value)} />
      <button type="submit">Search</button>
    </form>
  );
}
```
This will programmatically navigate to `/search?query=...` which should be a route your app handles (e.g., `<Route path="/search" element={<SearchResultsPage />} />`). The `SearchResultsPage` can use `useLocation()` to get the query string and extract the query param, then perhaps fetch results.

React Router also provides `<Form>` in v6.4+ which can integrate with its data fetching (though at time of writing that’s fairly new and beyond basics). Most commonly, you’ll manually handle form submission as shown.

**Using NavLink:** NavLink is like Link but adds styling for the active route. For example:
```jsx
<NavLink to="/about" className={({ isActive }) => isActive ? 'active' : ''}>
  About
</NavLink>
```
This will apply 'active' class when the current URL matches "/about". This is helpful for navigation menus indicating the current page.

### Working with Route Params and Forms

If you have a form on a page with dynamic route (e.g., an edit form at `/users/:id/edit`):
- You’d use `useParams()` to get `id` from URL.
- Likely fetch the current data for that user (maybe with useEffect on mount).
- Use a controlled form to allow editing.
- On submit, call an API to save and then navigate away or show a success message.

For example:
```jsx
function EditUserPage() {
  const { id } = useParams();
  const [userData, setUserData] = useState(null);
  const navigate = useNavigate();
  useEffect(() => {
    fetch(`/api/users/${id}`).then(res => res.json()).then(data => setUserData(data));
  }, [id]);

  const handleSubmit = e => {
    e.preventDefault();
    fetch(`/api/users/${id}`, { method: 'PUT', body: JSON.stringify(userData) })
      .then(() => navigate(`/users/${id}`));  // go back to profile page
  };

  if (!userData) return <p>Loading...</p>;
  return (
    <form onSubmit={handleSubmit}>
      <label>Name: 
        <input 
          value={userData.name} 
          onChange={e => setUserData({ ...userData, name: e.target.value })}
        />
      </label>
      {/* other fields... */}
      <button type="submit">Save</button>
    </form>
  );
}
```
In this scenario, React Router allows your EditUserPage to be rendered when URL matches `/users/123/edit`. The form loads user 123's data, allows editing, then on submit saves and navigates to `/users/123` (profile view) – possibly using navigate function to programmatically route.

### Forms with Navigation (like search, filtering)

It’s common to use the URL to reflect form state. For instance, if you have filters (checkboxes, selects) on a products page, you might update the query params as the user changes filters, so that the URL can be shared or revisited to get the same state.

React Router’s `useSearchParams()` can help manage query string in a state-like way. For example:
```jsx
function ProductsPage() {
  const [searchParams, setSearchParams] = useSearchParams();
  const [category, setCategory] = useState(searchParams.get('category') || 'all');

  useEffect(() => {
    // update query param when category state changes
    searchParams.set('category', category);
    setSearchParams(searchParams);
  }, [category]);

  // fetch products based on category...
}
```
Alternatively, form submission could directly navigate with desired params as shown earlier.

**React Router and Form Considerations:**
- If your form is on a route and after submission you navigate to another route, ensure that route is defined and can handle the data (perhaps via location state or by fetching based on params).
- If using older React Router (v5), the concepts are similar but you’d use `<Switch>` and `<Route>` with `component` or `render` props, and `withRouter` HOC or hooks from `react-router` (like `useHistory`).
- For multi-step forms, you might even break each step into a route (like `/signup/step1`, `/signup/step2`, etc.). React Router can handle that by treating each step as a separate route and perhaps preserving data via context or query params.

### Integration Example: A Protected Form

Imagine an “Edit Profile” form that should only be accessible if logged in:
- You could have a route `<Route path="/profile/edit" element={<ProtectedRoute><EditProfileForm /></ProtectedRoute>} />`.
- `ProtectedRoute` could be an element that checks auth (via context or a hook) and either renders children or navigates to login.
- Inside EditProfileForm, you load user data and allow editing.

This shows combining routing (protected route, dynamic URL) with forms (editing data and submitting).

**Key points:**
- Use `Link` or `navigate` instead of `<a>` to route without reloading the page (preserving SPA performance).
- If you want to cause a full page reload (rare in SPAs, but maybe to an external site), you’d use a normal `<a>` tag or `window.location`.
- React Router allows nested routes (e.g., define routes inside other components). This can be powerful for layout components that have their own sub-routes.

Finally, always handle the scenario where a route doesn’t exist (404). We showed a "*" route for that. Also, consider using `NavLink` to highlight active navigation tabs.

By using React Router, you turn your React app into a multi-page feeling app without server round-trips on each navigation. And by properly handling forms within this routing context (often involving preventing default and using router navigation), you create smooth user experiences.

**Sources:** Explanation of client-side routing with React Router ([React Router Basics: Routing in a Single-page Application](https://www.loginradius.com/blog/engineering/react-router-basics/#:~:text=As%20hinted%20at%20in%20the,rendering%20based%20on%20URL%20path))  `Link` vs traditional navigation ([React Router Basics: Routing in a Single-page Application](https://www.loginradius.com/blog/engineering/react-router-basics/#:~:text=As%20hinted%20at%20in%20the,rendering%20based%20on%20URL%20path))  ([React Router Basics: Routing in a Single-page Application](https://www.loginradius.com/blog/engineering/react-router-basics/#:~:text=allows%20containers%20to%20be%20swapped,rendering%20based%20on%20URL%20path)) 

---

# 12. Form Handling and Validation

Building forms is a common task, and beyond basic input handling, real-world forms need **validation** (ensuring the data is correct) and often more complex interactions. In this chapter, we’ll discuss strategies for form handling at scale, including validation approaches (both manual and using libraries like Formik or React Hook Form).

### Controlled Forms Recap and Scaling Up

For simple forms with a couple of fields, controlling each input with `useState` and writing a submit handler is straightforward. As forms grow (imagine dozens of fields), managing state for each can become repetitive. You might still use multiple useState hooks or a single useReducer to manage form state as one object. 

Example using a single state object for form:
```jsx
const [formData, setFormData] = useState({ name: '', email: '', password: '' });
function handleChange(e) {
  setFormData({ ...formData, [e.target.name]: e.target.value });
}
...
<input name="name" value={formData.name} onChange={handleChange} />
```
This way one handler updates any field by name, spreading formData to update that field. This DRYs up your code for large forms. Just ensure each input has a unique name that matches a key in the state object.

### Client-side Validation

Validation can be done:
- **On the client side (in the browser)**: to give immediate feedback to users.
- **On the server side**: to ensure data integrity (never rely solely on client validation, server must validate too, but that’s beyond React’s scope).

For client-side, you can validate:
- **On field blur** (when user leaves a field): e.g., check if an email is valid once they tab out.
- **On form submit**: check all fields and show errors.
- **On change (live validation)**: sometimes used for things like password strength meter or validating as user types.

You can implement validation manually:
```jsx
const [errors, setErrors] = useState({});
function validate() {
  const newErrors = {};
  if (!formData.email.includes('@')) {
    newErrors.email = "Invalid email address";
  }
  if (formData.password.length < 8) {
    newErrors.password = "Password must be at least 8 characters";
  }
  setErrors(newErrors);
  return Object.keys(newErrors).length === 0;
}
function handleSubmit(e) {
  e.preventDefault();
  if (validate()) {
    // proceed to submit to server
  }
}
```
In the JSX, you might display errors:
```jsx
<input name="email" ... />
{errors.email && <span className="error">{errors.email}</span>}
```

**Best practice:** Keep error messages in state, often in an object mapping field names to messages. Validate on submit, and optionally on blur/change to enhance UX. Ensure to clear or update errors as the user fixes inputs.

### Using Form Libraries

For larger projects, libraries can simplify form state and validation:
- **Formik:** A popular form library that manages form state, handles submissions, and integrates with validation libraries like Yup. It provides a `<Formik>` component or hook (`useFormik`) to tie form elements together.
- **React Hook Form:** A newer library that leverages Hooks (and uncontrolled components internally) for very performant form handling. It uses refs to track inputs and provides a useForm hook.
- **Redux Form or others:** In older patterns, forms were managed in Redux state. Redux Form (now deprecated in favor of Redux Toolkit + other libs) at the time managed form state but could be heavy.

**Formik example:**
```jsx
<Formik
  initialValues={{ email: '', password: '' }}
  validate={values => {
    const errors = {};
    if (!values.email) {
      errors.email = 'Required';
    } else if (!/^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,}$/i.test(values.email)) {
      errors.email = 'Invalid email address';
    }
    return errors;
  }}
  onSubmit={(values, { setSubmitting }) => {
    // submit logic
    setSubmitting(false);
  }}
>
  {({ values, errors, handleChange, handleSubmit, isSubmitting }) => (
    <form onSubmit={handleSubmit}>
      <input type="email" name="email" value={values.email} onChange={handleChange} />
      {errors.email && <div>{errors.email}</div>}
      <input type="password" name="password" value={values.password} onChange={handleChange} />
      {errors.password && <div>{errors.password}</div>}
      <button type="submit" disabled={isSubmitting}>Submit</button>
    </form>
  )}
</Formik>
```
Formik handles a lot: it tracks `values`, `errors`, submission state (`isSubmitting`). We provide a validate function or you can use a schema (like Yup) for validation. Many developers like Formik for complex forms, as it reduces boilerplate.

**React Hook Form example:**
```jsx
import { useForm } from 'react-hook-form';

function ContactForm() {
  const { register, handleSubmit, formState: { errors } } = useForm();
  const onSubmit = data => console.log(data);
  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input {...register("name", { required: true })} placeholder="Name" />
      {errors.name && <p>Name is required</p>}
      <input {...register("email", { 
                 required: "Email is required", 
                 pattern: { value: /\S+@\S+\.\S+/, message: "Invalid email" }
               })} 
             placeholder="Email" />
      {errors.email && <p>{errors.email.message}</p>}
      <button type="submit">Send</button>
    </form>
  );
}
```
Here `register` function connects inputs to the form state, and we specify validation rules. React Hook Form will populate `errors` if validation fails. It’s very concise and performs well by not re-rendering on every keystroke (it uses refs until you submit or explicitly watch fields).

**The benefits of these libraries:** They manage form state in a scalable way and often handle performance optimizations. They also often integrate with UI libraries or provide components to reduce boilerplate.

### Common Pitfalls in Forms

- **Not preventing default:** If you forget `e.preventDefault()` on submit, the browser will do a full page refresh, losing React state. Using onSubmit in React (either through Formik/HookForm or your own handler) and calling preventDefault is crucial.
- **Controlled vs Uncontrolled mismatch:** If you initially set an input without a value then later provide one, React might warn about switching from uncontrolled to controlled. Always initialize your state for each field (e.g., empty string) so it’s controlled from start.
- **Validation triggers:** Over-validating can annoy users (e.g., showing errors while they are still typing). A typical UX is to validate on blur or on submit, not on every keystroke for fields like email or name. However, some fields like password strength might update live.
- **Managing focus:** On error, you might want to focus the first failing field. React provides refs you can attach to inputs and then call `ref.current.focus()` if needed.
- **Form Submission UX:** Provide feedback on submit (e.g., disable submit button while submitting, show a loading spinner, etc.). This prevents duplicate submissions and assures user something is happening.
- **Persisting form state on navigation:** If your form spans multiple routes or you navigate away, consider how to preserve what the user entered if they come back (maybe keep it in context or localStorage if needed).

### Comparison of Tools

Manual handling (with useState/useReducer) is fine for many cases and gives full control. Formik simplifies form logic a lot but adds a layer of abstraction. React Hook Form focuses on minimal rerenders and uses uncontrolled component paradigm under the hood which can be more performant (especially with lots of fields) ([When should you use React Hook Form, and Why - DEV Community](https://dev.to/gervaisamoah/when-should-you-use-react-hook-form-and-why-1obd#:~:text=Some%20key%20features%20of%20React,Hook%20Form%20include))  Both Formik and React Hook Form can integrate with schema validation libraries like **Yup** to define a schema for your form data and automatically generate errors (this is powerful for consistent rules).

Formik example using Yup:
```jsx
const validationSchema = Yup.object({
  email: Yup.string().email("Invalid email").required("Required"),
  password: Yup.string().min(8, "Min 8 chars").required(),
});
<Formik initialValues={{ email:'', password:'' }} validationSchema={validationSchema} ...>
```
This way you separate validation logic from component code.

**Conclusion:** Effective form handling involves managing state of inputs, providing validation feedback, and handling submission (including async calls). Whether you choose to do it by hand or use a library, the goal is to ensure the user can input data easily and be informed of any issues, and that your app correctly captures and processes that data. By following best practices and possibly leveraging form libraries, you can avoid many common errors and build robust forms more quickly.

**Sources:** Formik’s goal (manage form state/validation) ([Validation | Formik](https://formik.org/docs/guides/validation#:~:text=Formik%20is%20designed%20to%20manage,of%20all%20of%20the%20above))  React Hook Form key features ([When should you use React Hook Form, and Why - DEV Community](https://dev.to/gervaisamoah/when-should-you-use-react-hook-form-and-why-1obd#:~:text=Some%20key%20features%20of%20React,Hook%20Form%20include)) (“Uncontrolled components; Minimal re-renders for improved performance; Validation handling; Integration with Yup”) which highlights why one might choose that library for efficiency.

---

# 13. State Management with Redux

As React applications grow, passing state via props or using context for everything can become challenging. **Redux** is a state management library commonly used with React to maintain predictable global state. In this chapter, we’ll outline how Redux works and how to integrate it with React.

### Why Redux?

Redux provides a **single source of truth** for application state in a **store**, and enforces that state can only be changed in a predictable fashion via **actions** and **reducers**. It helps manage complex state logic and sharing state between many components. 

Redux is often used when:
- You have a lot of application state that is needed in many places (e.g., authenticated user info, global UI state, cached data from server).
- You want predictable state updates (Redux’s strict unidirectional data flow and pure reducer functions provide this).

*“Redux is a predictable state container for JavaScript apps. It helps you write applications that behave consistently, run in different environments (client, server, native), and are easy to test.”* ([Redux with React is Simple. Redux is a predictable state container… | by Hidayat Arghandabi | JavaScript in Plain English](https://javascript.plainenglish.io/redux-with-react-is-simple-3e3480a83432#:~:text=Redux%20is%20a%20predictable%20state,and%20are%20easy%20to%20test))  Essentially, it centralizes state and makes state changes follow certain rules, which can greatly aid in debugging and scaling.

### Core Concepts of Redux

- **Store:** The Redux store holds the whole state tree of your application. There is usually a single store (you might split logic into multiple reducers combined into one store).
- **State:** The data, typically a plain JS object (or nested objects).
- **Action:** An object that represents an intention to change the state. It must have a `type` field (a string constant identifying the action) and can have additional data (payload).
- **Reducer:** A pure function `(state, action) => newState` that takes the previous state and an action, and returns the next state. The reducer must be pure (no side effects, and do not mutate state directly – instead return a new state object). 
- **Dispatch:** The function used to send an action to the store. `store.dispatch({ type: 'INCREMENT' })` will run the reducer and update the state.
- **Subscription:** Components subscribe to the store so they can re-render when the state they need changes.

Three main principles:
1. **Single source of truth:** the state of your whole app is stored in one object tree within the store ([Redux with React is Simple. Redux is a predictable state container… | by Hidayat Arghandabi | JavaScript in Plain English](https://javascript.plainenglish.io/redux-with-react-is-simple-3e3480a83432#:~:text=Redux%20is%20a%20predictable%20state,and%20are%20easy%20to%20test)) 
2. **State is read-only:** the only way to change state is to emit an action, an object describing what happened. (So you don’t directly set state in store; you dispatch actions.)
3. **Changes are made with pure functions:** Reducers implement how state is updated for each action.

For example, a counter reducer:
```js
function counterReducer(state = { count: 0 }, action) {
  switch(action.type) {
    case 'INCREMENT':
      return { count: state.count + 1 };
    case 'DECREMENT':
      return { count: state.count - 1 };
    default:
      return state;
  }
}
```
The store could be created as `createStore(counterReducer)` (with Redux toolkit or legacy redux package).

Dispatching actions:
```js
store.dispatch({ type: 'INCREMENT' });
```
Now any subscriber (like a React component) can get the updated state (count increased).

### Using Redux in React

With React, we use the **react-redux** library to connect Redux store to components.

Steps:
- Create the Redux store, likely in a separate file (possibly combining multiple reducers if needed).
- Provide the store to the React app using `<Provider store={store}>` at the root. This makes the Redux store available to any nested components via React context.
- Use `useSelector` and `useDispatch` hooks (in modern React-Redux) or the older `connect` HOC to interact with the store in components.

**Example:** Suppose we have a Redux store with a reducer managing a list of todos and a loading flag. 

Providing the store:
```jsx
import { Provider } from 'react-redux';
import store from './store';
ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);
```

In a component:
```jsx
import { useSelector, useDispatch } from 'react-redux';

function TodoList() {
  const todos = useSelector(state => state.todos);  // select part of state
  const loading = useSelector(state => state.loading);
  const dispatch = useDispatch();

  useEffect(() => {
    dispatch({ type: 'FETCH_TODOS_REQUEST' });
    fetch('/api/todos')
      .then(res => res.json())
      .then(data => dispatch({ type: 'FETCH_TODOS_SUCCESS', payload: data }))
      .catch(err => dispatch({ type: 'FETCH_TODOS_FAILURE', error: err }));
  }, [dispatch]);

  if (loading) return <p>Loading...</p>;
  return (
    <ul>
      {todos.map(todo => <li key={todo.id}>{todo.text}</li>)}
    </ul>
  );
}
```
Here, `useSelector` extracts the needed slices of state (React-Redux will automatically re-run this selector when store updates and trigger re-render if the data changed). `useDispatch` gives us the `dispatch` function to send actions.

The reducer would handle `'FETCH_TODOS_REQUEST'` (maybe set `loading=true`), `'FETCH_TODOS_SUCCESS'` (set `todos` and `loading=false`), etc.

This flow demonstrates how Redux centralizes data fetching status and the list of todos in global state, and the component simply reflects that state. If another component also needs to know loading status or the todos, it can use the same selectors without prop drilling from TodoList.

**Redux Toolkit:** In modern Redux usage, Redux Toolkit (RTK) is the recommended way to write Redux logic. It abstracts some of the boilerplate:
- Provides `configureStore` to set up the store (with devtools and middleware).
- Provides `createSlice` to define reducers + actions in one place with mutable syntax (which uses Immer under the hood to handle immutability).
- Example:
  ```js
  const todosSlice = createSlice({
    name: 'todos',
    initialState: { todos: [], loading: false },
    reducers: {
      fetchTodosRequest(state) { state.loading = true; },
      fetchTodosSuccess(state, action) { state.loading = false; state.todos = action.payload; },
      fetchTodosFailure(state) { state.loading = false; }
    }
  });
  export const { fetchTodosRequest, fetchTodosSuccess, fetchTodosFailure } = todosSlice.actions;
  export default todosSlice.reducer;
  ```
  This eliminates switch cases and action type constants.

**When to use Redux:** Not every app needs Redux. If your state management is simple (a few pieces of state lifted up or context usage), Redux might be overkill. But for large applications with complex interactions and a lot of shared state, Redux shines by giving structure and predictability. It also has powerful devtools: you can time-travel through state changes, log actions, etc., which is great for debugging. *It helps applications behave consistently* ([Redux with React is Simple. Redux is a predictable state container… | by Hidayat Arghandabi | JavaScript in Plain English](https://javascript.plainenglish.io/redux-with-react-is-simple-3e3480a83432#:~:text=Redux%20is%20a%20predictable%20state,and%20are%20easy%20to%20test))  as noted.

**State management comparison** (to tie with next chapters perhaps): Redux vs Context vs other libraries:
- Context is good for passing down data, but not as full-featured as Redux for complex logic (no built-in mechanism to handle async or middleware, etc.).
- There are alternatives like MobX (which is more OOP observable based) or Recoil (Facebook's experimental state library using atom/selector concepts). But Redux remains widely adopted and understood.

**Summary:** Redux introduces a structured approach: global store, actions to describe “what happened”, and reducers to compute new state, making state changes explicit and traceable ([Higher-Order Components – React](https://legacy.reactjs.org/docs/higher-order-components.html#:~:text=HOCs%20are%20common%20in%20third,Redux%E2%80%99s%20connect%20and%20Relay%E2%80%99s%20createFragmentContainer))  In React, react-redux hooks make using Redux fairly straightforward. For many large applications, this results in more maintainable code as the app grows, with state changes centralized and easier to debug.

**Sources:** Redux definition ([Redux with React is Simple. Redux is a predictable state container… | by Hidayat Arghandabi | JavaScript in Plain English](https://javascript.plainenglish.io/redux-with-react-is-simple-3e3480a83432#:~:text=Redux%20is%20a%20predictable%20state,and%20are%20easy%20to%20test))  Core concepts (store, actions, reducers) ([Introduction to Redux for State Management - Global Tech Council](https://www.globaltechcouncil.org/react/redux-for-state-management/#:~:text=Core%20concepts%20include%20the%20store%2C,Setting%20up%20Redux%20involves)) noting the single source of truth and necessity of understanding store/actions/reducers.

---

# 14. Material UI and Common Errors

Building UIs often involves using component libraries to speed up development. **Material-UI (MUI)** is a popular React UI framework following Google’s Material Design. In this chapter, we’ll cover how to use Material UI components and discuss some common errors developers encounter in React (and how to fix them).

### Material UI Basics

**Material UI (MUI)** provides a set of pre-built React components (like buttons, dialogs, grids, etc.) with Material Design styling out of the box. It allows developers to quickly create a consistent, themeable UI. 

To use Material UI:
- Install it: `npm install @mui/material @emotion/react @emotion/styled`. (Material-UI v5 uses Emotion for styling by default.)
- Import components as needed and use them like any React component.

**Example: Using Material UI Button and TextField**  
```jsx
import { Button, TextField } from '@mui/material';

function LoginForm() {
  return (
    <form>
      <TextField label="Email" variant="outlined" fullWidth margin="normal" />
      <TextField label="Password" type="password" variant="outlined" fullWidth margin="normal" />
      <Button variant="contained" color="primary" type="submit">Login</Button>
    </form>
  );
}
```
This renders nicely styled input fields and a button without custom CSS. Material UI handles the visual aspects, responsive layout if using their Grid or Box system, and interactions (like ripple effects on buttons).

**Customizing Material UI:** 
- Props: Most components have props to adjust styling/behavior (like `variant`, `color` on Button as shown).
- Themes: You can wrap your app in a `ThemeProvider` and create a custom theme to override colors, typography, etc. Material UI’s theming system allows you to define a palette (primary, secondary colors, etc.) and apply it consistently.
- CSS overrides: You can pass `sx` prop (in MUI v5) for quick CSS overrides (using a styling object).
  
Material UI aims to cover a wide range of common UI needs, so before reinventing a component, check MUI’s library (they have everything from accordions to progress spinners).

Material UI follows Material Design guidelines, which might dictate certain UX patterns. If your design matches that style, MUI saves a ton of time.

**Common Pitfalls with Material UI:**
- **Not wrapping in ThemeProvider:** If you customize theme, ensure to use MUI’s `<ThemeProvider theme={customTheme}>`. If omitted, components still work (they use default theme), but your customizations won’t apply.
- **Typography differences:** MUI might globally style `<body>` or use its own Typography component. If text looks off, consider wrapping content in `<Typography>` tags or customizing the theme’s typography scale.
- **Importing from wrong package:** Material UI v4 vs v5 differences. In v5, everything is in `@mui/material`. In older versions, it was `@material-ui/core`. Using mismatched version docs can lead to import errors.
- **CSS injection order issues:** If you override styles, sometimes you need to ensure your CSS loads after MUI’s. MUI v5 with Emotion largely handles this via `StyledEngineProvider` if needed. But be aware if using something like CSS Modules to override MUI class names, you might need to increase specificity or use `!important`.

Overall, Material UI can significantly accelerate development and reduce styling bugs because components are pre-tested and accessible.

### Common Errors in React (and how to fix them)

**1. Uncaught Invariant Violation: "X is not a function" or "X is undefined":**  
This often comes from using something before it’s defined or importing incorrectly. For example, using `useState` without importing it (`useState is not a function`). Solution: check imports, ensure proper named imports (`import { useState } from 'react'`). Also ensure functions are called correctly (e.g., if you did `const [value, setValue] = useState()` instead of `useState(initialValue)` you’ll get an error).

**2. "Cannot update a component while rendering a different component":**  
This warning happens if you call a state update (or dispatch) in the middle of rendering another component. Typically, this is by accident – e.g., calling `setState` in a component body (which runs during render). Fix: Move that state update into a useEffect or an event handler. For example, if you were doing:
  ```js
  function Parent() {
    // BAD: setState during render
    if (someCondition) {
      setOtherState(...);
    }
    return <Child />;
  }
  ```
  Instead, derive that logic outside of render or in useEffect so you’re not updating state as a side effect of rendering.

**3. "Each child in a list should have a unique 'key' prop":**  
This is a very common warning when rendering lists (like mapping an array to JSX). It means you forgot to provide a key, or the key isn’t unique. To fix: add a `key` prop to each element in the list, using a unique identifier (like an ID from data). Example:
  ```jsx
  {items.map(item => <li key={item.id}>{item.name}</li>)}
  ```
  If you used index as key, this warning wouldn’t show, but using index can cause issues if list order changes or items are added/removed (not truly unique identity across updates). Best practice is to use a stable ID.

**4. "Warning: A component is changing an uncontrolled input to be controlled" or vice versa:**  
This occurs when an input’s value prop goes from `undefined` (uncontrolled) to defined (controlled) or vice versa. For instance, if you conditionally render an input with value depending on state, or forget to initialize state. Fix: Always initialize the state for that input, even with an empty string, so it’s controlled from start. Or if intentionally uncontrolled, don’t later give it a value prop. Example fix:
  ```jsx
  const [name, setName] = useState(''); // initialize to empty string instead of undefined
  <input value={name} onChange={...} />
  ```

**5. "Warning: Can't perform a React state update on an unmounted component":**  
This happens if an async operation (like fetch or setTimeout) tries to set state after a component has unmounted. Common with data fetching in useEffect – if the component unmounts before fetch completes, the `setState` in the .then triggers this warning. Fix: Cancel the async operation or check mounted status. You can use a flag or AbortController for fetch:
  ```jsx
  useEffect(() => {
    let isMounted = true;
    fetchData().then(data => {
      if (isMounted) setData(data);
    });
    return () => { isMounted = false; };
  }, []);
  ```
  Or use `abortController.abort()` in cleanup for fetch to stop request.

**6. Stale closures (especially with Hooks):**  
E.g., using state inside a setTimeout in useEffect but not including it in dependencies – the timeout callback closes over old state. Fix: either include necessary state in dependencies so effect re-schedules when state changes, or use functional state updates to always get fresh state. This is not a red error but a logic bug often encountered.

**7. Infinite re-render (Max update depth exceeded):**  
Usually caused by updating state on every render (like forgetting to put an empty dependency array in useEffect, or calculating state that calls setState without conditions). Check useEffect dependencies and ensure you’re not calling setState unconditionally in render or effect without proper guard.

**Material UI related common issues:**

- **Module not found errors:** if you install @mui/material but forget @emotion packages, MUI v5 will error (since it uses emotion for styling). Solution: install required peer deps (emotion).
- **Icon usage:** If using Material Icons, you install `@mui/icons-material` and import e.g. `import DeleteIcon from '@mui/icons-material/Delete';`. If you forget to install icons package, you get errors trying to import them.
- **MUI styling override issues:** Trying to override styles but seeing they don't apply. MUI uses specific CSS classes; if you try to override via global CSS, ensure your CSS is loaded after, or use the `sx` prop or `styled` utility MUI provides for consistency.

### Debugging Common Errors

For runtime errors, always check the console error stack trace. It often pinpoints the file/line causing it. Warnings (like key warning) include a stack or at least component name to guide you.

Leverage React DevTools for component state debugging, and Redux DevTools if using Redux to see if state updates as expected.

**ESLint and TypeScript** can catch many mistakes before runtime:
- ESLint plugin for React can warn about missing keys, direct DOM manipulation, etc.
- TypeScript can catch undefined values, incorrect prop types, etc.

Finally, knowledge of these typical errors means you can recognize them instantly and apply the fix. For example, the key warning is so common that once you've seen it a few times, you immediately know to check your list rendering.

**Conclusion:** Material UI can significantly improve your development speed and UI consistency, just be mindful of properly setting it up and theming. And common React errors often have straightforward fixes once you understand the root cause, whether it's adding a key prop or adjusting how you update state. With experience, these errors become easier to avoid and fix, leading to smoother development.

**Sources:** Material UI introduction ([Material UI vs. Chakra UI: Which One to Choose? - DEV Community](https://dev.to/codeparrot/material-ui-vs-chakra-ui-which-one-to-choose-14f4#:~:text=Material%20UI%20is%20a%20popular,visually%20appealing%20and%20functional%20applications))  Key prop warning reference ([10 Common Mistakes to Avoid in React Development - Medium](https://medium.com/@sufianmustafa0900/10-common-mistakes-to-avoid-in-react-development-61a281e643ce#:~:text=10%20Common%20Mistakes%20to%20Avoid,rendering)) (common mistakes with keys leading to re-render issues).
