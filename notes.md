# JavaScript Questions & Answers

### Q1: What is Hoisting ?

Hoisting JavaScript ka behavior hai jisme variables aur functions ki declarations code run hone se pehle hi memory mein upar register ho jaati hain. Is wajah se kabhi kabhi unhe declaration se pehle bhi access kiya ja sakta hai.

```
console.log(a);
var a = 5;
```

Yahan:
a exist karta hai ✅
Lekin value abhi assign nahi hui ❌
Isliye output aata hai: undefined

### Q2: Closures kya hote hain?

- ✅ Jab ek function doosre function ke andar define hota hai
- ✅ Aur andar wala function bahar wale function ke variables ko access kar sakta hai
- ✅ Aur phir bahar wala function return kar diya jaye
- ✅ Tab closure banta hai

**Example:**

```javascript
function outerFunction(outerVariable) {
  return function innerFunction(innerVariable) {
    console.log(`Outer: ${outerVariable}`);
    console.log(`Inner: ${innerVariable}`);
  };
}
const newFunction = outerFunction("Hello");
newFunction("World");
```

### Q3: Closure Kyun Useful Hai?

- ✅ **Functional Programming** – Higher-order functions mein kaam aata hai
- ✅ **Event Handlers** – Callbacks mein bahut useful hota hai
- ✅ **Data Privacy** – Variables ko private rakhne ke liye use hota hai

### Q4: `this` kya hota hai?

`this` ka matlab hota hai: **"yeh wala object"**.
Matlab jis object ke andar function kaam kar raha hai, `this` us object ko point karta hai.

### Q5: Explicit Binding (call, apply, bind) mein kya farq hai?

- **call()** → Function ko abhi aur isi waqt chalao.
- **apply()** → Function ko abhi chalao (lekin arguments array ke saath bhejo).
- **bind()** → Function ko baad mein chalane ke liye ready karke ek naya function return karo.

### Q6: Lexical Scope kya hota hai?

Lexical scope mein function ko wahi variables milte hain:

1. Jo uske andar hain.
2. Ya uske outer (parent) scope mein hain.
   _Wo sibling function ke variables access nahi kar sakta._

> **Simple Example:** Har function ek room hai. Room apne ghar (parent scope) ki cheezen dekh sakta hai, lekin doosre room ki private cheezen nahi dekh sakta.

### Q7: Arrow function mein `this` kaise behave karta hai?

Regular function apna `this` khud banata hai, jo kabhi kabhi global object (`window`) ban jata hai aur `this.count` undefined ho sakta hai.
Lekin **Arrow function** ka apna `this` nahi hota, wo apne parent scope se `this` udhaar (inherit) leta hai.

### Q8: Loops mein farq (for...in, for...of, forEach)?

- 🔹 **for...in** -> Object ki **keys** (properties) iterate karta hai.
- 🔹 **for...of** -> **Values** iterate karta hai (arrays, strings, etc.)
- 🔹 **forEach()** -> Simple array loop ke liye best hai.
- 🔹 **for (simple)** -> Jab aapko loop par full control chahiye.

### Q9: Async/Await (Sequential vs Parallel)?

- **Sequential loop:** Start → wait → start → wait (Ek ke baad ek chalta hai, time zyada lagta hai).
- **Parallel (Promise.all):** Saare tasks ek saath start hote hain aur sabka wait ek saath hota hai (Fast hota hai).

### Q10: Why is `await` in a loop bad?

**Strong answer:** Kyunki ye **sequential execution (waterfall pattern)** banata hai, jis se total time badh jata hai. Independent async operations ko hamesha `Promise.all` se parallel chalana chahiye taki I/O concurrency badh sake. Sequential sirf tab use karein jab agla step pehle step ke result par depend karta ho.

### Q11: Async/Await Kya Hai?

Async/await JavaScript ka ek tareeqa hai jis se hum time lene wale kaam (jaise API call, file read) ko asaani se handle karte hain. Ye Promise-based code ko likhne ka ek saaf aur readable (synchronous-looking) tareeqa hai.

### Q12: Promise kya hota hai?

Iska matlab hai: "Kaam background mein karo, jab ready ho jaye to mujhe bata dena."

### Q13: Kya Promise ek hi baar settle hota hai?

Ji haan, Promise sirf ek baar final state mein ja sakta hai:

1. Ya **fulfilled** (resolve)
2. Ya **rejected** (reject)
   Ek baar settle ho gaya → phir kabhi change nahi hota.

### Q14: Async/await vs Promise?

Async/await bas Promise ko likhne ka ek **easy style (Syntactic Sugar)** hai. Andar se ye aaj bhi Promise hi use karta hai.

### Q15: Callback Hell Kya Hai?

Jab multiple async tasks ek ke baad ek execute karne hote hain, to code itna deeply nested ho jata hai ki wo triangle jaisa dikhne lagta hai. Isse "Pyramid of Doo
m" bhi kehte hain.

### Q16: Callback hell ko kaise avoid karte ho?

Promises ya Async/Await ka use karke. Async/await sabse clean aur readable approach hai.

### Q17: Hooks?

Hooks are special functions in React that let functional components use state and lifecycle features without writing classes.

useEffect – useEffect React ka hook hai jo component render hone ke baad extra kaam karne ke liye use hota hai. Jaise API call karna, data fetch karna, ya koi action perform karna.
useState – Component ka state manage karne ke liye
useContext – React context ka data access karna bina props drilling ke.
useRef – DOM element ka reference store karna – jaise input field ya div ko directly access karna.
Mutable value store karna jo component ke re-render ke beech change ho sakti hai, bina component ko re-render karwaye.

### Q18: Mutable & Immutable?

Mutable – Directly change karte ho – Nahi (re-render nahi hota) – useRef
Immutable – Naya copy banate ho – Haan (React automatically re-render karta hai) – useState

### Q19: what is state vs props ?

State: Component ka apna internal data jo change ho sakta hai aur component ko re-render karta hai.
Props: Props are data passed from parent to child component. They are read-only and cannot be modified by the child.

### Q20: what is optimize performance ?

Apni application ko fast aur efficient banana, taake woh kam resources use kare aur user experience smooth ho.

useCallback: Functions ko memorize karta hai, unnecessary recreation avoid karta hai.
useMemo: Heavy calculations ko cache karta hai, tabhi re-compute karta hai jab dependencies change ho.
Lazy Loading: React app ko chote chunks mein tod do, aur components ko tabhi load karo jab user unhe dekhe.

### Q21: what is Redux ?

Redux is a state management library for JavaScript apps (commonly React).
It helps manage app-wide state in a single central place, so multiple components can share data easily without prop-drilling.

App ke root me bnti ha iski file.

### Q22: what is DOM vs virtual DOM ?

DOM (Document Object Model) is the real structure of your webpage in the browser.
Jab bhi HTML load hoti hai, browser uska ek tree bana deta hai jise DOM kehte hain.

Virtual DOM ek lightweight copy hoti hai real DOM ki.
React pehle changes Virtual DOM mein karta hai, phir compare (diff) karta hai old aur new version ko, aur sirf jo part change hua hai wahi real DOM mein update karta hai.

### Q23: what is useEffect ?

useEffect React ka hook hai jo component render hone ke baad extra kaam karne ke liye use hota hai. Jaise API call karna, data fetch karna, ya koi action perform karna.

### Q24: how to manage state ?

In React, we manage state using useState for local component state and tools like Context API or Redux for global state management.

### Q25: what is component lifecycle ?

Component lifecycle refers to the different phases of a React component: mounting, updating, and unmounting. These stages determine when a component is created, updated, and removed from the DOM.

### Q26: What is Pure Component?

A Pure Component is a component that re-renders only when its props or state actually change.
export default React.memo(MyComponent);

### Q27: how virtual dom works?

Virtual DOM React ki ek lightweight copy hoti hai real DOM ki, jo memory mein hoti hai.
React pehle changes Virtual DOM mein karta hai, phir sirf jo part change hua hai woh real DOM mein update karta hai.

### Next Js

### Q28: how routing works (page and app routing) ?

### Page Routing (Traditional / MPA Concept)

Har URL pe new page load hota hai.
Browser server se naya HTML request karta hai.
Poora page reload hota hai.

### App Routing (SPA – React Style)

Sirf URL change hota hai, page reload nahi hota.
React background mein component change karta hai.
Faster user experience milta hai.

### Q29: SSG – Static Site Generation ?

Static Site Generation (SSG) ek technique hai jisme website ke pages pehle se (build time par) HTML files me generate kar diye jate hain — jab user request kare, toh server bas ready-made HTML file bhej deta hai.

🔎 SEO kaise improve karta hai?

Search engine ko ready-made HTML milta hai.
Crawl karna easy hota hai (JavaScript execute karne ki zarurat kam).
Page load fast hota hai → Core Web Vitals improve → ranking better.
Server load kam → performance stable.

Problem:
Page build-time pe generate hota hai → agar content change ho jaye, to site ko poora rebuild karna padta ha

### Q30: CSR – Client Side Rendering ?

Isme page ka content browser khud banata hai using JavaScript. Matlab server mostly empty HTML bhejta hai, aur page user ke browser me load hote-hote dikhta hai. Ye fast hota hai interaction ke liye, lekin initial load slow ho sakta hai aur SEO ke liye thoda weak hai.

### Q31: SSR (Server Side Rendering) ?

Isme server page ko ready HTML me generate karke bhejta hai. Matlab user ko turant content dikhai deta hai. Ye fast hota hai first load me aur SEO friendly hai, lekin server pe zyada load hota hai.

🔎 SEO kaise improve karta hai?

Dynamic content bhi fully rendered HTML me milta hai.
Search engines ko complete content instantly mil jata hai.
Meta tags (title, description) har page ke liye dynamically set ho sakte hain.
Social sharing (OG tags) properly work karte hain.

Problem:
Page har request pe generate hota hai → server pe load zyada hota hai.

### Q32: Next vs react ?

🔹 React: React ek JavaScript library hai jo UI banane ke liye use hoti hai.

Sirf frontend UI handle karta hai
Routing ke liye alag se library chahiye (jaise React Router)
By default Client-Side Rendering (CSR) karta hai
SEO handling manually karni padti hai

🔹 Next.js

Next.js React ke upar bana hua ek framework hai jo extra features provide karta hai.

Built-in routing system
Server-Side Rendering (SSR) support
Static Site Generation (SSG)
Better SEO
API routes bhi bana sakte ho

### Q33: why we use Next.js over react ?

Next.js is used over React for better SEO, built-in routing, performance optimization, and fullstack capabilities like API routes.

### Q34: What is ISR? ?

Static pages ko build-time pe generate karna, aur unhe runtime pe periodically update karna — bina poore site ko rebuild kiye.

Advantages:
Fast Performance
SEO Friendly
Scalable

🔎 SEO kaise improve karta hai?

Fast performance (jaise SSG)
Updated content (jaise SSR)
Google ko hamesha relatively fresh content milta hai
Rebuild ke liye pura site deploy karne ki zarurat nahi

export async function getStaticProps() {
const data = await fetch('https://api.example.com/posts').then(res => res.json());

return {
props: { posts: data },
revalidate: 60, // ISR: page will regenerate at most once every 60 seconds
};
}

🔹 Node.js

### Q35: What is Event Loop Node.js ?

Node.js ka event loop ek mechanism hai jo asynchronous operations ko handle karta hai.
Ye call stack aur callback queue ko monitor karta hai.
Jab call stack empty hota hai to event loop queue se callback utha kar execute karta hai.

```
console.log("Start");
setTimeout(() => {
  console.log("Hello");
}, 2000);
console.log("End");

Start
End
Hello
```

### Q36: what is request and response cycle ?

The Request–Response Cycle is the basic communication process between a client. When you open a website:
Client sends a Request → “Mujhe yeh page chahiye.”
Server processes the request
Server sends a Response → “Yeh lo tumhara page/data.”

### Q37: What are Microtasks and Macrotasks?

Macrotasks: Ye tasks event loop ke next iteration me execute hote hain. Examples: setTimeout, setInterval
Microtasks: Ye tasks current code ke baad, macrotasks se pehle execute hote hain. Examples: Promise.then

### Q38: How nodejs works ?

Node.js ek JavaScript runtime hai jo browser ke bahar JS run karne deta hai.
Single-threaded hai, lekin non-blocking I/O ki wajah se bohot saari requests ek saath handle kar sakta hai.

### Q39: How nodejs works (libuv library) ?

Modules Node.js ka ek reusable code ka part hain.
Har file ek module hoti hai, jisme functions, objects, ya variables ho sakte hain.
Require / Export se use kiya jata hai.

Libuv Node.js ka engine ka assistant hai jo heavy kaam background me handle karta hai aur main thread free rakhta hai.
Ye thread pool aur event loop manage karta hai.
Default 4 threads (configurable)

### Q40: Clustering kya hai?

Node.js single-threaded hai, matlab ek time pe ek thread main code run karta hai.
Agar CPU-heavy tasks ya multiple cores ko use karna ho, to clustering use hota hai.

### Q41: Node.js aur Threads?

Node.js single-threaded hota hai main JavaScript execution ke liye.
Matlab ek time pe ek hi thread main code execute hota hai.
Lekin, asynchronous I/O aur heavy tasks ke liye Node.js internally threads use karta hai via Libuv thread pool.

### Q42: How you know how much testcases are needed?

Node.js mein test cases likhne ke liye pehle Jest ya Mocha install karte hain. Phir apni function ke liye test file banate hain jahan check karte hain ke function sahi result de raha hai ya nahi, aur npm test chala kar tests run karte hain.

### Q43: How you know how much testcases are needed?

Test cases har function ke liye banaye jaate hain: normal input, edge cases, aur galat input ke liye. Important ya complex code ke liye thode extra tests bhi likh sakte hain

### Q44: what is middleware and how it works?

Middleware ek function hota hai jo request aur response ke beech kaam karta hai Node.js (usually Express.js) applications mein. Simple lafzon mein: ye ek “middle layer” hai jo request process hone se pehle ya response bhejne se pehle kuch kaam karta hai.

### Q45: Is restful api stateless??

Server ko har request ke liye poori information client se milni chahiye.
Server apni taraf se client ki previous requests ya session store nahi karta.
Iska fayda ye hai ke server simple, scalable aur reliable hota hai.
Example: Agar user login hai, har request me token (jaise JWT) bhejna padta hai, server khud session ya login state store nahi karta.

### Q46: If we have 10000 records to show in table how we optimnize this page speed ??

Pagination
Indexing
Send only required field

### Q47: Mongoose k middleware konse hn ??

In Mongoose (Node.js ODM), middleware (also called hooks) wo functions hote hain jo schema methods ke chalne se pehle ya baad mein run hote hain. Inko mainly pre aur post hooks ke through use kiya jata hai.

### Q48: Agr mre pas db se 10000 records aa rhy hn tou mn usko kse efficiently show krwao aur speed optimization kse axhi maintain kr skty ?

Server-side pagination use karte hain (LIMIT/OFFSET), taake ek time pe sirf 50–100 records load hon
Infinite scrolling ya pagination UI implement karte hain better UX ke liye
Frontend virtualization (react-window) use karte hain taake sirf visible items render hon
Database indexing apply karte hain taake queries fast ho jayein
Server-side filtering/searching use karte hain instead of frontend filtering
Aur caching (SWR / React Query) use karte hain taake unnecessary API calls avoid ho jayein

# Node.js Streams & MongoDB Performance Notes

## Node.js Streams

### readFile()

**Purpose:**

* Poori file memory mein load karta hai.

### Example

```js
fs.readFile("file.zip", (err, data) => {
  console.log(data);
});
```

### Flow

```text
File
↓
Poora RAM mein load
↓
Process
```

### Pros

* Simple

### Cons

* Large files par memory spike
* 2GB file = 2GB RAM use ho sakti hai

---

### createReadStream()

**Purpose:**

* File ko chunks mein read karta hai.

### Example

```js
const stream = fs.createReadStream("file.zip");

stream.on("data", (chunk) => {
  console.log(chunk.length);
});
```

### Flow

```text
File
↓
Chunk
↓
Process

File
↓
Chunk
↓
Process
```

### Pros

* Memory efficient
* Large files ke liye best

---

### pipe()

### Example

```js
const stream = fs.createReadStream("video.mp4");

stream.pipe(res);
```

### Flow

```text
File
↓
Stream
↓
Response
```

### Benefits

* Backpressure automatically handle karta hai
* Memory efficient

---

### Backpressure

#### Problem

```text
Producer Fast
↓
Consumer Slow
```

Memory bhar sakti hai.

#### Solution

```text
Producer
↓
Pause
↓
Consumer Catch-up
↓
Resume
```

---

## Memory Terms

### RSS

**Definition:**
Total RAM used by Node process.

### Example

```text
Before: 44 MB
After : 145 MB
```

Matlab Node process total 145 MB RAM use kar raha hai.

---

### Heap Used

**Definition:**
JavaScript Objects ki memory.

Includes:

* Objects
* Arrays
* Strings
* Functions

### Example

```js
const users = [];
```

Ye Heap memory use karega.

---

### External Memory

**Definition:**
Buffers aur file related memory.

Includes:

* Buffers
* File Data
* Streams

### Example

```js
fs.readFile("100mb-file")
```

External memory increase hogi.

---

# MongoDB Performance

## COLLSCAN

### Full Form

```text
Collection Scan
```

### Meaning

Mongo poori collection check kar raha hai.

### Example

```js
db.users.find({
  email: "abc@gmail.com"
});
```

Without index.

### Explain Output

```js
stage: "COLLSCAN"
```

### Bad Sign

```js
totalDocsExamined: 100000
```

---

## IXSCAN

### Full Form

```text
Index Scan
```

### Meaning

Mongo index use kar raha hai.

### Explain Output

```js
stage: "IXSCAN"
```

### Good Sign

```js
totalDocsExamined: 1
```

---

## explain()

### Purpose

Query internally kaise execute hui.

### Example

```js
db.users.find({
  email: "user99999@gmail.com"
}).explain("executionStats");
```

---

## executionTimeMillis

### Definition

Query execute hone mein kitna time laga.

### Example

```js
executionTimeMillis: 13
```

Meaning:

```text
13 milliseconds
```

---

## totalDocsExamined

### Definition

Mongo ne kitne actual documents check kiye.

### Bad

```js
100000
```

### Good

```js
1
```

---

## totalKeysExamined

### Definition

Mongo ne index mein kitni entries check ki.

### Bad

```js
100000
```

### Good

```js
1
```

---

# Indexes

## Create Single Index

```js
db.users.createIndex({
  email: 1
});
```

### Use Case

```js
db.users.find({
  email: "abc@gmail.com"
});
```

---

## Compound Index

```js
db.users.createIndex({
  city: 1,
  age: 1
});
```

### Meaning

Mongo pehle city ko sort karega, phir city ke andar age ko.

---

# Left Prefix Rule

Index:

```js
{
  city: 1,
  age: 1
}
```

### Works

```js
{
  city: "Lahore"
}
```

✅ Index Use

---

```js
{
  city: "Lahore",
  age: 25
}
```

✅ Index Use

---

### Doesn't Work

```js
{
  age: 25
}
```

❌ Index Use Nahi Hoga

### Reason

Mongo left-most field se index use karta hai.

---

# Practical Explain Analysis

## Without Index

```js
stage: "COLLSCAN"

totalDocsExamined: 100012
```

### Meaning

Mongo ne 100012 documents check kiye.

---

## With Email Index

```js
stage: "IXSCAN"

totalDocsExamined: 1

totalKeysExamined: 1
```

### Meaning

Mongo seedha required document tak gaya.

---

## With Compound Index

Index:

```js
{
  city: 1,
  age: 1
}
```

Query:

```js
{
  city: "Lahore",
  age: 25
}
```

Result:

```js
stage: "IXSCAN"

totalDocsExamined: 691
```

### Meaning

Mongo ne 100k+ docs skip kar diye aur sirf matching section scan kiya.

---

# Interview Quick Answers

## Q: COLLSCAN kya hai?

**Answer:**

Mongo poori collection scan kar raha hai.

---

## Q: IXSCAN kya hai?

**Answer:**

Mongo index use kar raha hai.

---

## Q: totalDocsExamined kya hai?

**Answer:**

Mongo ne kitne actual documents check kiye.

---

## Q: totalKeysExamined kya hai?

**Answer:**

Mongo ne kitni index entries check ki.

---

## Q: readFile vs createReadStream?

**Answer:**

```text
readFile
↓
Poora file RAM mein

createReadStream
↓
Chunks mein process
↓
Less memory
```

---

## Q: Backpressure kya hai?

**Answer:**

Jab producer fast ho aur consumer slow ho, to stream producer ko pause/resume karwati hai.

