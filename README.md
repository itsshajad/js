# 🧠 JavaScript Interview Questions
<details><summary><strong>Q - What is Promise in JavaScript</strong></summary>
Promise is built in javascript object and it is used to make asynchrounous operation.
It has three state
 
 <code>pending</code>
 <code>fulfilled</code>
 <code>rejected</code>
 <h3>Basic Syntax</h3>

 ```js
 const myPromise = new Promise((resolve, reject) => {
  // do some async work
  if(success){
    resolve('resolved');
  }
  else {
    reject('rejected')
  }
 })

//  consume a promise
myPromise.then((cb) => console.log(cb)).catch((error) => console.log(error))
 ```

 **Promises Method**

```Promise.resolve``` Creates a Promise that resolves with a given value. 

```Promise.reject``` Creates a Promise that rejects with a given error.

```Promise.all``` Run multiple Promises in parallel and waits for all to succeed. if any fails it will reject.

```js
const api1 = fetch('https://jsonplaceholder.typicode.com/todos/1').then((res) =>
  res.json()
);
const api2 = fetch('https://jsonplaceholder.typicode.com/todos/2').then((res) =>
  res.json()
);
  
  Promise.all([api1, api2])
  .then((res) => console.log(res))
  .catch((error) => console.log(error));
```

```Promise.allSetteled``` Run multiple Promises in parallel but waits for all to finish whether fullfilled or rejected.

```js
const api1 = fetch('https://jsonplaceholder.typicode.com/todos/1').then((res) =>
  res.json()
);
const api2 = fetch('https://jsonplaceholder.typicode.com/todos/2').then((res) =>
  res.json()
);
  
  Promise.allSettled([api1, api2])
  .then((res) => console.log(res))
  .catch((error) => console.log(error));
```

```Promise.race``` Return the result of first promise either either resolved or rejected

```js
const api1 = fetch('https://jsonplaceholder.typicode.com/todos/1').then((res) =>
  res.json()
);
const api2 = fetch('https://jsonplaceholder.typicode.com/todos/2').then((res) =>
  res.json()
);
  
  Promise.race([api1, api2])
  .then((res) => console.log(res))
  .catch((error) => console.log(error));
```
 
```Promise.any``` Return the result of first fulfilled promise. ingnore rejections unless all fail.
```js
const api1 = fetch('https://jsonplaceholder.typicode.com/todos/1').then((res) =>
  res.json()
);
const api2 = fetch('https://jsonplaceholder.typicode.com/todos/2').then((res) =>
  res.json()
);
  
  Promise.any([api1, api2])
  .then((res) => console.log(res))
  .catch((error) => console.log(error));
```
 
</details>

---

<details>
<summary><strong>Q - What is <code>async</code> / <code>await</code>?</strong></summary>

**Answer:**  
`async` and `await` make working with Promises easier. They let you write async code that looks like regular synchrounous code. which makes it easier to read and handle errors. 

</details>

---

<details><summary><strong>Q - App route and page route</strong></summary>
<strong>Answer:</strong> <br />
<code>App route</code> introduce in Next.js 13+ based on <code>/app</code> <strong>directory</strong> uses React server components by default and its has feature like group route (folder) without affecting routing and private route _folder it will opt the folder and all child segment out of routing. nested route folder/folder

- uses file-based routing with special files.
- layout.js
- template.js
- error.js (React error boundary)
- loading.js (React suspense boundary)
- not-found.js (React error boundary)
- page.js or nested layout.js

<code>Page route</code> exits since initial based on <code>/page</code> directory uses  only client component simple structure: each file become route.
</details>

---

<details><summary><strong>Q - Middleware</strong></summary>
<strong>Answer:</strong>
Middleware is a function that acts as a bridge between request and response.
it is used to process modify, or log requests/responses before they reach the final handler or after the response is sent. <br />
<code>Redux</code> middleware allow you to intercept action before they reach reducer.<br />

```js
const logger = store => next => action => {
  console.log("Dispatching:", action);
  return next(action); // pass it to the next middleware or reducer
};

```
<code>NextJs</code> nextjs middleware runs before a request is completed, allowing logic like: Redirect Authentication checks Geo/blocking logic

```js
// middleware.ts
import { NextResponse } from 'next/server';

export function middleware(request) {
  const loggedIn = checkAuth(request);
  if (!loggedIn) {
    return NextResponse.redirect(new URL('/login', request.url));
  }
  return NextResponse.next();
}
```
</details>

---

<details>
<summary><strong>Q - Different between <code>undefined</code> and <code>null</code></strong></summary>
<strong>Answer:</strong>

<code>undefined</code>
Means the variable has been declared but not assigned a value. Set by javascript automatically. 
data type is primitive <code>typeof undefined is 'undefined'</code>

<code>null</code>
Means the value is null is forcefully set by developer
</details>

---

<details><summary><strong>Q - Different between type never and unknown</strong></summary>
  <strong>Answer</strong>
  type never is used when the value will never occur
  function that never return 
  ex - 

  ```js
  function throwError():never{
    throw new Error('Something went wrong')
  }

  OR
   
  // infinite loop
  function loop():never{
    while(true){
      console.log('hi')
    }
  }
  ```
  <code>type unknown</code> means that the type of value is unknown
  but we can make a check on it
  let say

  ```js
    function getUserId(value: unknown) {
      if (typeof value === 'string') {
        // value is now known to be a string
        console.log(value.toUpperCase());
      } else {
        console.log('Unknown type');
      }
    }
  ```
</details>

---

<details>
  <summary><strong>Q - What is static type and dynamic type in typescript</strong></summary>
  <strong>Answer:</strong>

  <code>Static type</code>  Static type mean types are checked at compile time not at runtime.
  ex - 

  ```js
  const username: string = 'shajad';
  username = 40; //❌ Error: Type 'number' is not assignable to type 'string'
  ```

  <code>Dynamic type</code> Dynamic type means that the type can change or it's <strong>not strictly enforced.</strong> in typescript this is typically done using: <code>any, unknown</code>
  
</details>

---

<details>
<summary><strong>Q - NextJs rendering <code>(SSG, CSR, SSR, ISR)</code></strong></summary>
<strong>
  Answer
</strong>

  Next js is by default SSG for pages that don't require external data. If a page needs to fetch data at runtime then server side rendering (SSR) is used.

  Next js provdes multiple rendering strategies depending on the page's data fetching needs.
  <code>SSG</code>: static site generation pages are generated at build time. and served as static HTML <br />
  pros - Fast loading, seo friendly, good for blogs marking pages. benefits for prerendering data and for seo like blogs etc.<br />
  cons - data is stale until you redeploy.

```js
export async function getStaticProps() {
  const res = await fetch('https://api.example.com/data');
  const data = await res.json();

  return {
    props: { data },
  };
}
```

<code>SSR</code>: Pages are render on server on request time.

pros - Always upto date data, good for dynamic content. <br />
cons - Slower performance compared to static. relies on server availability.

```js
export async function getServerSideProps() {
  const res = await fetch('https://api.example.com/data');
  const data = await res.json();

  return {
    props: { data },
  };
}
```
<code>CSR</code> client side rendering by default react application is client side initially client side is initially empty it will go to page when we request the page code build on client side and served

pros - Light initial load, full control on client.
const - Bad for SEO, slower performance

```js
import { useEffect, useState } from 'react';

function Page() {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch('/api/data')
      .then((res) => res.json())
      .then(setData);
  }, []);

  return <div>{data ? JSON.stringify(data) : 'Loading...'}</div>;
}
```
<code>ISR</code> Works like SSG but allows pages to be revalidate on a time interval without a full redeploy.

pros - Best of both SSG and SSR; fresh data without rebuild. <br />
cons - Slightly more complex caching strategy

```js
export async function getStaticProps() {
  const res = await fetch('https://api.example.com/data');
  const data = await res.json();

  return {
    props: { data },
    revalidate: 60, // Regenerate every 60 seconds
  };
}
```

</details>

---

<details>
  <summary><strong>Q - usePrevious pattern</strong></summary>
<strong>Answer:</strong>
  usePrevious pattern is a technique in react used to store previous value
  so that we can clear use later ex- clearing user id getting previous value

  ```js

const usePrevious = (count: number) => {
    const ref = useRef<number>(0);
    useEffect(() => {
        ref.current = count;
    }, [count]);

    return ref.current;
}

const Counter = () => {
    const [count, setCount] = useState(0);
    const previousValue = usePrevious(count);

    return (
        <div>
            <p>{previousValue} : {count}</p>
            <button onClick={() => setCount((prev) => prev + 1)}>Click</button>
        </div>
    )
}
  ```
</details>

---

<details>
<summary><strong>Q - Flatten Array</strong></summary>
<strong>Answer:</strong>

convert a multi-dimensional array into single dimensional array

```js
const arr = [2,3,5,[3,2],2,[5,[10,11,[20]]]];

// js inbuild method
const result = arr.flat(Infinity);
console.log(result);
// [2, 3, 5, 3, 2, 2, 5, 10, 11, 20];

// custom 
const flattenArray = (arr) => {
  let result = [];
  for(i of arr){
    if(Array.isArray(i)){
     result =  result.concat(flattenArray(i));
    }
    else {
      result.push(i)
    }
  }
  return result;
}
console.log(flattenArray(arr));
// [2, 3, 5, 3, 2, 2, 5, 10, 11, 20]


// using reduce and recursion
const flattenArray = (arr) => {
 return arr.reduce((acc, curr) => Array.isArray(curr) ?  acc.concat(flattenArray(curr)) : acc.concat(curr), [])
}
console.log(flattenArray(arr));
// [2, 3, 5, 3, 2, 2, 5, 10, 11, 20]
```
</details>

---

<details>
<summary><strong>Q - Intersection observer</strong></summary>
**Answer:**
 Intersection observer api is a web browser native feature designed to track the visibility of element in the viewport its lightweight efficient and run outside the main thread meaning no performance hits from expensive scroll events.

<strong>Use case</strong>
  Lazy loading image
  infinite scroll and scroll triggered effects etc.


```js
EX --
  // take two parameters callback and option
  const observer = new IntersectionObserver((entry) => {
  // entry will be always in array
  entry.forEach((item) => {
    if(item.isIntersecting){
      // add logic
    }
  }) 
  }, {
    threshold: 1; // value from 0 to 1 0 is by default 1 if the element visibile 100% on viewport 0 if the element visibile 1px in the viewport
    root: "", // is it used to set the root of viewport by default it is root viewport means html and we can set to any container ex - document.querySelector('.card-container)
    rootMargin: "100px", // root margin is use to set margin negative or positive it is helpful calling the api before we reached to element.
  });

  // now observe the element
  const cards = document.querySelectorAll('.card');
  observer.observe(cards);
```
</details>

---

<details>
<summary><strong>Q. What is a Polyfill in JavaScript?</strong></summary>

**Answer:**  
A *polyfill* is a piece of code (usually JavaScript) that provides modern functionality on older browsers that do not natively support it. It essentially "fills in" the gap for missing features.

</details>

---

<details>
<summary><strong>Q. What is <code>prototype</code> and <code>__proto__</code>?</strong></summary>

**Answer:**  
- **`prototype`** is a property of constructor functions. It allows you to define methods and properties that should be shared by all instances created from that constructor. It's commonly used for inheritance and polyfills.
- **`__proto__`** is a reference to the object’s prototype (i.e., the value of the constructor’s `prototype` property). It’s used internally by JavaScript for the prototype chain lookup.

</details>

---

<details>
<summary><strong>Q. What are <code>call</code>, <code>apply</code>, and <code>bind</code>?</strong></summary>

**Answer:**  
These are the methods in javascript is used to set this manually inside function

- **`call`**: call the function immediately with custom this.

- accepts two arguments
- **`first`** is thisArrg
- **`second`** is restArg

work on normal function only not arrow function

```js
EX --
function callFunction() {
 console.log(`${message}, my name is ${this.name}`);
}
const person = {name:'shajad'};
callFunction.call(person)
```


- **`apply`**: Similar to `call`, but takes arguments as an array.  
  `fn.apply(context, [arg1, arg2])`

```js 
function bindFunction(msg) {
  console.log(`My name is ${this.name} my age is ${this.age} and i ${msg.map((val) => val)}`)
}
const person = {name:'Shajad', age: 26}
bindFunction.apply(person, ['love', 'you'])
```

- **`bind`**: Does not call function immediately 
  Returns a new function with `this` value.  
  Useful for callbacks and event handlers.

```js
function bindFunction(msg) {
  console.log(`${msg} is my ${this.role}`)
}

const bindFunction('shajad', role = 'hero')
```

</details>

---

<details>
<summary><strong>Q. What is a Closure?</strong></summary>

**Answer:**  
A *closure* when a function written inside another function and inner function has access of its outer function variables even after the execution context is finish.
it is useful for remembering data and keeping things private.
</details>

---

<details>
<summary><strong>Q. What is Recursion?</strong></summary>

**Answer:**  
Recursion is technique whera a function call itself to solve problem. It helps simplify complex problems by breaking them down into simpler ones.
</details>

---

<details>
<summary><strong>Q. What are Callbacks and Callback Hell?</strong></summary>

**Answer:**  
- A *callback* is a function passed as an argument to another function to execute after some operation is complete.
- *Callback hell* occurs when multiple nested callbacks make code hard to read and maintain, forming a "pyramid of doom."

</details>

---

<details>
<summary><strong>Q. What is Debouncing and Throttling?</strong></summary>

**Answer:**  
These are optimization techniques to control the rate of function execution.

- **Debouncing**: Delays execution until after a pause in events (like typing).
- **Throttling**: Ensures a function runs at most once in a defined interval, regardless of how many events occur.

</details>

---

<details>
<summary><strong>Q. What is Event Delegation?</strong></summary>

**Answer:**  
Event delegation is a technique where you add a single event listener to a parent element to handle events on its child elements. This is done using event bubbling and the `event.target` property.

</details>

---

<details>
<summary><strong>Q. What is <code>event.preventDefault()</code>?</strong></summary>

**Answer:**  
The `event.preventDefault()` method prevents the default action associated with an event (like stopping a form from submitting or a link from navigating).

</details>

---

<details>
<summary><strong>Q. What is the difference between Shallow Copy and Deep Copy?</strong></summary>

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

- **Deep Copy**: Copies all level of nested objects. <br />

  Ways of deepclone

  ```js
  // built in modern browser and Nodejs 17+
  const obj2 = structuredClone(obj1);
  obj2.address.location = 'Delhi';
  console.log(obj1) // Location remain the same as mumbai for obj1
  console.log(obj2) // Location is now changed to Delhi because we have changed the value in obj2

  // using JSON.stringify

  const obj2 = JSON.parse(JSON.stringify(obj));
  // custom method of array
  
  function deepClone(obj){
    if(obj === null || typeof obj !== 'object'){
      return obj;
    }

    if(obj instanceof Date){
      return new Date(obj);
    }

    if(Array.isArray(obj)){
      return obj.map((val) => deepClone(val))
    }

    const result = {};
    for(const key in obj) {
      if(obj.hasOwnProperty(key)){
        result[key] = deepClone(obj[key])
      }
    }

    return result;

  }

  const obj2 = deepClone(obj1)
  
  ```
</details>

---

<details>
  <summary><strong>Q - Async defer in script tag</strong></summary>
  <strong>Answer</strong>
  
  Async defer is asynchrounously called the javascript file 
  but there is a different between them

  <code>async</code> attribute is used to call asynchrounously and dons'nt block the main thread it will execute when its ready

  <code>defer</code> attribute is also used to call asynchrounously and doesn't block the main the thread but it will excute only once the html parsing finish
</details>
