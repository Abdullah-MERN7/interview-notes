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

## Q: Backpressure kya hai?

**Answer:**

Jab producer fast ho aur consumer slow ho, to stream producer ko pause/resume karwati hai.

# Redis Basics Notes

## What is Redis?

Redis (Remote Dictionary Server) ek in-memory key-value database hai.

### Key Features

* Data RAM mein store hota hai.
* Bahut fast hota hai.
* Caching ke liye use hota hai.
* OTP storage ke liye use hota hai.
* Rate limiting ke liye use hota hai.
* Session storage ke liye use hota hai.
* BullMQ queues Redis use karti hain.

# Redis vs MongoDB

## MongoDB

* Persistent Storage
* Data disk par store hota hai.
* Long-term storage ke liye use hota hai.

### Example

```js
{
  name: "Abdullah",
  email: "abdullah@gmail.com"
}
```

## Redis

* Temporary Fast Storage
* Data RAM mein store hota hai.
* Caching aur temporary data ke liye use hota hai.

# Redis Installation (Docker)

Run Redis Container

```bash
docker run -d --name redis-server -p 6379:6379 redis
```

Check Running Containers

```bash
docker ps
```

Open Redis CLI

```bash
docker exec -it redis-server redis-cli
```

# Redis CLI Basics

## Check Connection

```redis
PING
```

Output

```text
PONG
```

Meaning:

Redis server active hai.

## Store Data

```redis
SET name Abdullah
```

Output

```text
OK
```

Meaning:

Key = name

Value = Abdullah

## Read Data

```redis
GET name
```

Output

```text
"Abdullah"
```

## Delete Data

```redis
DEL name
```

# TTL (Time To Live)

Redis ki sabse powerful features mein se ek.

### Store Data With Expiry

```redis
SET otp 1234 EX 60
```

Meaning:

```text
Key = otp

Value = 1234

Expire = 60 seconds
```

## Check Remaining Time

```redis
TTL otp
```

Output

```text
(integer) 53
```

Meaning:

53 seconds baqi hain.

## Read OTP

```redis
GET otp
```

Output

```text
"1234"
```

60 seconds baad:

```redis
GET otp
```

Output

```text
(nil)
```

Meaning:

Redis ne key automatically delete kar di.

# Real World OTP Example

Store OTP

```redis
SET otp:abdullah@gmail.com 4821 EX 300
```

Meaning:

```text
OTP = 4821

Expiry = 5 Minutes
```

Benefits:

* No manual cleanup
* Auto deletion
* Fast access

# Redis with Node.js

Install Package

```bash
npm install redis
```

## Connect Redis

```js
const { createClient } = require("redis");

const client = createClient();

async function main() {
  await client.connect();

  await client.set("name", "Abdullah");

  const value = await client.get("name");

  console.log(value);

  await client.quit();
}

main();
```

Output

```text
Abdullah
```

# Concepts Learned

## Redis Server

Redis database server jo requests handle karta hai.

## SET

Data save karna.

Example:

```redis
SET name Abdullah
```

## GET

Data retrieve karna.

Example:

```redis
GET name
```

## TTL

Time To Live.

Example:

```redis
SET otp 1234 EX 60
```

Meaning:

60 seconds baad key automatically delete ho jayegi.

## Node.js + Redis

Node application Redis se connect karke data read/write kar sakti hai.

# Interview Quick Answers

## Redis kya hai?

In-memory key-value database.


## Redis MongoDB se fast kyun hai?

Kyuki Redis RAM mein data store karta hai.


## TTL kya hota hai?

Key ki expiry time.


## OTP MongoDB ki bajaye Redis mein kyun store karte hain?

* Fast access
* Auto expiry
* No cleanup required

# Redis Caching & Rate Limiting Notes

# Cache Aside Pattern

## Problem

Har request par MongoDB hit karna expensive hai.

Example:

```js
const user = await User.findById(id);
```

1000 requests:

```text
1000 Mongo Queries
```

---

## Solution

Redis cache use karo.

Flow:

```text
Request
↓
Redis Check
↓
Found?
↓      ↓
Yes    No
↓      ↓
Return Mongo
         ↓
      Save Redis
         ↓
       Return
```

---

# Cache Aside Example

```js
async function getUser(id) {
  const cacheKey = `user:${id}`;

  const cachedUser = await client.get(cacheKey);

  if (cachedUser) {
    console.log("Data from Redis");

    return JSON.parse(cachedUser);
  }

  const user = await getUserFromDB(id);

  await client.set(
    cacheKey,
    JSON.stringify(user),
    {
      EX: 60,
    }
  );

  console.log("Data from MongoDB");

  return user;
}
```

---

# Cache Miss

Definition:

Redis mein data nahi milta.

Flow:

```text
Redis ❌
↓
Mongo ✅
↓
Save Redis
↓
Return
```

Example Output:

```text
Fetching from MongoDB...
Data from MongoDB
```

---

# Cache Hit

Definition:

Redis mein data mil jata hai.

Flow:

```text
Redis ✅
↓
Return
```

Example Output:

```text
Data from Redis
```

Mongo hit nahi hoti.

---

# Stale Cache

Definition:

Mongo mein latest data hai lekin Redis mein purana data hai.

Example:

Mongo:

```js
{
  name: "Abdullah Tahir"
}
```

Redis:

```js
{
  name: "Abdullah"
}
```

Problem:

```text
User ko purana data milega.
```

---

# Cache Invalidation

Definition:

Update ke baad cache delete karna.

Example:

```js
await User.findByIdAndUpdate(id, data);

await client.del(`user:${id}`);
```

Flow:

```text
Update Mongo
↓
Delete Redis Cache
↓
Next Request
↓
Mongo
↓
Save Redis
```

---

# Redis DEL

Purpose:

Key delete karna.

Example:

```js
await client.del("user:123");
```

---

# TTL + Cache

Cache ko expiry dena.

Example:

```js
await client.set(
  "user:123",
  JSON.stringify(user),
  {
    EX: 60,
  }
);
```

Meaning:

```text
60 seconds baad cache auto delete
```

---

# Rate Limiting

Definition:

Ek user ya IP ko limited requests allow karna.

Example:

```text
5 requests per minute
```

---

# Redis INCR

Purpose:

Counter increase karna.

Example:

```redis
INCR login:192.168.1.1
```

Results:

```text
Request 1 -> 1
Request 2 -> 2
Request 3 -> 3
Request 4 -> 4
Request 5 -> 5
Request 6 -> 6
```

---

# Rate Limiter Logic

```js
const count = await client.incr("login:ip");

if (count === 1) {
  await client.expire("login:ip", 60);
}

if (count > 5) {
  return res.status(429).json({
    message: "Too many requests"
  });
}
```

---

# Why expire() Only Once?

Correct:

```js
if (count === 1) {
  await client.expire("login:ip", 60);
}
```

Reason:

Countdown sirf first request par start karna hai.

---

Wrong:

```js
await client.expire("login:ip", 60);
```

har request par.

Problem:

```text
Request
↓
60 sec

Request
↓
60 sec reset

Request
↓
60 sec reset
```

Key kabhi expire nahi hogi.

---

# Rate Limiting Flow

Request 1

```text
Count = 1
Expire = 60 sec
Allow
```

---

Request 2

```text
Count = 2
Allow
```

---

Request 3

```text
Count = 3
Allow
```

---

Request 4

```text
Count = 4
Allow
```

---

Request 5

```text
Count = 5
Allow
```

---

Request 6

```text
Count = 6
↓
Block
↓
429 Too Many Requests
```

---

# After 60 Seconds

Redis key auto delete.

Example:

```text
login:192.168.1.1
↓
Deleted
```

Next Request:

```text
Count = 1
```

because key no longer exists.

---

# HTTP Status Code

Rate limit exceed:

```http
429 Too Many Requests
```

# Interview Quick Answers

## Cache Miss

Redis mein data nahi mila.

## Cache Hit

Redis mein data mil gaya.

## Stale Cache

Redis mein purana data pada hua hai.

## Cache Invalidation

Update ke baad cache delete karna.

## INCR

Redis counter increase karta hai.

## DEL

Redis key delete karta hai.

## TTL

Key ki expiry time.

## Redis Down Ho Jaye To?

Application chal sakti hai.

Reason:

```text
MongoDB source of truth hai.

Redis performance improve karti hai.
```

Result:

```text
App Slow
❌ App Down nahi
```

# BullMQ Fundamentals Notes

# What is BullMQ?

BullMQ ek queue system hai jo Redis ke upar build hota hai.

Purpose:

* Background jobs process karna
* Heavy tasks request lifecycle se bahar nikalna
* Retries handle karna
* Scheduled jobs run karna

# Problem Without Queue

Example:

```js
await User.create(user);

await sendWelcomeEmail(user.email);

return res.json({
  success: true,
});
```

Flow:

```text
Signup
↓
Send Email
↓
Wait
↓
Response
```

Problem:

```text
User ko unnecessary wait karna padega.
```

# Solution With BullMQ

```text
Signup
↓
Create User
↓
Add Job To Queue
↓
Response Immediately

Background Worker
↓
Send Email
```

Benefits:

```text
Fast API Response
Background Processing
Retries
Scalability
```

# Main Components

## Queue

Waiting area for jobs.

Example:

```text
Job 1
Job 2
Job 3
Job 4
```

## Job

Single task.

Example:

```json
{
  "email": "abdullah@gmail.com"
}
```

## Worker

Queue se jobs uthata hai aur process karta hai.

Flow:

```text
Queue
↓
Worker
↓
Execute Task
```

# Producer

Producer ka kaam:

```text
Create Job
↓
Add To Queue
```

Example:

```js
await emailQueue.add(
  "send-email",
  {
    email: "abdullah@gmail.com",
  }
);
```

Producer task execute nahi karta.

Sirf queue mein add karta hai.

# Worker

Worker ka kaam:

```text
Queue Se Job Lo
↓
Process Karo
```

Example:

```js
const worker = new Worker(
  "email-queue",
  async (job) => {
    console.log(job.data);
  }
);
```

# FIFO

FIFO = First In First Out

Example:

```text
Job 1
Job 2
Job 3
```

Processing:

```text
Job 1
↓
Job 2
↓
Job 3
```

Jo pehle queue mein aaya woh pehle process hoga.

# Concurrency

## Concurrency = 1

Example:

```text
Job 1
↓
Complete

Job 2
↓
Complete

Job 3
↓
Complete
```

One job at a time.

Example:

```text
5 Jobs
3 sec each
```

Total:

```text
15 sec
```

## Concurrency = 5

```js
const worker = new Worker(
  "email-queue",
  async (job) => {
    // work
  },
  {
    concurrency: 5,
  }
);
```

Flow:

```text
Job 1
Job 2
Job 3
Job 4
Job 5
```

All start together.

Example:

```text
5 Jobs
3 sec each
```

Total:

```text
≈ 3 sec
```

# Failed Jobs

Example:

```js
throw new Error("Email Service Down");
```

Output:

```text
Job Failed
```

# Retries

Example:

```js
await emailQueue.add(
  "send-email",
  {
    email: "abdullah@gmail.com",
  },
  {
    attempts: 3,
  }
);
```

Flow:

```text
Try 1
↓
Fail

Try 2
↓
Fail

Try 3
↓
Fail
```

BullMQ automatically retry karti hai.

# Backoff

Retries ke darmiyan delay.

Example:

```js
await emailQueue.add(
  "send-email",
  {
    email: "abdullah@gmail.com",
  },
  {
    attempts: 3,

    backoff: {
      type: "fixed",
      delay: 5000,
    },
  }
);
```

Flow:

```text
Try 1
↓
Fail

Wait 5 sec

Try 2
↓
Fail

Wait 5 sec

Try 3
↓
Fail
```

# Worker Down Scenario

Queue:

```text
Queue ✅
Worker ❌
```

Result:

```text
Jobs delete nahi hoti
Jobs queue mein wait karti hain
```

Jab worker start hota hai:

```text
Queue
↓
Worker
↓
Process Jobs
```

# When To Use Queue?

Rule:

```text
Heavy tasks jo user response ke liye immediately required nahi hote.
```

# Direct Tasks

User response ke liye required.

Examples:

```text
Login
Password Validation
JWT Generation
User Creation
Payment Validation
OTP Verification
```

# Queue Tasks

Background processing.

Examples:

```text
Welcome Email
Newsletter Email
PDF Generation
Excel Export
Image Resize
Video Processing
Push Notifications
```

# Special Case: OTP Email

OTP email usually:

```text
Direct ✅
```

Reason:

```text
User next step OTP par depend karta hai.
```

Example:

```text
Forgot Password
↓
OTP Email
↓
OTP Enter
↓
Reset Password
```

OTP ke baghair flow continue nahi kar sakta.

# Real World Examples

## Queue

```text
Welcome Email
PDF Generation
Excel Export
Image Processing
Video Processing
Push Notifications
```

## Direct

```text
Login
Signup
JWT Generate
OTP Verification
Payment Validation
```

## BullMQ Kya Hai?

Redis based queue system.

## Queue Kyun Use Karte Hain?

* Fast API response
* Background jobs
* Retries
* Scalability

## Producer Kya Karta Hai?

Job create karta hai aur queue mein add karta hai.

## Worker Kya Karta Hai?

Queue se job uthata hai aur process karta hai.

## FIFO Kya Hai?

First In First Out.

Jo pehle queue mein aata hai woh pehle process hota hai.

## attempts: 3 Kya Karta Hai?

Job fail hone par BullMQ automatically 3 times retry karti hai.

# MongoDB Query Optimization Notes

# Projection Optimization

## Query

```js
db.users.find({
  city: "Lahore"
})
```

Result:

```text
IXSCAN ✅
FETCH ✅

totalKeysExamined: 33339
totalDocsExamined: 33339
```

Mongo index use karta hai lekin poora document bhi fetch karta hai.

Flow:

```text
IXSCAN
↓
FETCH
↓
Return Documents
```

## Projection

```js
db.users.find(
  {
    city: "Lahore"
  },
  {
    name: 1,
    email: 1,
    _id: 0
  }
)
```

Result:

```text
PROJECTION_SIMPLE

totalDocsExamined: 33339
```

Observation:

```text
Documents examined same rahe
Lekin response size kam ho gaya
```

Benefits:

* Less network transfer
* Less memory usage
* Faster response

# FETCH

MongoDB ke paas:

```text
Index
+
Actual Documents
```

hote hain.

Example:

```js
{
  _id: 1,
  name: "Abdullah",
  email: "abdullah@gmail.com",
  age: 25,
  city: "Lahore"
}
```

Index:

```text
abdullah@gmail.com
↓
Document Location
```

FETCH ka matlab:

```text
Index se document location mili
↓
Collection mein jao
↓
Actual document uthao
```

# Covered Query

Rule:

```text
Filter fields
+
Projection fields

Dono index mein hone chahiye.
```

Example:

Index:

```js
db.users.createIndex({
  email: 1
})
```

Query:

```js
db.users.find(
  {
    email: "user99999@gmail.com"
  },
  {
    email: 1,
    _id: 0
  }
)
```

Result:

```text
PROJECTION_COVERED

totalDocsExamined: 0
totalKeysExamined: 1
```

Observation:

```text
Mongo collection mein gaya hi nahi.
```

Flow:

```text
IXSCAN
↓
Return Result
```

# Covered Query Kab Break Hoti Hai?

Query:

```js
db.users.find(
  {
    email: "user99999@gmail.com"
  },
  {
    email: 1,
    age: 1,
    _id: 0
  }
)
```

Problem:

```text
age index mein nahi hai.
```

Result:

```text
FETCH wapas aa jayega.
```

Flow:

```text
IXSCAN
↓
FETCH
↓
Return
```

# Pagination Optimization

## Skip Pagination

Query:

```js
db.users.find()
.skip(50000)
.limit(10)
```

Result:

```text
totalDocsExamined: 50010
```

Why?

Mongo internally:

```text
1
2
3
...
50000
```

skip karta hai.

Phir:

```text
50001
50002
...
50010
```

return karta hai.

Problem:

```text
Large datasets par slow ho jata hai.
```

## Cursor Pagination

Query:

```js
db.users.find({
  _id: {
    $gt: lastId
  }
})
.sort({ _id: 1 })
.limit(10)
```

Example:

```js
db.users.find({
  _id: {
    $gt: ObjectId("69b2449cc2c4f2a81f6beb38")
  }
})
.sort({ _id: 1 })
.limit(10)
```

Result:

```text
IXSCAN

totalKeysExamined: 10
totalDocsExamined: 10
executionTimeMillis: 0
```

Observation:

```text
Mongo directly index par jump karta hai.
```

Flow:

```text
IXSCAN
↓
FETCH
↓
Return 10 Docs
```

# Skip vs Cursor Pagination

## Skip Pagination

```js
db.users.find()
.skip(50000)
.limit(10)
```

Result:

```text
totalDocsExamined: 50010
```

Cons:

* Slow on large datasets
* Extra document scanning
* Poor scalability

## Cursor Pagination

```js
db.users.find({
  _id: {
    $gt: lastId
  }
})
.limit(10)
```

Result:

```text
totalDocsExamined: 10
```

Pros:

* Direct index jump
* Better performance
* Scales to millions of records
* Production-friendly

# Important Concepts Learned

✅ Projection

✅ FETCH

✅ PROJECTION_SIMPLE

✅ Covered Query

✅ PROJECTION_COVERED

✅ totalDocsExamined

✅ totalKeysExamined

✅ Skip Pagination

✅ Cursor Pagination

✅ Query Optimization Thinking

# Common Optimization Checklist

1. Check explain()

```js
.explain("executionStats")
```

2. Verify:

```text
IXSCAN
```

instead of

```text
COLLSCAN
```

3. Check:

```text
totalDocsExamined
```

4. Use Projection when possible

5. Use Covered Queries when possible

6. Avoid large skip()

7. Prefer Cursor Pagination on large datasets

```
```

# Additional MongoDB Production Notes

## 1. Prefix Search

Contains Search:

```js
{
  name: {
    $regex: "john",
    $options: "i"
  }
}
```

Matches:

* John Doe
* MyJohn
* abcjohn

Problem:

* Index efficiently use nahi hota.
* Large datasets par slow ho sakta hai.

---

Prefix Search:

```js
{
  name: {
    $regex: new RegExp(`^${search}`, "i")
  }
}
```

Matches:

* John Doe
* John Wick

Doesn't Match:

* MyJohn
* abcjohn

Benefits:

* Index-friendly
* Better performance
* Recommended for search APIs

---

## 2. Dynamic Query Building

Avoid:

```js
query = {
  name: ...,
  isAdmin: ...
}
```

Preferred:

```js
let query = {};

if (search) {
  query.name = {
    $regex: new RegExp(`^${search}`, "i"),
  };
}

if (isAdmin !== undefined) {
  query.isAdmin = isAdmin === "true";
}
```

Benefits:

* Independent filters
* Easy to maintain
* Easy to add new filters

---

## 3. Boolean Filter

Request:

```http
GET /api/users?isAdmin=true
```

Implementation:

```js
query.isAdmin = isAdmin === "true";
```

Reason:

`req.query` always returns strings.

---

## 4. Date Range Filter

Request:

```http
GET /api/users?createdAfter=2026-01-01&createdBefore=2026-12-31
```

Implementation:

```js
if (createdAfter) {
  query.createdAt = {
    ...query.createdAt,
    $gte: new Date(createdAfter),
  };
}

if (createdBefore) {
  query.createdAt = {
    ...query.createdAt,
    $lte: new Date(createdBefore),
  };
}
```

Benefits:

* Works if only `createdAfter` is provided.
* Works if only `createdBefore` is provided.
* Works if both are provided.

---

## 5. countDocuments()

Useful for pagination.

```js
const totalUsers = await User.countDocuments(query);
```

Calculate total pages:

```js
const totalPages = Math.ceil(totalUsers / limit);
```

---

## 6. lean()

Without:

```js
const users = await User.find();
```

Returns:

* Mongoose Document

```text
instanceof User -> true
typeof user.save -> function
constructor -> model
```

---

With:

```js
const users = await User.find().lean();
```

Returns:

* Plain JavaScript Object

```text
instanceof User -> false
typeof user.save -> undefined
constructor -> Object
```

Use `lean()`:

* GET APIs
* Read-only APIs
* Listing APIs

Don't use `lean()` when:

```js
user.save();
```

is required.

---

## 7. Production User API

Current API supports:

* Search
* Prefix Search
* Sorting
* Pagination
* Boolean Filter
* Date Range Filter
* Projection
* countDocuments()
* lean()

Example:

```http
GET /api/users?page=1&limit=10&search=jo&sort=name&isAdmin=true&createdAfter=2026-01-01&createdBefore=2026-12-31
```

# Express Middleware & Error Handling

## What is Middleware?

Middleware ek function hota hai jo:

- Request receive karta hai.
- Request ko process karta hai.
- Ya to agle middleware ko pass karta hai.
- Ya client ko response bhej deta hai.

Structure:

```js
(req, res, next) => {}
```

Flow:

```text
Request
    ↓
Middleware 1
    ↓
Middleware 2
    ↓
Route
    ↓
Response
```

# app.use()

`app.use()` middleware register karta hai.

Example:

```js
app.use(express.json());

app.use(logger);

app.use(authMiddleware);
```

Routes bhi middleware chain ka part hote hain.

```js
app.use("/users", userRoutes);
```

# next()

`next()` ka matlab:

```text
Agla middleware ya route execute karo.
```

Example:

```js
app.use((req, res, next) => {
    console.log("Middleware");

    next();
});
```

Flow:

```text
Middleware
    ↓
next()
    ↓
Next Middleware / Route
```

# next() Function Stop Nahi Karta

Example:

```js
app.use((req, res, next) => {
    console.log("1");

    next();

    console.log("2");
});
```

Output:

```text
1
2
```

Observation:

```text
next() current function ko stop nahi karta.
```

# return next()

Example:

```js
app.use((req, res, next) => {
    console.log("1");

    return next();

    console.log("2");
});
```

Output:

```text
1
```

Observation:

```text
return next()

↓

Current middleware/function ko terminate kar deta hai.
```

# res.send()

Example:

```js
app.get("/", (req, res) => {
    console.log("A");

    res.send("Hello");

    console.log("B");
});
```

Output:

```text
A
B
```

Observation:

```text
res.send()

↓

Sirf response bhejta hai.

↓

Function continue karta hai.
```

# return res.send()

Example:

```js
app.get("/", (req, res) => {
    console.log("A");

    return res.send("Hello");

    console.log("B");
});
```

Output:

```text
A
```

Observation:

```text
return

↓

Current function terminate.
```
# Error Handling (Without Middleware)

Example:

```js
router.get("/", async (req, res) => {
    try {
        const users = await User.find();

        res.json(users);

    } catch (err) {
        res.status(500).json({
            message: err.message
        });
    }
});
```

Problem:

```text
Har route mein duplicate try/catch.
```

# Global Error Middleware

Structure:

```js
app.use((err, req, res, next) => {

});
```

Express kaise pehchanta hai?

```text
4 Parameters

(err, req, res, next)

↓

Error Middleware
```

Normal Middleware:

```js
(req, res, next)
```

# next(err)

Meaning:

```text
Current error ko Express ke Error Middleware tak bhejo.
```

Flow:

```text
Route

↓

Error

↓

next(err)

↓

Normal Middleware Skip

↓

Error Middleware

↓

Client Response
```

# Error Middleware Example

```js
const errorHandler = (err, req, res, next) => {

    return res.status(500).json({
        message: err.message
    });

};
```

# asyncHandler

Problem:

Har route mein:

```js
try {

} catch(err){

    return next(err);

}
```

repeat ho raha tha.

Solution:

```js
const asyncHandler = (fn) => {

    return (req, res, next) => {

        return fn(req, res, next).catch(next);

    };

};
```

Usage:

```js
router.get(
    "/users",

    asyncHandler(async (req, res) => {

        const users = await User.find();

        res.json(users);

    })
);
```

Flow:

```text
Request

↓

Route Execute

↓

Promise Resolve
        ↓
     Success

OR

Promise Reject
        ↓
.catch(next)
        ↓
next(err)
        ↓
Global Error Middleware
        ↓
Client Response
```

# Promise.catch(next)

Equivalent:

```js
.catch((err) => {

    next(err);

});
```

# Why asyncHandler?

Benefits:

- Removes duplicate try/catch
- Cleaner routes
- Centralized error handling
- Easy maintenance
- Production-friendly

# Golden Rules

## Rule 1

```text
next()

↓

Agla middleware execute.
```

## Rule 2

```text
return next()

↓

Current middleware stop.
```

## Rule 3

```text
res.send()

↓

Response send

↓

Function continue.
```

## Rule 4

```text
return res.send()

↓

Response send

↓

Function terminate.
```

## Rule 5

```text
next(err)

↓

Normal middleware skip

↓

Error Middleware execute.
```
# Node.js Notes (Part 2)

---

# Promise.all()

## Sequential Execution

```js
const users = await getUsers();
const chats = await getChats();
```

Flow:

```
Users

↓

Wait

↓

Chats

↓

Wait
```

Total Time:

```
2 sec + 3 sec = 5 sec
```

Use When:

- Operation B depends on Operation A.

Example:

```js
const user = await User.findById(id);

const posts = await Post.find({
    userId: user._id
});
```

---

## Parallel Execution

```js
const [users, chats] = await Promise.all([
    getUsers(),
    getChats()
]);
```

Flow:

```
Users Start

Chats Start

↓

Users Finish

Chats Finish

↓

Promise.all Resolve
```

Total Time:

```
Longest Operation
```

Example:

```
Users = 2 sec
Chats = 3 sec

Total = 3 sec
```

Use When:

- Operations are independent.
- One operation does not need another operation's result.

Example:

```js
await Promise.all([
    User.countDocuments(),
    Product.countDocuments(),
    Order.countDocuments()
]);
```

---

## Golden Rule

Dependent Operations

```
await
await
await
```

Independent Operations

```
Promise.all()
```

---

## Promise.all() Failure

If one Promise rejects:

```js
await Promise.all([
    Promise.resolve(1),
    Promise.reject("Error"),
    Promise.resolve(3)
]);
```

Result:

```
Promise.all Reject
```

Remaining Promises:

```
Continue in background.
```

Promise.all does NOT cancel running operations.

---

## Promise.allSettled()

Purpose:

Return result of every Promise.

Even if some fail.

Example:

```js
const result = await Promise.allSettled([
    Promise.resolve("Users"),
    Promise.reject("DB Error"),
    Promise.resolve("Orders")
]);
```

Output:

```js
[
  {
    status: "fulfilled",
    value: "Users"
  },
  {
    status: "rejected",
    reason: "DB Error"
  },
  {
    status: "fulfilled",
    value: "Orders"
  }
]
```

Use Case:

- Dashboard
- Analytics
- Reports

Where partial data is acceptable.

---

# Streams

## Why Streams?

Problem:

```js
fs.readFile("movie.mp4");
```

Loads complete file into RAM.

Large files may cause:

```
Out Of Memory
```

---

## Stream Solution

```js
fs.createReadStream()
```

Reads file in chunks.

Example:

```
100 MB File

↓

10 MB

↓

10 MB

↓

10 MB

↓

...
```

Memory remains almost constant.

---

## Important Events

### data

Runs for every chunk.

```js
readStream.on("data", (chunk) => {});
```

---

### end

Runs after complete file is read.

```js
readStream.on("end", () => {});
```

---

### error

Runs if reading fails.

```js
readStream.on("error", (err) => {});
```

---

## Write Stream

```js
const writeStream =
fs.createWriteStream("copy.txt");
```

Writes data into a file.

---

## Pipe

Without Pipe:

```js
readStream.on("data", chunk => {
    writeStream.write(chunk);
});

readStream.on("end", () => {
    writeStream.end();
});
```

With Pipe:

```js
readStream.pipe(writeStream);
```

Purpose:

Automatically move chunks from Read Stream to Write Stream.

---

## Pipe Limitation

Pipe copies data as-is.

Cannot modify data.

If data transformation is required:

```js
chunk.toString().toUpperCase()
```

Use manual processing (or Transform Streams).

---

# Redis

## What is Redis?

Redis is an in-memory database.

Purpose:

Store frequently accessed data temporarily in RAM.

---

## Why Redis?

Without Redis:

```
Client

↓

MongoDB

↓

Response
```

Every request hits MongoDB.

With Redis:

```
Client

↓

Redis

↓

Found?

↓

Yes → Response

No → MongoDB

↓

Save to Redis

↓

Response
```

---

## Cache Hit

```
Data found in Redis.
```

MongoDB is not used.

---

## Cache Miss

```
Data not found in Redis.
```

MongoDB is queried.

Data is stored again in Redis.

---

## TTL

Full Form:

```
Time To Live
```

Purpose:

Automatically remove cached data after a specific time.

Example:

```
TTL = 60 seconds

↓

Key expires automatically.
```

---

# Rate Limiting

Problem:

Attacker sends:

```
10000 requests/minute
```

Without Rate Limiting:

```
MongoDB

↓

10000 Queries
```

---

## Solution

Store request counter in Redis.

Example:

```
IP

↓

Counter = 1

↓

Counter = 2

↓

Counter = 3
```

If limit exceeded:

```
429 Too Many Requests
```

Request is rejected before reaching MongoDB.

---

## Why Redis?

Request counter changes frequently.

Redis stores data in RAM.

Much faster than MongoDB.

---

## Rate Limiting Flow

```
Request

↓

Redis

↓

Counter Exists?

↓

No

↓

Counter = 1

TTL = 60 sec

↓

Allow Request

----------------

Counter Exists

↓

Increment Counter

↓

Counter > Limit ?

↓

Yes

↓

429 Too Many Requests

↓

No

↓

Allow Request
```

---

# Quick Revision

## Promise.all()
- Parallel Execution
- Independent Operations
- Fail Fast
- Doesn't cancel running Promises
---
## Promise.allSettled()
- Returns all results
- Resolve + Reject both returned
---
## Streams
- Reads data in chunks
- Saves RAM
- data
- end
- error
- pipe()
---
## Redis
- In-memory database
- Cache
- Cache Hit
- Cache Miss
- TTL
---
## Rate Limiting
- Redis Counter
- TTL
- 429 Too Many Requests

# Node.js - Promise & Async Notes

# 1. Sequential Execution

```js
const users = await getUsers();
const chats = await getChats();
```

Execution:

```
getUsers()

↓

Wait

↓

getChats()

↓

Wait
```

✅ Use when:

- Operation B depends on Operation A.

Example:

```js
const user = await User.findById(id);

const posts = await Post.find({
    userId: user._id
});
```

# 2. Parallel Execution (Promise.all)

```js
const [users, chats] = await Promise.all([
    getUsers(),
    getChats()
]);
```

Execution:

```
getUsers()  🚀

getChats()  🚀

↓

Wait for both

↓

Result
```

✅ Use when:

- Operations are independent.

Example:

```js
await Promise.all([
    User.find(),
    Post.find(),
    Comment.find()
]);
```

# Promise.all Rules

✅ Input order maintain hota hai.

```js
const [users, posts] = await Promise.all([
    User.find(),
    Post.find()
]);
```

Chahe Post pehle complete ho.

Result:

```js
[users, posts]
```

✅ Ek promise reject

↓

Promise.all reject.

✅ Baaki promises automatically cancel nahi hoti.

Wo background mein chalti rehti hain.

# Start Early, Await Late

❌ No Benefit

```js
const usersPromise = User.find();

const users = await usersPromise;
```

Immediately wait.

✅ Better

```js
const usersPromise = User.find();

const config = await getConfig();

const users = await usersPromise;
```

Rule:

Start promise as early as possible.

Await as late as possible.

Faida tabhi hai jab beech mein koi aur useful work ho.

# Promise.allSettled()

```js
const result = await Promise.allSettled([
    User.find(),
    Post.find(),
    Notification.find()
]);
```

Result:

```js
[
    {
        status: "fulfilled",
        value: ...
    },
    {
        status: "rejected",
        reason: ...
    }
]
```

Use when:

- Partial data bhi acceptable ho.

Examples:

- Dashboard
- Analytics
- Reports
- Admin Panel

# Promise.all vs Promise.allSettled

Promise.all

- All success required.
- One reject → Whole reject.

Promise.allSettled

- Success + Failure dono ka result milta hai.
- Har promise ka status available hota hai.

# Async Loop

❌ Wrong

```js
users.forEach(async (user) => {
    await saveUser(user);
});
```

Reason:

forEach promises ka wait nahi karta.

✅ Sequential

```js
for (const user of users) {
    await saveUser(user);
}
```

Use when:

Order matter karta ho.

✅ Parallel

```js
await Promise.all(
    users.map(user => saveUser(user))
);
```

Execution:

users

↓

map()

↓

[Promise, Promise, Promise]

↓

Promise.all()

↓

[Value, Value, Value]

# map()

```js
users.map(user => saveUser(user))
```
Returns:

```js
[
    Promise,
    Promise,
    Promise
]
```

Promise.all wait karta hai.

Final result:

```js
[
    value1,
    value2,
    value3
]
```

# Golden Rules

## Sequential

```js
await A();
await B();
```

When:

B depends on A.

## Parallel

```js
await Promise.all([
    A(),
    B()
]);
```

When:

A & B are independent.

## Partial Success

```js
await Promise.allSettled([
    A(),
    B()
]);
```

When:

Available data bhi return karna ho.

## Loop

❌

```js
forEach(async ...)
```

```js
for...of
```

Sequential.

```js
Promise.all(arr.map(...))
```
Parallel.
# Remember

✔ Promise.all preserves input order.

✔ Promise.all rejects if one promise rejects.

✔ Promise.all does NOT cancel other promises.

✔ forEach does NOT wait for async callbacks.

✔ map() returns an array.

✔ async function always returns a Promise.

✔ Start Early, Await Late only when there's useful work before await.

# Node.js - Streams, EventEmitter & Buffer Notes

# Streams

## Problem

```js
fs.readFile("movie.mp4");
```

Large file.

↓

Entire file RAM mein load hoti hai.

Problem:

- High Memory Usage
- Out Of Memory
- Large files ke liye suitable nahi.

## Stream Solution

Instead of loading whole file:

```
File

↓

Chunk

↓

Process

↓

Discard

↓

Next Chunk

↓

Process
```

Benefits:

- Low Memory Usage
- Large Files Handle
- Memory Efficient

## Read Stream Events

### data

Har new chunk par fire hota hai.

```js
stream.on("data", (chunk) => {});
```

### end

Jab poori file successfully read ho jaye.

```js
stream.on("end", () => {});
```

### error

Read karte waqt koi problem aaye.

Examples:

- File not found
- Permission denied
- Disk Error

```js
stream.on("error", (err) => {});
```

## Stream Flow

```
File

↓

Chunk

↓

data Event

↓

Chunk

↓

data Event

↓

Chunk

↓

data Event

↓

end Event
```

# Writable Stream

```js
const write = fs.createWriteStream("copy.txt");
```

Used to write data.

# pipe()

Manual:

```js
read.on("data", (chunk) => {
    write.write(chunk);
});
```

Production:

```js
read.pipe(write);
```

Benefits:

- Cleaner Code
- Automatic Chunk Transfer
- Automatic Backpressure Handling

## pipe() Flow

```
Read Stream

↓

pipe()

↓

Write Stream
```

Automatically continues until Read Stream ends.

# Backpressure

Problem:

```
Read Speed

100 MB/s

↓

Write Speed

20 MB/s
```

Without handling:

```
Memory keeps increasing.
```

Solution:

```
pipe()

↓

Pause Read

↓

Write Complete

↓

Resume Read
```

Rule:

Fast producer should slow down when consumer is slow.

# Stream Purpose

Streams optimize:

✅ Memory

Not Time.

# EventEmitter

Normal Class

```js
class Chat {}
```

No events.

Enable Events

```js
class Chat extends EventEmitter {}
```

Now Chat has:

```js
.on()

.emit()

.once()

.off()
```

## on()

Registers listener.

```js
chat.on("message", callback);
```

Does NOT execute callback immediately.

## emit()

Triggers event.

```js
chat.emit("message");
```

Flow:

```
emit()

↓

Event

↓

Listener

↓

Callback
```

## once()

Runs only first time.

```js
chat.once("message", callback);
```

Flow:

```
First emit

↓

Callback

↓

Listener Removed

↓

Next emit

↓

Nothing
```

## off()

Removes listener.

```js
chat.off("message", callback);
```

After removing:

```js
emit()
```

↓

Nothing happens.

# EventEmitter Examples

Browser

```js
button.addEventListener("click", callback);
```

Concept:

```
Click

↓

Event

↓

Callback
```

Streams

```js
stream.on("data", callback);
```

Concept:

```
Chunk

↓

Event

↓

Callback
```

# Buffer

Computer stores everything as:

```
Binary (0 & 1)
```

Node.js stores binary data temporarily inside:

```
Buffer
```

Definition:

Buffer = Temporary memory area for binary data.

# Buffer Flow

```
File

↓

Binary

↓

Buffer

↓

Your Code
```

# Stream Chunk

```js
stream.on("data", (chunk) => {});
```

Question:

What is chunk?

Answer:

```
Buffer
```

Not String.

# Buffer Output

```js
console.log(chunk);
```

Output:

```text
<Buffer ...>
```

# Convert Buffer → String

```js
chunk.toString();
```

Example:

```
Buffer

↓

toString()

↓

Hello
```

# When to use toString()

✅ Text Files

- txt
- json
- csv
- xml

---

❌ Do NOT use for

- Images
- Videos
- PDFs
- ZIP Files

These should remain binary.

# Buffer Checks

```js
typeof buffer
```

Output:

```text
object
```

Specific check:

```js
Buffer.isBuffer(buffer)
```

Output:

```text
true
```
# Connection

```
Disk

↓

Binary

↓

Buffer

↓

Stream

↓

data Event

↓

Your Code
```

# Golden Rules

## Streams

Purpose:

```
Memory Optimization
```

## Promise.all

Purpose:

```
Time Optimization
```

## Buffer

Purpose:

```
Handle Binary Data Efficiently
```
## EventEmitter

```
on()
```

↓

Register Listener

```
emit()
```

↓

Fire Event


```
once()
```

↓

Run Once

```
off()
```

↓

Remove Listener


# Remember

✔ Streams process data chunk by chunk.

✔ Chunk is Buffer.

✔ Buffer stores binary data.

✔ Buffer ≠ String.

✔ Use toString() only for text data.

✔ pipe() automatically handles chunk transfer & backpressure.

✔ EventEmitter is the foundation of Streams.

# Redis Fundamentals

## Why Redis?

Problem:

```js
const products = await Product.find();
```

Every request hits MongoDB.

```
1000 Users
↓
1000 MongoDB Queries
```

## Solution

Store frequently accessed data in Redis.

```
Client
↓
Redis
↓
Cache Hit ✅
↓
Response
```

## Cache Hit

Data exists in Redis.

## Cache Miss

Data not found in Redis.
↓
MongoDB
↓
Redis
↓
Response

## TTL

Automatically removes cache after a specific time.

```redis
EXPIRE products 300
```

## Commands

```redis
SET products "[...]"
GET products
DEL products
EXPIRE products 300
TTL products
```

# Redis Practical Implementation

## GET /products Flow

```
Client
↓
Express
↓
Redis
↓
Cache Hit?
├── Yes → Return Response
└── No
      ↓
   MongoDB
      ↓
   Store in Redis
      ↓
   Return Response
```

## Cache Hit

```js
const cachedProducts = await redis.get("products");

if (cachedProducts) {
    return res.json(JSON.parse(cachedProducts));
}
```

No MongoDB query.

## Cache Miss

```js
const products = await Product.find();

await redis.set("products", JSON.stringify(products));

await redis.expire("products", 300);

return res.json(products);
```

Flow:

```
Cache Miss
↓
MongoDB
↓
Redis SET
↓
EXPIRE
↓
Response
```

## Better Approach

Instead of:

```js
await redis.set("products", JSON.stringify(products));
await redis.expire("products", 300);
```

Prefer:

```redis
SET products "data" EX 300
```

Reason:

- Single command
- Atomic operation
- Prevents data without TTL

## Cache Invalidation

After updating MongoDB:

```js
await redis.del("products");
```

Flow:

```
Update MongoDB
↓
Delete Redis Cache
↓
Next Request
↓
Cache Miss
↓
MongoDB
↓
Redis Store
```

## Invalidate All Affected Caches

If Product 2 changes:

```
products
featured-products
top-selling-products
product:2
```

All related caches should be invalidated.

Do not invalidate unrelated caches like:

```
users
cart
sessions
```

## Redis String

Best for:

- Cache
- OTP
- JWT
- Access Token
- Refresh Token
- Complete JSON Objects

Store:

```js
await redis.set(
    "user:15",
    JSON.stringify(user)
);
```

Read:

```js
const data = await redis.get("user:15");

const user = JSON.parse(data);
```

Flow:

```
Object
↓
JSON.stringify()
↓
Redis String
↓
GET
↓
JSON.parse()
↓
Object
```

## Limitation of String

Updating one field requires:

```
GET
↓
JSON.parse()
↓
Update Field
↓
JSON.stringify()
↓
SET
```

Entire object must be rewritten.

## Redis Hash

Best for:

- User Profile
- User Session
- Product Details
- Frequently Updated Objects

Structure:

```
user:15

id      → 15
name    → Ali
email   → ali@gmail.com
role    → Admin
```

Only required fields can be updated.

No need to rewrite the whole object.

## Hash Commands

Store field:

```redis
HSET user:15 name Ali
```

Get one field:

```redis
HGET user:15 email
```

Get multiple fields:

```redis
HMGET user:15 name email role
```

Get complete hash:

```redis
HGETALL user:15
```

Check field exists:

```redis
HEXISTS user:15 phone
```

## String vs Hash

### String

Use when:

- Single value
- Complete JSON cache
- Rare updates

### Hash

Use when:

- Individual fields update frequently
- Partial reads are common
- Partial updates are required

## Golden Rules

- Always check Redis before MongoDB.
- Cache Hit should never query MongoDB.
- Cache Miss should populate Redis.
- Always set TTL for cache.
- Use atomic `SET ... EX` when possible.
- Invalidate every affected cache after updates.
- Store objects as JSON in String.
- Use Hash when fields change independently.
- Fetch only the fields you actually need.