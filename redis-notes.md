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

