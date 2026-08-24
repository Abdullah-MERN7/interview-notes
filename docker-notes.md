# Docker Notes

## 1. Docker kya hai?

Docker application ko uske required environment ke saath container mein run karne mein help karta hai.

Code + Runtime + Dependencies → Container

### GitHub vs Docker

**GitHub:**

* Code
* Package versions

**Docker:**

* Runtime environment
* Services
* Networking
* Isolation

Example:

App
├── Node.js
├── MongoDB
└── Redis

Developer ko manually Node.js, MongoDB aur Redis install karne ki zarurat nahi hoti. Docker Compose containers manage karta hai.

## 2. Dockerfile

Dockerfile image banane ki recipe hoti hai.

```dockerfile
FROM node:22-alpine

WORKDIR /app

COPY package*.json ./

RUN npm ci --omit=dev

COPY src ./src

USER node

CMD ["node", "src/app.js"]
```

## 3. Production Dependencies

Production image mein unnecessary development dependencies nahi honi chahiye.

* Development dependencies ❌
* Production dependencies ✅

Build:

```bash
docker build -t bookstore-app .
```

## 4. Docker Compose

Multiple services ko ek saath run aur manage karne ke liye Docker Compose use hota hai.

App
├── MongoDB
└── Redis

Run:

```bash
docker compose up
```

Background mein:

```bash
docker compose up -d
```

`-d` = Detached Mode. Containers background mein run hote hain aur terminal free rehta hai.

## 5. Service Names = Hostnames

Docker Compose mein:

```yaml
services:
  mongodb:
  redis:
```

App:

```env
MONGO_URI=mongodb://mongodb:27017/bookstore
REDIS_HOST=redis
```

Service names hostname ki tarah use hote hain.

`localhost` use nahi karte kyunki har container ka apna separate environment hota hai.

App Container
├── mongodb → MongoDB Container
└── redis → Redis Container

## 6. Healthcheck

Healthcheck check karta hai ke service sirf start nahi hui, balki properly respond bhi kar rahi hai.

### Redis

```yaml
healthcheck:
  test: ["CMD", "redis-cli", "ping"]
  interval: 5s
  timeout: 3s
  retries: 5
```

### MongoDB

```yaml
healthcheck:
  test: ["CMD", "mongosh", "--eval", "db.adminCommand('ping')"]
  interval: 5s
  timeout: 3s
  retries: 5
```

## 7. Volumes

Volume container ke bahar data persist karta hai.

```yaml
volumes:
  - mongo-data:/data/db
```

Container delete → Volume remains → Data remains

Without volume:

Container removed → Data can be lost

## 8. `docker compose down` vs `docker compose down -v`

### Normal down

```bash
docker compose down
```

* Containers removed
* Network removed
* Named volumes remain
* Data remains

### Down with volumes

```bash
docker compose down -v
```

* Containers removed
* Volumes removed
* Data deleted

Fresh MongoDB data:

```bash
docker compose down -v
docker compose up -d
```

## 9. Docker Hub

Docker image ko registry par store aur share karne ke liye Docker Hub use hota hai.

Local Code → Docker Image → Docker Hub → Server / Production

Image tag:

```bash
docker tag bookstore-app:v1 abdullahdev904/bookstore-app:v1
```

Push:

```bash
docker push abdullahdev904/bookstore-app:v1
```

## 10. Production Compose

Development:

```yaml
build: .
```

Production:

```yaml
image: abdullahdev904/bookstore-app:v1
```

Production server existing image use karta hai, isliye source code se dobara image build karne ki zarurat nahi hoti.

## 11. Image Versioning

```text
bookstore-app:v1
bookstore-app:v2
```

Har version ek specific application image ko represent karta hai.

## 12. Rollback

Scenario:

v1 → Working ✅
v2 → Bug ❌

Rollback:

```yaml
image: abdullahdev904/bookstore-app:v1
```

Phir:

```bash
docker compose -f docker-compose.prod.yml up -d
```

v2 → v1

Rollback ke liye image dobara build karna zaruri nahi hota agar previous version Docker Hub par available ho.

## 13. Docker ka Real-World Use

### Local Development

Developer A → App + MongoDB + Redis

Developer B → App + MongoDB + Redis

Har developer ke apne containers aur apna local data ho sakta hai.

### Shared Database

Developer A ─┐
Developer B ─┼──→ Shared MongoDB
Developer C ─┘

### Production

App Container → Managed MongoDB / Managed Redis

Docker har service ko container mein run karna compulsory nahi hai.

## 14. GitHub vs Docker

`package-lock.json` ke saath:

GitHub → Code same + npm package versions same

Docker:

* Code
* Node.js runtime
* MongoDB
* Redis
* Networking
* Environment

**Simple:**

> GitHub project ka code deta hai, Docker project ko chalane ka same environment provide karta hai.

## 15. Book Store Project Implementation

Is project mein implement kiya:

* Dockerfile
* Production dependencies
* Docker Compose
* MongoDB container
* Redis container
* Healthchecks
* Named MongoDB volume
* Docker networking
* Service names as hostnames
* Docker Hub image push
* Image versioning
* `v1 → v2` deployment
* `v2 → v1` rollback
* Production Compose setup
