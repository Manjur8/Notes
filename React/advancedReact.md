# 🚀 Ultra-Advanced React Questions (FAANG Level)

### 1. Explain how React Fiber improves rendering.

Answer:
React Fiber is a re-written reconciliation engine that makes rendering interruptible. Instead of rendering everything in one shot, it breaks work into small units. This allows React to pause work, prioritize more urgent updates, resume later, and avoid blocking the main thread. This is the foundation for features like concurrent rendering, transitions, and Suspense.

### 2. What problem does Concurrent Mode solve?

Answer:
Concurrent mode solves the problem of blocking renders. In large apps, heavy renders can freeze the UI. Concurrent features let React keep the UI responsive by preparing updates in the background without blocking interactions. It focuses on perceived performance, not raw speed.

### 3. How does Suspense for data fetching actually work internally?

Answer:
Suspense works by throwing promises during rendering. When a component tries to read data that isn’t ready, it throws a promise. React catches it, pauses the render, and shows a fallback. Once the promise resolves, React retries the render. This enables a unified async rendering model without explicit loading states.

### 4. How do React Server Components (RSC) differ from SSR?

Answer:
SSR renders HTML on the server but sends the entire JavaScript bundle to the client.
React Server Components render parts of the component tree entirely on the server and send a serialized tree structure (not HTML) to the client. These components never ship JavaScript to the client, reducing bundle size and improving performance.

### 5. Explain the difference between streaming SSR and traditional SSR.

Answer:
In traditional SSR, the server builds the full HTML before sending it.
In streaming SSR, React sends chunks of HTML as they are generated, allowing the browser to start rendering earlier. With Suspense boundaries, React can stream non-blocked parts first and fill in the rest later, dramatically improving Time To First Byte and perceived performance.

### 6. How does React handle priority scheduling?

Answer:
React uses its internal scheduler to assign priorities like:
 * Immediate
 * User-blocking
 * Normal
 * Low
 * Idle

Based on the priority, React decides whether to interrupt work, defer it, or batch it. This scheduling is what enables transitions and smooth user interactions.

### 7. What are transitions and how do they help UX?

Answer:
Transitions mark state updates as non-urgent. This tells React:
“Keep the old UI visible while preparing the new UI in the background.”
This avoids UI flickering and lag when filtering search results or rendering large lists.

### 8. How would you debug a React performance bottleneck in production?

Answer:
First, I check React DevTools Profiler to identify wasted re-renders and expensive components.
Then I look for unnecessary state lifting, unstable functions, and large list renders.
Next I enable memoization (React.memo, useMemo, useCallback), window large lists, and split bundles using lazy loading.
Finally, I use browser performance tools to measure paint, layout, and script bottlenecks.

### 9. What is the difference between hydration and progressive hydration?

Answer:
Hydration attaches event listeners to server-rendered HTML.
Progressive hydration hydrates only parts of the UI when they become visible or interactive.
This improves performance by not hydrating the full page immediately.

### 10. How does React avoid layout thrashing?

Answer:
React batches DOM writes together and keeps DOM reads separate. Whenever useLayoutEffect or refs are used for measurements, React minimizes the read/write interleaving that causes layout thrashing.

### 11. What is an async boundary in React?

Answer:
An async boundary is essentially a Suspense boundary. It defines a point in the UI where React can pause rendering due to async data and show fallback UI but still render the rest of the application normally.

### 12. How do you design a highly optimized component architecture for a large React app?

Answer:
I structure the app using domain-based folders, co-locate logic with components, use RSC for heavy data fetching, avoid prop drilling with Context or dedicated stores, aggressively use memoization, split large lists, and adopt transitions to keep interactions smooth.

### 13. How does React ensure consistency when multiple state updates occur?

Answer:
React batches multiple updates, even from async events, and processes them in a stable order. This ensures state updates are predictable and consistent.

### 14. Explain how keys work in the diffing algorithm for list rendering.

Answer:
Keys help React identify which items changed. Without keys, React matches items by index, causing unnecessary re-renders. With stable keys, React only re-renders components whose identities change, improving performance.

### 15. How would you implement infinite scrolling efficiently?

Answer:
I use Intersection Observer API to detect scroll thresholds, keep data virtualized using react-window or react-virtualized, fetch new pages in the background, and avoid rerendering the entire list by memoizing rows.

### 16. Why is context sometimes a performance problem?

Answer:
Any component consuming context re-renders when the context changes. In large apps, this can cause a cascading re-render chain. To avoid this, I split context, memoize value objects, or use Zustand/Jotai/Recoil.

### 17. What is a render phase vs. commit phase side effect?

Answer:
 * Render phase (not allowed): must be pure, no side effects.
 * Commit phase: safe to modify DOM or run effects.
React enforces this using useEffect (commit phase) and disallows effects in render.

### 18. How does React’s event delegation work?

Answer:
React attaches a single event listener at the root and uses an internal event system to handle events. This improves performance and maintains a consistent cross-browser event model.

### 19. What patterns replace HOCs in modern React?

Answer:
Custom Hooks replaced HOCs by extracting logic without creating nested component structures. Hooks are more readable and avoid wrapper hell.

### 20. Describe the ideal state management strategy for a large React app.

Answer:
I use local state for UI logic, Context for global settings, a lightweight store like Zustand or Jotai for shared business state, and React Query or SWR for server cache. This avoids Redux boilerplate and spreads load evenly across layers.