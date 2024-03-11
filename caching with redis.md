# Caching with Redis

- [Why need caching?](#why-need-caching)
- [What is Redis?](#what-is-redis)
  - [Start Redis Server](#start-redis-server)
  - [Basic Node.js Application](#basic-nodejs-application)
  - [Install Redis Dependency and Connect to Redis](#install-redis-dependency-and-connect-to-redis)
  - [Caching Functionality](#caching-functionality)
  - [Clean Cache Middleware](#clean-cache-middleware)

# Why need caching?

- Caching is a technique to store a copy of the data in a faster storage system (i.e. cache) to speed up the data retrieval.

- Caching is used to store the data that the users frequently access. It helps reduce the load on the main storage system and improves the application's performance.

# What is Redis?

- Redis is an open-source in-memory data structure store that can be used as a database, cache, and message broker.

- It supports various data structures such as strings, hashes, lists, sets, sorted sets, bitmaps, hyperloglogs, and geospatial indexes with radius queries.

## Start Redis Server

- If you have not installed Redis, you can use <https://console.upstash.com/> to create a Redis server.

- Get the connection string from the dashboard.

## Basic Node.js Application

- Create a new node.js application with express.

- Or you can use my node starter template [Node-ENV](https://github.com/Adosh74/Node-Env)

## Install Redis Dependency and Connect to Redis

- Install the `redis` package using yarn.

```bash
yarn add ioredis @types/ioredis
```

note: i use `yarn` because it's faster than npm and can install packages in parallel.

- serve the Redis server connection string in the `.env` file or use the connection string directly in the code.

- Create a new file `redis.ts` and connect to the Redis server.

```typescript
import dotenv from 'dotenv';
import Redis from 'ioredis';
import { LOGGER } from '../logging';

dotenv.config({ path: `${process.cwd()}/.env` });

const { REDIS_URL } = process.env;

if (!REDIS_URL) {
 LOGGER.error('Please make sure that you have a valid Redis URL in your .env file');
 process.exit(1);
}

export const client = new Redis(REDIS_URL);

client.on('connect', () => {
 LOGGER.info('Connected to Redis');
});

client.on('error', (err) => {
 LOGGER.error(`Redis error: ${err}`);
 process.exit(1);
});
```

If you aren't familiar with logging, you can use `console.log` instead.

## Caching Functionality

- Create a new file `cache.ts` and implement the caching functionality.

```typescript
import mongoose, { Document } from 'mongoose';
import { client } from '../database/redis';

declare module 'mongoose' {
 interface Query<ResultType, DocType, THelpers, RawDocType = DocType> {
  useCache: boolean;
  hashKey: string;
  cache(options?: { key?: string }): this;
 }
}

const exec: typeof mongoose.Query.prototype.exec = mongoose.Query.prototype.exec;

mongoose.Query.prototype.cache = function (options = {}) {
 this.useCache = true;
 this.hashKey = JSON.stringify(options.key || '');
 return this;
};

mongoose.Query.prototype.exec = async function <T extends Document>(): Promise<T[]> {
 if (!this.useCache) {
  return exec.call(this);
 }

 const key = JSON.stringify(
  Object.assign({}, this.getQuery(), {
   collection: this.model.collection.name,
  })
 );

 const cacheValue = await client.hget(this.hashKey, key);

 if (cacheValue) {
  const doc = JSON.parse(cacheValue);
  return Array.isArray(doc)
   ? doc.map((d: any) => new this.model(d))
   : [new this.model(doc)];
 }

 const result = await exec.call(this);
 await client.hset(this.hashKey, key, JSON.stringify(result), 'EX', 1000);

 return result;
};

export const clearHash = (hashKey: string): void => {
 client.del(JSON.stringify(hashKey));
};
```

- Let's understand the code above.

- First, we are extending the `mongoose.Query` interface to add the `cache` method.

- The `cache` method is used to enable caching for the query.

- The `hashKey` is used to store the cache data in the Redis server.

- The `exec` method is overridden to implement the caching functionality.

- If the `useCache` is set to `true`, then we check if the data is available in the cache.

- If the data is available in the cache, then we return the data from the cache.

- If the data is not available in the cache, then we execute the original `exec` method and store the data in the cache.

- The `clearHash` method is used to clear the cache data for a specific `hashKey`.

## Clean Cache Middleware

- Create a new file `cleanCache.ts` and implement the clean cache middleware.

```typescript
import { NextFunction, Response } from 'express';
import { clearHash } from '../services/cache.service';

export default async (req: Request, res: Response, next: NextFunction) => {
 await next();
 clearHash((req as any).user.id.toString());
};
```

- Let's understand the code above.

- The `cleanCache` middleware is used to clear the cache data after the request is completed.

- `await next()` is used to execute the next middleware then we use the `clearHash` method to clear the cache data for the specific `hashKey`.

- We are using the `clearHash` method to clear the cache data for the specific `hashKey`.
