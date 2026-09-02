Haan bhai 😭 meri galti. **Ek hi single code block mein de raha hoon**, taake pura ek sath copy ho jaye:

````md
# Redis Caching – Day 2

## 1. Dynamic Cache Keys

Query parameters ke according unique cache key banani chahiye.

Example:

GET /books?author=John&page=1
GET /books?author=Ali&page=1

Different data ke liye different keys:

books:author:John:page:1
books:author:Ali:page:1

### Problem with JSON.stringify(req.query)

```js
const cacheKey = `books:${JSON.stringify(req.query)}`;
````

Issue:

/books?author=John&page=1
/books?page=1&author=John

Dono logically same request hain, lekin query parameter order different hone ki wajah se different cache keys ban sakti hain.

### Better Approach

```js
const sortedQuery = Object.keys(req.query)
  .sort()
  .map((key) => `${key}:${req.query[key]}`)
  .join(":");

const cacheKey = sortedQuery
  ? `books:${sortedQuery}`
  : "books";
```

Ab dono requests ki same cache key banegi:

books:author:John:page:1

## 2. Dynamic Cache Invalidation

Dynamic cache keys:

books:author:John:page:1
books:author:Ali:page:1
books:page:2

Sirf:

```js
await redisClient.del("books");
```

delete karna enough nahi hai.

Create, update ya delete ke baad related dynamic cache keys bhi invalidate karni hongi.

## 3. KEYS vs SCAN

### KEYS

```js
const keys = await redisClient.keys("books:*");
```

Small project mein theek hai, lekin production mein large number of keys ke sath expensive/blocking ho sakta hai.

### SCAN

Production-friendly approach:

```js
for await (const keys of redisClient.scanIterator({
  MATCH: "books:*",
})) {
  if (keys.length > 0) {
    await redisClient.del(keys);
  }
}
```

Agar default cache key bhi use ho rahi hai:

```js
await redisClient.del("books");

for await (const keys of redisClient.scanIterator({
  MATCH: "books:*",
})) {
  if (keys.length > 0) {
    await redisClient.del(keys);
  }
}
```

## 4. Cache Invalidation Flow

GET Request
↓
Cache MISS
↓
MongoDB
↓
Redis Cache Save

Same GET Request
↓
Cache HIT

POST / Update / Delete
↓
Invalidate Related Cache Keys

Next GET
↓
Cache MISS
↓
MongoDB se fresh data
↓
Redis mein new cache

## 5. Docker vs Local Service Hostnames

Docker ke andar:

App → mongodb
App → redis

Local Node.js app:

MongoDB → 127.0.0.1:27018
Redis → 127.0.0.1:6380

Docker service names:

mongodb
redis

sirf Docker network ke andar resolve hote hain.

## 6. Docker MongoDB Port Mapping

Local MongoDB already port 27017 use kar rahi thi.

Docker MongoDB ko alag port diya:

```yaml
mongodb:
  ports:
    - "27018:27017"
```

Meaning:

localhost:27018
↓
Docker MongoDB:27017

Compass connections:

Local MongoDB:
mongodb://localhost:27017

Docker MongoDB:
mongodb://localhost:27018

## 7. Important Debugging Lesson

Agar local Node app aur Docker app dono same port use kar rahe hon:

localhost:4000

To request unexpected app/container ko ja sakti hai.

Check:

```bash
docker compose ps
```

Agar local nodemon test karna ho aur Docker app port use kar rahi ho:

```bash
docker compose stop app
```

## Key Takeaways

* Different query/data variations → different cache keys
* Same logical request → same deterministic cache key
* Dynamic cache keys ko invalidate bhi properly karna hota hai
* Production mein KEYS ke bajaye SCAN prefer karna chahiye
* Docker service hostname aur localhost ka context different hota hai
* Port conflicts mein check karo service actually kahan run ho rahi hai


Bilkul. **Last MD notes ke baad se abhi tak ke important points** ko compact notes mein rakh raha hoon:

# Redis — Important Notes

## 1. Cache Stampede

Jab cache expire/miss hota hai aur ek hi time par bohat saari requests MongoDB ko hit karti hain, usay **Cache Stampede** kehte hain.

### Lock

Redis lock use karke sirf **ek request** database se data fetch karti hai.

```js
const lock = await redisClient.set(lockKey, lockToken, {
  NX: true,
  EX: 10,
});
```

* `NX` → lock sirf tab create hoga jab exist nahi karta
* `EX` → lock automatically expire hoga
* `lockToken` → unique ownership token

Agar lock na mile:

* cache dobara check
* short wait
* limited retries
* cache phir bhi na mile to fallback DB

### Safe Lock Release

Lock ko blindly delete nahi karna, kyunki lock expire hone ke baad doosri request naya lock le sakti hai.

Unique token se verify karke release karna safer hai.

## 2. TTL Jitter

Sab cache keys ek hi waqt expire na hon, isliye TTL mein random variation add karte hain.

```js
const baseTTL = 60;
const jitter = Math.floor(Math.random() * 20);
const ttl = baseTTL + jitter;
```

TTL approximately **60–79 seconds** ho jayega.

Useful especially jab bohat saari cache keys hon.

## 3. Rate Limiting

Rate limiter API requests ko control karta hai.

Example:

```text
100 requests / 60 seconds
```

Limit cross hone par:

```text
HTTP 429
Too Many Requests
```

### Sliding Window

Fixed Window ki boundary problem avoid karne ke liye **Sliding Window** use kiya.

Redis **Sorted Set (ZSET)** mein requests ke timestamps store kiye:

* `ZADD` → request add
* `ZREMRANGEBYSCORE` → old requests remove
* `ZCARD` → current requests count
* `EXPIRE` → Redis key cleanup

### Lua Script

Remove → Add → Count → Decision ko atomic banaya.

Current testing:

```js
const LIMIT = 3;
```

Result:

```text
1st → 1 → Allow
2nd → 1 → Allow
3rd → 1 → Allow
4th → 0 → Block
```

Production example:

```js
const LIMIT = 100;
```

## 4. Redis Pub/Sub

Pub/Sub mein:

```text
Publisher
   ↓
Redis Channel
   ↓
Subscriber
```

Publisher message send karta hai:

```js
await redisClient.publish("book-events", message);
```

Subscriber channel listen karta hai:

```js
await subscriber.subscribe("book-events", callback);
```

### Book Store Implementation

Book create hone par:

```text
POST /books
   ↓
Book Created
   ↓
PUBLISH "book-events"
   ↓
Subscriber
   ↓
Email/Notification action
```

Event example:

```js
{
  type: "BOOK_CREATED",
  bookId: "...",
  title: "joe"
}
```

### Important

**BullMQ vs Pub/Sub:**

* **BullMQ** → reliable background jobs / queues
* **Pub/Sub** → real-time event/message distribution

Pub/Sub subscriber offline ho to normally missed message ko baad mein queue ki tarah process nahi karta.

