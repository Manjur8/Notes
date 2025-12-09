# 🚀 FAANG-Level Scenario-Based React Questions & Answers

(Spoken like a real interview candidate)

### 1. Your React app becomes slow after adding a search feature. What do you do?

Answer:
First, I check where the bottleneck is using React Profiler.
If the slowdown happens while typing, it usually means the filter logic is expensive or causing heavy re-renders.
I solve it by wrapping the expensive computation in useMemo, and I wrap the search handler in useCallback to avoid recreating functions.
If the list is large, I switch to list virtualization using react-window so only visible items render.
Finally, I mark the filtering state with useTransition so the UI stays responsive even while searching.

### 2. You have a list of 50,000 items and the UI freezes. How do you optimize it?

Answer:
Rendering 50,000 DOM nodes at once is expensive.
I use windowing libraries like react-window or react-virtualized, which render only the items in the viewport.
Then I memoize each row with React.memo to avoid re-renders.
If filtering is involved, I also debounce the input and move filtering to a Web Worker so the UI thread remains free.

### 3. A React page renders inconsistently in SSR and CSR, causing hydration issues. What is your debugging approach?

Answer:
Hydration mismatches typically happen when the server and client generate different HTML.
I first look for non-deterministic values like timestamps, random IDs, or browser-only APIs in the render phase.
I move such logic into useEffect so it only runs on the client.
If I need dynamic content on the server, I stabilize the values using deterministic IDs or server time.
I re-run the app with hydration warnings enabled and fix each mismatch until the render is consistent.

### 4. A component re-renders too many times. How do you find and fix it?

Answer:
I use React DevTools Profiler to identify the exact component that is re-rendering.
Usually, the root cause is unstable props—like inline functions, inline objects, or unnecessary context updates.
I fix it by memoizing functions using useCallback, memoizing heavy calculations with useMemo, and wrapping the component with React.memo.
If context is causing it, I split the context into smaller ones or move the state closer to where it’s used.

### 5. How do you design a React system to handle millions of user interactions per day?

Answer:
I keep state local whenever possible and avoid lifting it unnecessarily.
I use React Query or SWR for caching server data, which prevents redundant network calls.
I split the UI into small memoized components, use RSC for heavy server-side work, and lazy-load non-critical sections.
For interaction-heavy areas, I use useTransition to keep the UI responsive and windowing for large lists.
Finally, I monitor performance in production with tools like Web Vitals.

### 6. You are asked to migrate a legacy class-based React app to hooks. What's your strategy?

Answer:
I start by identifying components with simple lifecycle logic, like componentDidMount + componentWillUnmount, and migrate them to useEffect.
Complex components with nested effects are migrated gradually.
I extract reusable logic from class components into custom hooks.
I also ensure that the business logic is preserved and covered with unit tests.
The migration happens in phases to avoid regressions and minimize risk.

### 7. Your React app lags while scrolling due to heavy DOM. What do you do?

Answer:
I check if the scroll handler is expensive. If so, I throttle or debounce it.
Next, I ensure I'm not doing layout thrashing—so I batch DOM reads and writes.
If the page has many elements, I implement virtualization.
Finally, I ensure CSS animations use GPU-accelerated properties like transform and opacity.

### 8. You have a deeply nested component tree suffering from prop drilling. How do you fix it?

Answer:
If the state is global in nature, I switch to Context API or a store like Zustand or Redux.
For large apps, I prefer splitting the context to avoid re-renders.
Alternatively, I create custom hooks to encapsulate logic and provide data directly where needed.

### 9. How do you avoid tearing and inconsistent UI in Concurrent Rendering?

Answer:
Tearing happens when different parts of the UI show inconsistent versions of state.
To prevent it, I keep related state together so they update atomically.
I use transitions for non-urgent updates so the UI stays consistent.
If multiple components depend on the same async data, I use a library like React Query to ensure they all read from the same cached value.

### 10. A child component needs to re-render only when a specific part of props change. What do you do?

Answer:
I wrap the child in React.memo and pass a custom comparison function.
This ensures the child re-renders only when the fields I care about actually change.
This technique is very useful in large list items or card components.

### 11. How do you optimize React for low-end devices?

Answer:
I minimize bundle size using code splitting, remove unused libraries, and compress images.
I keep component trees shallow and avoid unnecessary effects.
I use requestIdleCallback or transitions for non-urgent tasks.
I also avoid large synchronous JS that blocks the main thread.

### 12. The design team requests 60fps animations in React. How do you handle that?

Answer:
React is not ideal for heavy animations.
I either offload them to CSS animations or use libraries like Framer Motion which work outside the main React render cycle.
This prevents React from blocking animations and maintains smooth FPS.

### 13. You need to build a real-time dashboard (live updates every second). What is your approach?

Answer:
I use WebSockets or SSE for streaming data.
I store minimal state—only the latest values—to avoid re-render storms.
I batch updates using useTransition or useDeferredValue.
For charts, I use canvas or libraries that render outside React to avoid heavy DOM updates.

### 14. How do you test React components that rely on hooks and async logic?

Answer:
I use React Testing Library, which focuses on user behavior rather than implementation.
For async logic, I use waitFor and mock API calls using MSW.
I test custom hooks separately using renderHook.
I also isolate state-based logic so tests are stable and not dependent on timing.

### 15. Your application’s initial load time is slow. How do you fix it?

Answer:
I analyze the bundle using tools like Webpack Bundle Analyzer.
Then I split the bundle with React.lazy, remove unused dependencies, and compress JS/CSS.
I preload critical resources and push non-critical JS to after hydration.
Using React Server Components also reduces client-side bundle size dramatically.