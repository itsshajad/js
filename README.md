# 🧠 JavaScript Interview Questions

---

<details>
<summary><strong>Q1. What is a Polyfill in JavaScript?</strong></summary>

**Answer:**  
A *polyfill* is a piece of code (usually JavaScript) that provides modern functionality on older browsers that do not natively support it. It essentially "fills in" the gap for missing features.

</details>

---

<details>
<summary><strong>Q2. What is <code>prototype</code> and <code>__proto__</code>?</strong></summary>

**Answer:**  
- **`prototype`** is a property of constructor functions. It allows you to define methods and properties that should be shared by all instances created from that constructor. It's commonly used for inheritance and polyfills.
- **`__proto__`** is a reference to the object’s prototype (i.e., the value of the constructor’s `prototype` property). It’s used internally by JavaScript for the prototype chain lookup.

</details>

---

<details>
<summary><strong>Q3. What are <code>call</code>, <code>apply</code>, and <code>bind</code>?</strong></summary>

**Answer:**  
These methods allow you to explicitly set the value of `this` inside a function.

- **`call`**: Calls a function with a specified `this` and individual arguments.  
  `fn.call(context, arg1, arg2)`
- **`apply`**: Similar to `call`, but takes arguments as an array.  
  `fn.apply(context, [arg1, arg2])`
- **`bind`**: Returns a new function with `this` permanently set to the specified context.  
  Useful for callbacks and event handlers.

</details>

---

<details>
<summary><strong>Q4. What is a Closure?</strong></summary>

**Answer:**  
A *closure* when a function written inside another function and inner function has access of its outer function variables even after the execution context is finish.
it is useful for remembering data and keeping things private.
</details>

---

<details>
<summary><strong>Q5. What is Recursion?</strong></summary>

**Answer:**  
Recursion is technique whera a function call itself to solve problem. It helps simplify complex problems by breaking them down into simpler ones.
</details>

---

<details>
<summary><strong>Q6. What is <code>async</code> / <code>await</code>?</strong></summary>

**Answer:**  
`async` and `await` are syntactic sugar over Promises to make asynchronous code look and behave more like synchronous code, improving readability and error handling.

</details>

---

<details>
<summary><strong>Q7. What are Callbacks and Callback Hell?</strong></summary>

**Answer:**  
- A *callback* is a function passed as an argument to another function to execute after some operation is complete.
- *Callback hell* occurs when multiple nested callbacks make code hard to read and maintain, forming a "pyramid of doom."

</details>

---

<details>
<summary><strong>Q8. What is Debouncing and Throttling?</strong></summary>

**Answer:**  
These are optimization techniques to control the rate of function execution.

- **Debouncing**: Delays execution until after a pause in events (like typing).
- **Throttling**: Ensures a function runs at most once in a defined interval, regardless of how many events occur.

</details>

---

<details>
<summary><strong>Q9. What is Event Delegation?</strong></summary>

**Answer:**  
Event delegation is a technique where you add a single event listener to a parent element to handle events on its child elements. This is done using event bubbling and the `event.target` property.

</details>

---

<details>
<summary><strong>Q10. What is <code>event.preventDefault()</code>?</strong></summary>

**Answer:**  
The `event.preventDefault()` method prevents the default action associated with an event (like stopping a form from submitting or a link from navigating).

</details>

---

<details>
<summary><strong>Q11. What is the difference between Shallow Copy and Deep Copy?</strong></summary>

**Answer:**

- **Shallow Copy**: Copies only the first level of the object. Nested objects remain as references.
  
  Example:
  ```js
  const obj1 = {
    name: 'Shajad',
    address: {
      email: 'shajadsheikh32@gmail.com',
      location: 'Mumbai'
    }
  };

  const obj2 = { ...obj1 };
  obj2.name = 'Sheikh';
  obj2.address.location = 'Delhi';

  console.log(obj1); // Location will be 'Delhi' due to shared reference
