# 🚀 Advanced React Interview Questions
### 1. What is the difference between Server Components and Client Components in React?

Answer:
Server Components run on the server, so they don’t include JavaScript in the client bundle. They are great for data fetching and improving performance. Client Components run in the browser and can use state, effects, and browser APIs. In modern React, we mix both to get the best performance.

### 2. What is Concurrent Rendering in React?

Answer:
Concurrent rendering enables React to interrupt, pause, or resume renders. It prioritizes more urgent updates, making the UI feel more responsive. It doesn’t change the UI behavior, but improves performance under heavy workloads.

### 3. What is React Fiber?

Answer:
React Fiber is the internal engine behind React. It breaks rendering work into small units and spreads them across frames, which makes concurrency and features like Suspense possible.

### 4. What are Suspense boundaries?

Answer:
Suspense boundaries allow me to wrap parts of the UI that may delay due to data fetching or lazy loading. Instead of blocking the entire UI, only that part shows a fallback, improving user experience.

### 5. What are custom hooks and when do you use them?

Answer:
Custom hooks let me extract reusable logic out of components. I use them when multiple components share the same logic such as form handling, fetching data, or managing subscriptions.

### 6. What is the difference between useMemo and useCallback?

Answer:
useMemo memoizes a value, while useCallback memoizes a function.
I use useMemo for expensive computations and useCallback when passing functions to child components to prevent unnecessary re-renders.

### 7. How does React handle re-rendering?

Answer:
React re-renders a component when its state or props change. During reconciliation, React compares the new virtual DOM with the previous one and updates only the elements that changed. Memoization techniques help optimize unnecessary re-renders.

### 8. What are render props?

Answer:
Render props allow me to share logic across components by passing a function that returns UI. It’s an older pattern before hooks but still used in some libraries.

### 9. What are portals in React?

Answer:
A portal lets me render a component’s UI outside its parent DOM hierarchy. I commonly use it for modals, tooltips, and dropdowns.

### 10. What are error boundaries?

Answer:
Error boundaries catch JavaScript errors inside child components and show fallback UI instead of breaking the app. They only work in class components, but React 18+ supports error handling with Suspense for async errors.

### 11. How does React batching work?

Answer:
React batches multiple state updates into a single render for better performance. With React 18, batching happens automatically even inside promises, timeouts, and event handlers.

### 12. What is useImperativeHandle?

Answer:
useImperativeHandle lets me customize the value exposed to parent components when using refs. I use it only when I need imperative control, like exposing focus methods on custom input components.

### 13. What is useTransition?

Answer:
useTransition lets me mark certain updates as non-urgent. It keeps the UI responsive by showing old UI while the new UI is being prepared, commonly used in large list filtering.

### 14. What is useDeferredValue?

Answer:
useDeferredValue delays updating a piece of state until more urgent updates are complete. It's similar to debouncing but managed by React for smooth UIs.

### 15. What is the difference between client-side rendering (CSR), server-side rendering (SSR), and static site generation (SSG)?

Answer:

* CSR: Entire UI rendered in browser, slower first load.

* SSR: Server generates HTML for every request, better SEO.

* SSG: Pre-renders pages at build time, fastest for static content.

Frameworks like Next.js allow choosing per page.

### 16. How does React handle memory leaks?

Answer:
Memory leaks often happen due to unmounted components still holding subscriptions or timers. I prevent them by cleaning up side effects inside useEffect’s return function.

### 17. What is reconciliation algorithm?

Answer:
React uses the “diffing algorithm” to compare virtual DOM trees. It assumes components with different types produce different trees, and it compares lists using keys to minimize DOM operations.

### 18. What is lazy loading and code splitting?

Answer:
Lazy loading loads components only when needed. With React.lazy and Suspense, React automatically splits bundles and improves performance.

### 19. What is the difference between controlled and uncontrolled components at scale?

Answer:
Controlled components offer more control and validation but can be slower with complex forms. Uncontrolled components are more performant but less flexible. Libraries like React Hook Form balance both approaches.

### 20. Explain the rendering process in React.

Answer:
*React follows two phases:

- Render Phase – React builds the virtual DOM.

- Commit Phase – React updates the actual DOM.
The render phase is interruptible (in concurrent mode), but the commit phase is always synchronous.*

### 21. What is tree shaking in React apps?

Answer:
Tree shaking removes unused code during bundling. Tools like Webpack and Vite ensure only the parts of React you actually import are included in the final bundle.

### 22. What is the difference between “useEffect” and “useLayoutEffect”?

Answer:
useLayoutEffect runs synchronously before the browser paints, so it blocks rendering. useEffect runs after the paint. I only use useLayoutEffect when I need to measure DOM size or position.

### 23. What is hydration mismatch?

Answer:
Hydration mismatch happens when server-rendered HTML doesn’t match the HTML generated by the client. This usually happens when rendering non-deterministic values like dates or random numbers without handling them properly.

### 24. How does React optimize large lists?

Answer:
I use techniques like pagination, windowing (via react-window or react-virtualized), memoization, and stable keys. Rendering thousands of DOM nodes at once is avoided.

### 25. What are some common performance optimization techniques in React?

Answer:

- Memoizing components with React.memo

- Using useMemo and useCallback

- Windowing large lists

- Avoiding anonymous functions inside render

- Code splitting with React.lazy()

- Keeping state local and minimizing re-renders

- Avoiding prop-drilling with Context or Redux