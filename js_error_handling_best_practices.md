---


---

<h3 id="error-handling-best-practices-for-javascript-react-react-query-and-typescript-in-sensitive-applications">Error Handling Best Practices for JavaScript, React, React Query, and TypeScript in Sensitive Applications</h3>
<p><strong>Key Points:</strong></p>
<ul>
<li><strong>JavaScript Error Handling:</strong> Use try/catch for synchronous code and .catch() for asynchronous operations, but avoid overusing try/catch to let errors propagate appropriately.</li>
<li><strong>React Error Handling:</strong> Implement error boundaries to prevent app crashes and use try/catch for event handlers, ensuring a smooth user experience.</li>
<li><strong>React Query Error Handling:</strong> Leverage <code>isError</code> states and global <code>QueryCache</code> callbacks for consistent error management, especially for API calls.</li>
<li><strong>TypeScript Error Handling:</strong> Define custom error types for type safety and consider functional approaches like Result types for robust error handling.</li>
<li><strong>Sensitive Applications (e.g., Banking):</strong> Never expose sensitive details in error messages, log errors securely, and provide user-friendly feedback with error codes.</li>
<li><strong>Scalable Solutions:</strong> Use centralized error reporting services like Sentry and consistent logging strategies for maintainability.</li>
<li><strong>Controversy Note:</strong> Some developers advocate for functional error handling (e.g., Result types) over traditional try/catch, as seen in discussions from the JavaScript community, but both approaches have trade-offs depending on application needs.</li>
</ul>
<h4 id="general-javascript-error-handling">General JavaScript Error Handling</h4>
<p>In JavaScript, errors can disrupt application flow if not handled properly. For synchronous code, wrapping potentially risky operations in try/catch blocks allows you to catch and manage errors gracefully. For asynchronous code, such as promises or async/await, use .catch() to handle errors. It’s best to avoid catching errors unnecessarily—let them bubble up to a higher level where they can be handled more effectively. Creating custom error classes can help identify specific issues, making debugging easier. For example, instead of throwing a generic error, you might define a <code>DatabaseError</code> class for database-related issues.</p>
<h4 id="react-error-handling">React Error Handling</h4>
<p>React applications benefit from error boundaries, introduced in React 16, which catch errors in the component tree during rendering, lifecycle methods, or constructors, preventing the entire app from crashing. You can create an error boundary component to display a fallback UI, like an error message, when an issue occurs. However, error boundaries don’t catch errors in event handlers, so you’ll need try/catch blocks for those. For instance, if an onClick handler might fail, wrap its logic in a try/catch to handle errors without breaking the UI.</p>
<h4 id="react-query-error-handling">React Query Error Handling</h4>
<p>React Query, a library for managing server state in React, provides built-in error handling mechanisms. You can check the <code>isError</code> flag or <code>status === 'error'</code> to render error messages in components. For more advanced handling, enable <code>throwOnError</code> to integrate with React’s error boundaries, allowing errors from API calls to be caught and displayed gracefully. Setting up global error handling with <code>QueryCache</code> ensures consistent error notifications, such as showing a single toast message for failed API requests, which is particularly useful in large applications.</p>
<h4 id="typescript-error-handling">TypeScript Error Handling</h4>
<p>TypeScript enhances error handling by allowing you to define custom error types, ensuring type safety. For example, you can create a <code>CustomError</code> interface to enforce specific error properties, making it easier to handle errors predictably. Some developers prefer functional approaches, like using Result types, which return either a success value or an error, reducing reliance on try/catch. This can be particularly effective in TypeScript, where the type system helps enforce proper error handling.</p>
<h4 id="error-handling-in-sensitive-applications">Error Handling in Sensitive Applications</h4>
<p>For sensitive applications like banking, security is paramount. Never expose stack traces or detailed error messages to users, as these can reveal system vulnerabilities. Instead, provide generic messages like “Something went wrong, please try again” with an error code for support teams to reference. Log errors securely in a backend system for auditing and debugging, ensuring no sensitive data is included. Implement fail-safe mechanisms, such as defaulting to a safe state if an error occurs, to prevent unauthorized access or data leaks.</p>
<h4 id="scalable-error-handling-solutions">Scalable Error Handling Solutions</h4>
<p>To scale error handling in large applications, use centralized error reporting services like <a href="https://sentry.io/">Sentry</a> or Rollbar to track and analyze errors across the application. Implement a consistent logging framework to capture error details, including context like user actions or API responses. A uniform error handling strategy, such as a global error handler in React Query or a standardized error response format for APIs, ensures maintainability as the application grows.</p>
<h4 id="recommended-resources">Recommended Resources</h4>
<ul>
<li><strong>Books:</strong> <em>Eloquent JavaScript</em> by Marijn Haverbeke includes a section on error handling and bug fixing, while <em>JavaScript Error Handling</em> by Din Asotić focuses specifically on error handling and security.</li>
<li><strong>Articles:</strong> The <a href="https://legacy.reactjs.org/docs/error-boundaries.html">React Documentation on Error Boundaries</a> and <a href="https://tkdodo.eu/blog/react-query-error-handling">TkDodo’s blog on React Query Error Handling</a> provide practical guidance. For security, <a href="https://owasp.org/www-community/Improper_Error_Handling">OWASP’s guide on Improper Error Handling</a> is essential for sensitive applications.</li>
</ul>
<hr>
<h3 id="comprehensive-guide-to-error-handling-in-javascript-react-react-query-and-typescript-for-sensitive-and-data-intensive-applications">Comprehensive Guide to Error Handling in JavaScript, React, React Query, and TypeScript for Sensitive and Data-Intensive Applications</h3>
<p>This guide provides a detailed overview of error handling best practices for JavaScript, with a focus on React, React Query, and TypeScript, tailored for sensitive and data-intensive applications like banking systems. It incorporates insights from the JavaScript community, including YouTube videos, X posts, and reputable articles, as well as engineering blogs from companies like Google. The guide also addresses scalable error handling solutions and recommends resources for further reading.</p>
<h4 id="general-javascript-error-handling-1">1. General JavaScript Error Handling</h4>
<p>JavaScript applications encounter various error types, including syntax errors, runtime errors, and logical errors. Effective error handling ensures applications remain robust and user-friendly.</p>
<ul>
<li>
<p><strong>Try/Catch for Synchronous Code:</strong> Use try/catch blocks to handle errors in synchronous operations. For example:</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">try</span> <span class="token punctuation">{</span>
  <span class="token comment">// Risky operation</span>
  <span class="token keyword">const</span> result <span class="token operator">=</span> <span class="token function">riskyFunction</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span> <span class="token keyword">catch</span> <span class="token punctuation">(</span><span class="token class-name">error</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
  console<span class="token punctuation">.</span><span class="token function">error</span><span class="token punctuation">(</span><span class="token string">"An error occurred:"</span><span class="token punctuation">,</span> error<span class="token punctuation">.</span>message<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>
<p>This approach catches errors like <code>TypeError</code> or <code>ReferenceError</code> and prevents application crashes.</p>
</li>
<li>
<p><strong>Asynchronous Error Handling:</strong> For promises or async/await, use .catch() or try/catch. For instance:</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">async</span> <span class="token keyword">function</span> <span class="token function">fetchData</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
  <span class="token keyword">try</span> <span class="token punctuation">{</span>
    <span class="token keyword">const</span> response <span class="token operator">=</span> <span class="token keyword">await</span> <span class="token function">fetch</span><span class="token punctuation">(</span><span class="token string">"https://api.example.com/data"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token operator">!</span>response<span class="token punctuation">.</span>ok<span class="token punctuation">)</span> <span class="token keyword">throw</span> <span class="token keyword">new</span> <span class="token class-name">Error</span><span class="token punctuation">(</span><span class="token string">"Network error"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token keyword">return</span> <span class="token keyword">await</span> response<span class="token punctuation">.</span><span class="token function">json</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
  <span class="token punctuation">}</span> <span class="token keyword">catch</span> <span class="token punctuation">(</span><span class="token class-name">error</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    console<span class="token punctuation">.</span><span class="token function">error</span><span class="token punctuation">(</span><span class="token string">"Fetch failed:"</span><span class="token punctuation">,</span> error<span class="token punctuation">.</span>message<span class="token punctuation">)</span><span class="token punctuation">;</span>
  <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
<p>This ensures errors from API calls or network issues are handled gracefully.</p>
</li>
<li>
<p><strong>Avoid Over-Catching:</strong> Only catch errors where you can take meaningful action. Letting errors propagate to a higher level, such as a global error handler, reduces unnecessary code and improves debugging.</p>
</li>
<li>
<p><strong>Custom Error Classes:</strong> Define custom errors for specific scenarios, enhancing clarity. For example:</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">class</span> <span class="token class-name">DatabaseError</span> <span class="token keyword">extends</span> <span class="token class-name">Error</span> <span class="token punctuation">{</span>
  <span class="token function">constructor</span><span class="token punctuation">(</span>message<span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">super</span><span class="token punctuation">(</span>message<span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token keyword">this</span><span class="token punctuation">.</span>name <span class="token operator">=</span> <span class="token string">"DatabaseError"</span><span class="token punctuation">;</span>
  <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
<span class="token keyword">throw</span> <span class="token keyword">new</span> <span class="token class-name">DatabaseError</span><span class="token punctuation">(</span><span class="token string">"Failed to connect to database"</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>This helps differentiate between error types during debugging.</p>
</li>
<li>
<p><strong>Community Insights:</strong> An X post by ThePrimeagen (<a href="https://x.com/ThePrimeagen/status/1640721850094239744">Using JavaScript Properly</a>) highlights the importance of handling uncaught exceptions in Node.js using <code>process.on("uncaughtException")</code>, emphasizing the unpredictability of errors in complex systems.</p>
</li>
</ul>
<h4 id="error-handling-in-react">2. Error Handling in React</h4>
<p>React applications require robust error handling to prevent UI crashes and ensure a seamless user experience. Since React 16, error boundaries have been a key tool.</p>
<ul>
<li>
<p><strong>Error Boundaries:</strong> These are React components that catch JavaScript errors in their child component tree, log them, and display a fallback UI. Example:</p>
<pre class=" language-jsx"><code class="prism  language-jsx"><span class="token keyword">import</span> React<span class="token punctuation">,</span> <span class="token punctuation">{</span> Component <span class="token punctuation">}</span> <span class="token keyword">from</span> <span class="token string">'react'</span><span class="token punctuation">;</span>

<span class="token keyword">class</span> <span class="token class-name">ErrorBoundary</span> <span class="token keyword">extends</span> <span class="token class-name">Component</span> <span class="token punctuation">{</span>
  state <span class="token operator">=</span> <span class="token punctuation">{</span> hasError<span class="token punctuation">:</span> <span class="token boolean">false</span><span class="token punctuation">,</span> error<span class="token punctuation">:</span> <span class="token keyword">null</span> <span class="token punctuation">}</span><span class="token punctuation">;</span>

  <span class="token keyword">static</span> <span class="token function">getDerivedStateFromError</span><span class="token punctuation">(</span>error<span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">return</span> <span class="token punctuation">{</span> hasError<span class="token punctuation">:</span> <span class="token boolean">true</span><span class="token punctuation">,</span> error <span class="token punctuation">}</span><span class="token punctuation">;</span>
  <span class="token punctuation">}</span>

  <span class="token function">componentDidCatch</span><span class="token punctuation">(</span>error<span class="token punctuation">,</span> info<span class="token punctuation">)</span> <span class="token punctuation">{</span>
    console<span class="token punctuation">.</span><span class="token function">error</span><span class="token punctuation">(</span><span class="token string">"Error caught:"</span><span class="token punctuation">,</span> error<span class="token punctuation">,</span> info<span class="token punctuation">)</span><span class="token punctuation">;</span>
  <span class="token punctuation">}</span>

  <span class="token function">render</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token keyword">this</span><span class="token punctuation">.</span>state<span class="token punctuation">.</span>hasError<span class="token punctuation">)</span> <span class="token punctuation">{</span>
      <span class="token keyword">return</span> <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>h1</span><span class="token punctuation">&gt;</span></span>Something went wrong<span class="token punctuation">:</span> <span class="token punctuation">{</span><span class="token keyword">this</span><span class="token punctuation">.</span>state<span class="token punctuation">.</span>error<span class="token punctuation">.</span>message<span class="token punctuation">}</span><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>h1</span><span class="token punctuation">&gt;</span></span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    <span class="token keyword">return</span> <span class="token keyword">this</span><span class="token punctuation">.</span>props<span class="token punctuation">.</span>children<span class="token punctuation">;</span>
  <span class="token punctuation">}</span>
<span class="token punctuation">}</span>

<span class="token keyword">export</span> <span class="token keyword">default</span> ErrorBoundary<span class="token punctuation">;</span>
</code></pre>
<p>Wrap top-level components or specific widgets with this boundary to isolate errors (<a href="https://legacy.reactjs.org/docs/error-boundaries.html">React Error Boundaries</a>).</p>
</li>
<li>
<p><strong>Event Handlers:</strong> Error boundaries don’t catch errors in event handlers. Use try/catch instead:</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token function-variable function">handleClick</span> <span class="token operator">=</span> <span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
  <span class="token keyword">try</span> <span class="token punctuation">{</span>
    <span class="token comment">// Risky operation</span>
    <span class="token function">riskyOperation</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
  <span class="token punctuation">}</span> <span class="token keyword">catch</span> <span class="token punctuation">(</span><span class="token class-name">error</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    console<span class="token punctuation">.</span><span class="token function">error</span><span class="token punctuation">(</span><span class="token string">"Event handler error:"</span><span class="token punctuation">,</span> error<span class="token punctuation">.</span>message<span class="token punctuation">)</span><span class="token punctuation">;</span>
  <span class="token punctuation">}</span>
<span class="token punctuation">}</span><span class="token punctuation">;</span>
</code></pre>
</li>
<li>
<p><strong>Lifecycle Methods:</strong> Handle errors in lifecycle methods like <code>componentDidMount</code> using try/catch to prevent component failures.</p>
</li>
<li>
<p><strong>Community Insights:</strong> A YouTube video titled “Error Handling in React (Complete Tutorial)” by Cosden Solutions emphasizes the importance of error boundaries for component-level error management, providing practical examples for React developers.</p>
</li>
</ul>
<h4 id="error-handling-with-react-query">3. Error Handling with React Query</h4>
<p>React Query simplifies server-state management in React, offering robust error handling for API interactions.</p>
<ul>
<li>
<p><strong>Error States:</strong> Use the <code>isError</code> flag or <code>status === 'error'</code> to render error messages:</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">const</span> <span class="token punctuation">{</span> isError<span class="token punctuation">,</span> error<span class="token punctuation">,</span> data <span class="token punctuation">}</span> <span class="token operator">=</span> <span class="token function">useQuery</span><span class="token punctuation">(</span><span class="token string">'todos'</span><span class="token punctuation">,</span> fetchTodos<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token keyword">if</span> <span class="token punctuation">(</span>isError<span class="token punctuation">)</span> <span class="token keyword">return</span> <span class="token operator">&lt;</span>div<span class="token operator">&gt;</span>Error<span class="token punctuation">:</span> <span class="token punctuation">{</span>error<span class="token punctuation">.</span>message<span class="token punctuation">}</span><span class="token operator">&lt;</span><span class="token operator">/</span>div<span class="token operator">&gt;</span><span class="token punctuation">;</span>
</code></pre>
<p>This approach is straightforward but can lead to repetitive code in large applications.</p>
</li>
<li>
<p><strong>Error Boundaries Integration:</strong> Enable <code>throwOnError</code> to throw errors to the nearest error boundary:</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">const</span> queryClient <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">QueryClient</span><span class="token punctuation">(</span><span class="token punctuation">{</span>
  defaultOptions<span class="token punctuation">:</span> <span class="token punctuation">{</span>
    queries<span class="token punctuation">:</span> <span class="token punctuation">{</span>
      throwOnError<span class="token punctuation">:</span> <span class="token punctuation">(</span>error<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> error<span class="token punctuation">.</span>response<span class="token operator">?</span><span class="token punctuation">.</span>status <span class="token operator">&gt;=</span> <span class="token number">500</span><span class="token punctuation">,</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
  <span class="token punctuation">}</span><span class="token punctuation">,</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>This is useful for server errors (5xx) while handling client errors (4xx) locally (<a href="https://tkdodo.eu/blog/react-query-error-handling">React Query Error Handling</a>).</p>
</li>
<li>
<p><strong>Global Error Handling:</strong> Configure <code>QueryCache</code> for centralized error handling:</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">const</span> queryClient <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">QueryClient</span><span class="token punctuation">(</span><span class="token punctuation">{</span>
  queryCache<span class="token punctuation">:</span> <span class="token keyword">new</span> <span class="token class-name">QueryCache</span><span class="token punctuation">(</span><span class="token punctuation">{</span>
    onError<span class="token punctuation">:</span> <span class="token punctuation">(</span>error<span class="token punctuation">)</span> <span class="token operator">=&gt;</span> <span class="token punctuation">{</span>
      toast<span class="token punctuation">.</span><span class="token function">error</span><span class="token punctuation">(</span><span class="token template-string"><span class="token string">`Something went wrong: </span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>error<span class="token punctuation">.</span>message<span class="token interpolation-punctuation punctuation">}</span></span><span class="token string">`</span></span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span><span class="token punctuation">,</span>
  <span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">,</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>This ensures a single notification for errors, avoiding duplicates when multiple components use the same query.</p>
</li>
<li>
<p><strong>Community Insights:</strong> TkDodo’s blog post on React Query error handling highlights the importance of global callbacks to prevent redundant error notifications, a common issue in complex applications.</p>
</li>
</ul>
<h4 id="error-handling-in-typescript">4. Error Handling in TypeScript</h4>
<p>TypeScript’s type system enhances error handling by ensuring errors are predictable and well-defined.</p>
<ul>
<li>
<p><strong>Type-Safe Errors:</strong> Define custom error interfaces or classes:</p>
<pre class=" language-typescript"><code class="prism  language-typescript"><span class="token keyword">interface</span> <span class="token class-name">CustomError</span> <span class="token keyword">extends</span> <span class="token class-name">Error</span> <span class="token punctuation">{</span>
  code<span class="token punctuation">:</span> <span class="token keyword">string</span><span class="token punctuation">;</span>
  details<span class="token operator">?</span><span class="token punctuation">:</span> <span class="token keyword">any</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token keyword">class</span> <span class="token class-name">ApiError</span> <span class="token keyword">implements</span> <span class="token class-name">CustomError</span> <span class="token punctuation">{</span>
  name <span class="token operator">=</span> <span class="token string">'ApiError'</span><span class="token punctuation">;</span>
  <span class="token keyword">constructor</span><span class="token punctuation">(</span><span class="token keyword">public</span> message<span class="token punctuation">:</span> <span class="token keyword">string</span><span class="token punctuation">,</span> <span class="token keyword">public</span> code<span class="token punctuation">:</span> <span class="token keyword">string</span><span class="token punctuation">,</span> <span class="token keyword">public</span> details<span class="token operator">?</span><span class="token punctuation">:</span> <span class="token keyword">any</span><span class="token punctuation">)</span> <span class="token punctuation">{</span><span class="token punctuation">}</span>
<span class="token punctuation">}</span>

<span class="token keyword">throw</span> <span class="token keyword">new</span> <span class="token class-name">ApiError</span><span class="token punctuation">(</span><span class="token string">'API request failed'</span><span class="token punctuation">,</span> <span class="token string">'API_001'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
</code></pre>
<p>This ensures errors have specific properties, improving type safety.</p>
</li>
<li>
<p><strong>Functional Error Handling:</strong> Some developers advocate for Result types to avoid try/catch:</p>
<pre class=" language-typescript"><code class="prism  language-typescript"><span class="token keyword">type</span> Result<span class="token operator">&lt;</span>T<span class="token punctuation">,</span> E<span class="token operator">&gt;</span> <span class="token operator">=</span> <span class="token punctuation">{</span> success<span class="token punctuation">:</span> <span class="token keyword">true</span><span class="token punctuation">;</span> value<span class="token punctuation">:</span> T <span class="token punctuation">}</span> <span class="token operator">|</span> <span class="token punctuation">{</span> success<span class="token punctuation">:</span> <span class="token keyword">false</span><span class="token punctuation">;</span> error<span class="token punctuation">:</span> E <span class="token punctuation">}</span><span class="token punctuation">;</span>

<span class="token keyword">function</span> <span class="token function">fetchData</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">:</span> Result<span class="token operator">&lt;</span><span class="token keyword">string</span><span class="token punctuation">,</span> ApiError<span class="token operator">&gt;</span> <span class="token punctuation">{</span>
  <span class="token keyword">try</span> <span class="token punctuation">{</span>
    <span class="token keyword">return</span> <span class="token punctuation">{</span> success<span class="token punctuation">:</span> <span class="token keyword">true</span><span class="token punctuation">,</span> value<span class="token punctuation">:</span> <span class="token string">'Data'</span> <span class="token punctuation">}</span><span class="token punctuation">;</span>
  <span class="token punctuation">}</span> <span class="token keyword">catch</span> <span class="token punctuation">{</span>
    <span class="token keyword">return</span> <span class="token punctuation">{</span> success<span class="token punctuation">:</span> <span class="token keyword">false</span><span class="token punctuation">,</span> error<span class="token punctuation">:</span> <span class="token keyword">new</span> <span class="token class-name">ApiError</span><span class="token punctuation">(</span><span class="token string">'Failed'</span><span class="token punctuation">,</span> <span class="token string">'API_002'</span><span class="token punctuation">)</span> <span class="token punctuation">}</span><span class="token punctuation">;</span>
  <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
<p>This approach, discussed in a Codementor article (<a href="https://www.codementor.io/@supermacro/type-safe-error-handling-in-typescript-1bp40rs502">Type-Safe Error Handling</a>), reduces runtime errors but requires careful type management.</p>
</li>
<li>
<p><strong>Community Insights:</strong> A YouTube video titled “Try Catch Error Handling With TypeScript” emphasizes type-safe error handling, demonstrating how TypeScript’s type system can prevent common error-handling mistakes.</p>
</li>
</ul>
<h4 id="error-handling-in-sensitive-applications-1">5. Error Handling in Sensitive Applications</h4>
<p>Banking applications demand stringent error handling to protect sensitive data and maintain user trust.</p>
<ul>
<li>
<p><strong>Security First:</strong> Avoid exposing stack traces or detailed error messages to users, as these can reveal system vulnerabilities (<a href="https://owasp.org/www-community/Improper_Error_Handling">OWASP Improper Error Handling</a>). Use generic messages:</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token keyword">if</span> <span class="token punctuation">(</span>error<span class="token punctuation">)</span> <span class="token punctuation">{</span>
  <span class="token keyword">return</span> <span class="token operator">&lt;</span>div<span class="token operator">&gt;</span>Something went wrong<span class="token punctuation">.</span> Please contact support <span class="token keyword">with</span> code ERR<span class="token number">-001</span><span class="token punctuation">.</span><span class="token operator">&lt;</span><span class="token operator">/</span>div<span class="token operator">&gt;</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
</code></pre>
</li>
<li>
<p><strong>Secure Logging:</strong> Log errors to a secure backend system, excluding sensitive data like user credentials. Use tools like <a href="https://sentry.io/">Sentry</a> for detailed error tracking.</p>
</li>
<li>
<p><strong>Fail-Safe Mechanisms:</strong> Implement fallback states to prevent unauthorized access. For example, if a payment API fails, default to a “transaction declined” state rather than exposing partial data.</p>
</li>
<li>
<p><strong>User-Friendly Feedback:</strong> Provide clear, non-technical error messages with support codes for traceability. For instance, “Transaction failed. Please try again or contact support (Code: TXN-123).”</p>
</li>
<li>
<p><strong>Community Insights:</strong> Google’s engineering blog emphasizes raising errors early and logging error codes for debugging, critical for banking systems where traceability is essential (<a href="https://developers.google.com/tech-writing/error-messages/error-handling">Google Error Handling Rules</a>).</p>
</li>
</ul>
<h4 id="scalable-error-handling-solutions-1">6. Scalable Error Handling Solutions</h4>
<p>For large-scale applications, centralized and consistent error handling is key.</p>
<ul>
<li>
<p><strong>Error Reporting Services:</strong> Tools like <a href="https://sentry.io/">Sentry</a> or Rollbar provide centralized error tracking, aggregating errors across the application for analysis and alerting.</p>
</li>
<li>
<p><strong>Logging Frameworks:</strong> Implement a logging framework to capture error context, such as user actions or API responses. Ensure logs are stored securely and comply with regulations like GDPR for banking apps.</p>
</li>
<li>
<p><strong>Consistent Error Strategy:</strong> Define a standardized error response format for APIs:</p>
<pre class=" language-javascript"><code class="prism  language-javascript"><span class="token punctuation">{</span>
  error<span class="token punctuation">:</span> <span class="token punctuation">{</span>
    code<span class="token punctuation">:</span> <span class="token string">'ERR-001'</span><span class="token punctuation">,</span>
    message<span class="token punctuation">:</span> <span class="token string">'Invalid request'</span><span class="token punctuation">,</span>
    details<span class="token punctuation">:</span> <span class="token punctuation">{</span> field<span class="token punctuation">:</span> <span class="token string">'email'</span><span class="token punctuation">,</span> issue<span class="token punctuation">:</span> <span class="token string">'Invalid format'</span> <span class="token punctuation">}</span>
  <span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
<p>This format, recommended by the <a href="https://blog.postman.com/best-practices-for-api-error-handling/">Postman Blog</a>, ensures consistency across services.</p>
</li>
<li>
<p><strong>Global Handlers:</strong> Use React Query’s <code>QueryCache</code> or a global error boundary to handle errors uniformly, reducing code duplication and improving maintainability.</p>
</li>
</ul>
<h4 id="recommended-resources-1">7. Recommended Resources</h4>
<ul>
<li><strong>Books:</strong>
<ul>
<li><em>Eloquent JavaScript</em> by Marijn Haverbeke (<a href="https://eloquentjavascript.net/">Eloquent JavaScript</a>) covers error handling and bug fixing, suitable for general JavaScript knowledge.</li>
<li><em>JavaScript Error Handling</em> by Din Asotić (<a href="https://www.amazon.com/JavaScript-Handling-Elemental-Literature-Official/dp/B0BXMRB5Q3">Amazon</a>) focuses on error handling and security, ideal for in-depth study.</li>
</ul>
</li>
<li><strong>Articles and Documentation:</strong>
<ul>
<li><a href="https://legacy.reactjs.org/docs/error-boundaries.html">React Error Boundaries</a> provides official guidance on implementing error boundaries.</li>
<li><a href="https://tkdodo.eu/blog/react-query-error-handling">TkDodo’s React Query Error Handling</a> offers practical React Query error handling techniques.</li>
<li><a href="https://owasp.org/www-community/Improper_Error_Handling">OWASP Improper Error Handling</a> details security considerations for error handling.</li>
<li><a href="https://developers.google.com/tech-writing/error-messages/error-handling">Google Error Handling Rules</a> outlines general error handling principles.</li>
<li><a href="https://www.codementor.io/@supermacro/type-safe-error-handling-in-typescript-1bp40rs502">Type-Safe Error Handling in TypeScript</a> explores functional error handling approaches.</li>
</ul>
</li>
</ul>
<h4 id="example-implementation-for-a-banking-app">8. Example Implementation for a Banking App</h4>
<p>Below is an example of a React component for a banking transaction form, incorporating error handling best practices with React Query and TypeScript.</p>
<pre class=" language-tsx"><code class="prism  language-tsx">import React, { useState } from 'react';
import { useQuery, QueryClient, QueryCache } from 'react-query';
import toast from 'react-hot-toast';

// Define custom error type
interface TransactionError extends Error {
  code: string;
  details?: any;
}

// Configure global error handling
const queryClient = new QueryClient({
  queryCache: new QueryCache({
    onError: (error: TransactionError) =&gt; {
      toast.error(`Error ${error.code}: Please try again or contact support.`);
    },
  }),
});

// API call function
async function submitTransaction(amount: number): Promise&lt;string&gt; {
  const response = await fetch('/api/transaction', {
    method: 'POST',
    body: JSON.stringify({ amount }),
  });
  if (!response.ok) {
    const errorData = await response.json();
    throw new TransactionError(errorData.message, { name: 'TransactionError', code: errorData.code });
  }
  return response.json();
}

// Error Boundary Component
class TransactionErrorBoundary extends React.Component&lt;{}, { hasError: boolean; error: TransactionError | null }&gt; {
  state = { hasError: false, error: null };

  static getDerivedStateFromError(error: TransactionError) {
    return { hasError: true, error };
  }

  componentDidCatch(error: TransactionError, info: React.ErrorInfo) {
    console.error('Transaction error:', error, info);
  }

  render() {
    if (this.state.hasError) {
      return &lt;div&gt;Error {this.state.error?.code}: Transaction failed. Please contact support.&lt;/div&gt;;
    }
    return this.props.children;
  }
}

// Transaction Form Component
const TransactionForm: React.FC = () =&gt; {
  const [amount, setAmount] = useState&lt;number&gt;(0);

  const { isLoading, isError, error, mutate } = useQuery&lt;string, TransactionError&gt;(
    ['transaction', amount],
    () =&gt; submitTransaction(amount),
    { enabled: false, throwOnError: (err) =&gt; err.code.startsWith('5') } // Throw server errors to boundary
  );

  const handleSubmit = () =&gt; {
    try {
      mutate();
    } catch (err) {
      console.error('Submission error:', err);
    }
  };

  return (
    &lt;TransactionErrorBoundary&gt;
      &lt;div className="p-4"&gt;
        &lt;input
          type="number"
          value={amount}
          onChange={(e) =&gt; setAmount(Number(e.target.value))}
          className="border p-2"
        /&gt;
        &lt;button onClick={handleSubmit} disabled={isLoading} className="bg-blue-500 text-white p-2"&gt;
          {isLoading ? 'Processing...' : 'Submit Transaction'}
        &lt;/button&gt;
        {isError &amp;&amp; &lt;div className="text-red-500"&gt;Error: {error.message}&lt;/div&gt;}
      &lt;/div&gt;
    &lt;/TransactionErrorBoundary&gt;
  );
};

export default TransactionForm;
</code></pre>
<p>This example demonstrates:</p>
<ul>
<li><strong>TypeScript:</strong> Custom <code>TransactionError</code> type for type-safe error handling.</li>
<li><strong>React Query:</strong> Global error handling with <code>QueryCache</code> and <code>throwOnError</code> for server errors.</li>
<li><strong>React:</strong> Error boundary to catch rendering errors and display user-friendly messages.</li>
<li><strong>Security:</strong> Generic error messages with codes, avoiding sensitive data exposure.</li>
<li><strong>Scalability:</strong> Centralized error handling suitable for large-scale applications.</li>
</ul>
<h4 id="conclusion">9. Conclusion</h4>
<p>Effective error handling in JavaScript, React, React Query, and TypeScript is essential for building reliable and secure applications, especially in sensitive domains like banking. By using error boundaries, type-safe errors, global error handlers, and secure logging practices, developers can ensure stability, protect user data, and maintain a positive user experience. Scalable solutions like centralized error reporting and consistent error formats enable maintainability in large applications. Leveraging community insights and established resources ensures adherence to industry best practices.</p>
<p><strong>Key Citations:</strong></p>
<ul>
<li><a href="https://legacy.reactjs.org/docs/error-boundaries.html">React Documentation: Error Boundaries</a></li>
<li><a href="https://tkdodo.eu/blog/react-query-error-handling">TkDodo’s Blog: React Query Error Handling</a></li>
<li><a href="https://owasp.org/www-community/Improper_Error_Handling">OWASP: Improper Error Handling</a></li>
<li><a href="https://developers.google.com/tech-writing/error-messages/error-handling">Google Developers: General Error Handling Rules</a></li>
<li><a href="https://eloquentjavascript.net/">Eloquent JavaScript by Marijn Haverbeke</a></li>
<li><a href="https://www.amazon.com/JavaScript-Handling-Elemental-Literature-Official/dp/B0BXMRB5Q3">JavaScript Error Handling by Din Asotić</a></li>
<li><a href="https://sentry.io/">Sentry: Error Monitoring Platform</a></li>
<li><a href="https://blog.postman.com/best-practices-for-api-error-handling/">Postman Blog: Best Practices for API Error Handling</a></li>
<li><a href="https://www.codementor.io/@supermacro/type-safe-error-handling-in-typescript-1bp40rs502">Codementor: Type-Safe Error Handling in TypeScript</a></li>
<li><a href="https://x.com/ThePrimeagen/status/1640721850094239744">ThePrimeagen: Using JavaScript Properly</a></li>
</ul>

