# Caching in System Design

## Locality of Reference Principle

Caching takes advantage of the **locality of reference** principle, which states that recently requested data is likely to be requested again. This principle underpins many caching strategies and is key to optimizing system performance.

### Example Around You

- **Music Streaming:** When you listen to a song on a music streaming app like Spotify, the app temporarily caches the song data on your device. If you play the song again, it loads instantly from the cache, saving time and reducing data usage.

- **Social Media:** As you scroll through a social media app, the posts, images, and videos you view are cached. If you revisit them later, they load instantly, making your browsing experience faster and more seamless.

- **Food Delivery:** When you open a food delivery app, it caches the list of nearby restaurants from your previous session. The next time you use the app, the restaurant list appears instantly, allowing you to place your order faster without waiting for the data to reload.

### Industry Use Cases/Scenarios

1. **Web Applications:** A popular e-commerce site caches product images and details in memory, reducing the load on the database and speeding up page load times for users.
  
2. **Content Delivery Networks (CDNs):** Global news sites use CDNs to cache static content, such as articles and images, across multiple edge servers. This reduces the distance data must travel to reach users, improving load times and reducing server load.
  
3. **Database Query Caching:** A financial services company pre-calculates and caches complex reports (like daily trading summaries) to ensure that users can access them instantly, rather than waiting for a new query to be run each time.

4. **Social Media Platforms:** Suggested stories or friend recommendations are often pre-generated based on user behavior and cached, so they can be quickly served to users when they log in.

---





## What is Caching?

Caching involves temporarily storing data in a faster storage layer (like memory) to reduce the time it takes to retrieve that data. When a request is made, the system first checks the cache. If the data is found (a "cache hit"), it is returned directly from the cache. If not (a "cache miss"), the system fetches the data from the slower, primary storage, stores it in the cache for future requests, and then returns it.

## Why Use Caching?

- **Performance:** By storing data in memory, which is faster than disk storage, caching can significantly reduce the time it takes to serve requests.
- **Reduced Latency:** Caching brings data closer to the application, reducing the time it takes to retrieve the data.
- **Lower Database Load:** Caching can reduce the number of queries sent to a database, freeing up resources and preventing bottlenecks.
- **Cost Savings:** By reducing the need for expensive disk I/O operations and database queries, caching can lower operational costs.
- **Locality of Reference:** Caching takes advantage of the principle that recently requested data is likely to be requested again, improving efficiency and response times.

---

## Types of Caching


- **Client-Side Caching:** 
  - **Description:** Caching done on the user's device, typically within the browser or a mobile app. It stores assets like images, CSS, and JavaScript files locally.
  - **Benefits:** Reduces the need for repeated downloads of the same assets, speeds up page load times, and lowers network traffic.
  - **Example:** When you visit a website, your browser caches images and stylesheets so that the next time you visit the same site, it loads faster because it doesn't have to re-download these resources.

- **Server-Side Caching:** 
  - **Description:** Caching performed on the server, which includes in-memory caches like Redis or Memcached. This layer stores frequently accessed data to avoid redundant database queries.
  - **Benefits:** Improves response times for data retrieval and reduces the load on databases.
  - **Example:** A web application caches user session data in Redis to quickly serve user information without querying the database each time.

- **Database Caching:** 
  - **Description:** Databases often have internal caching mechanisms to speed up query results by storing frequently accessed data in memory.
    Database caching refers to the internal mechanisms of a database that store query results, frequently accessed data, or index information in memory.


  - **Benefits:** Enhances performance by reducing the need for repeated disk reads and complex query processing.
  - **Example:** SQL databases may cache the results of common queries to quickly return results without re-executing the query.

- **CDN Caching:** 
  - **Description:** Content Delivery Networks cache static content at various edge locations worldwide. This reduces the distance data travels from the server to the user.
  - **Benefits:** Lowers latency, speeds up content delivery for global users, and reduces the load on the origin server.
  - **Example:** A CDN caches images and videos of a popular website, allowing users to load these assets from a nearby edge server rather than the website's central server.

- **Distributed Caching:** 
  - **Description:** In large-scale systems, caching is spread across multiple nodes or servers. This approach handles high volumes of data and traffic, and ensures high availability and reliability.
  - **Benefits:** Provides scalability, improves fault tolerance, and balances the load across multiple cache instances.
  - **Example:** An e-commerce platform uses a distributed cache to store session data and product information across multiple servers, ensuring quick access and consistency even as traffic spikes.

---

## Caching Strategies


## Reading Data

### 🔹 Cache-Aside (Lazy Loading)
- **Process:**
  1. The application first checks the cache for the data.
  2. If the data is in the cache (cache hit), it is returned directly.
  3. If the data is not in the cache (cache miss), the application fetches it from the database.
  4. The fetched data is then stored in the cache for future requests.
 
     ![image](https://github.com/user-attachments/assets/37c21a7f-c37f-45d8-9148-3e599630de1b)

  


### 🔹 Read-Through
- **Process:**
  1. The application requests the data from the cache.
  2. If the data is in the cache, it is returned directly (cache hit).
  3. If the data is not in the cache (cache miss), the cache itself fetches the data from the database.
  4. The fetched data is returned to the application and stored in the cache.

![image](https://github.com/user-attachments/assets/b250d305-ebd6-4462-823d-8022ed40de9a)


## Writing Data

### 🔹 Write-Around
- **Process:**
  1. The application writes the data directly to the database, bypassing the cache.
  2. The cache is updated only when the data is read again.

![image](https://github.com/user-attachments/assets/599a8a04-6b19-4fae-b17d-cc8e1adb282c)


### 🔹 Write-Back (Write-Behind)
- **Process:**
  1. The application writes the data to the cache.
  2. The cache asynchronously writes the data to the database after some time or under specific conditions (e.g., when the cache is about to evict the data).
 
     
  ![image](https://github.com/user-attachments/assets/1fb611ed-fff7-4f8c-bef6-c634f5d49576)


### 🔹 Write-Through
- **Process:**
  1. The application writes the data to both the cache and the database simultaneously.
  2. The data in the cache is always up-to-date with the database.


![image](https://github.com/user-attachments/assets/a02a569d-c9d0-4bbd-9702-cd7e9048afe8)


# When to Use Each Caching Strategy

## Reading Data

### 🔹 Cache-Aside (Lazy Loading)
- **When to Use:**
  - **Simple Caching Needs:** When you want more control over what gets cached and when.
  - **Selective Caching:** When you don’t need all data to be cached, but only certain pieces of data that are frequently accessed.
  - **Data Freshness Isn’t Critical:** If it’s okay for some data to be missing from the cache temporarily, especially if the data doesn’t change often.
  - **Memory Efficiency:** When you want to avoid filling up the cache with data that might never be requested.

### 🔹 Read-Through
- **When to Use:**
  - **Consistent Caching:** When you want the cache to always have the most recent data automatically.
  - **Simplified Code:** When you prefer to simplify the application logic by letting the cache manage the loading of data.
  - **Data Consistency:** When it’s important that the data in the cache is always synchronized with the database.
  - **High Read Load:** When your application has a high read load, and you want to reduce the frequency of cache misses by automating data fetching.

## Writing Data

### 🔹 Write-Around
- **When to Use:**
  - **Read-Heavy Workloads:** When your application reads data much more frequently than it writes data.
  - **Avoiding Cache Pollution:** When you want to prevent the cache from being filled with data that’s written but not frequently accessed.
  - **Infrequent Writes:** When write operations are rare, and the cost of missing cached data is low.

### 🔹 Write-Back (Write-Behind)
- **When to Use:**
  - **High Write Performance:** When write performance is critical, and you can afford some delay in writing data to the database.
  - **Batching Writes:** When you want to batch writes to the database to reduce the load on the database server.
  - **Tolerance for Data Loss:** When your application can tolerate potential data loss in case the cache fails before writing to the database.

### 🔹 Write-Through
- **When to Use:**
  - **Data Consistency:** When it’s crucial to keep the cache and the database in sync at all times.
  - **Simple Consistent Writes:** When you want a simple, consistent approach to writing data where every write is immediately reflected in both the cache and the database.
  - **Frequent Reads After Writes:** When the data being written will be read frequently shortly after being written, ensuring that the data is immediately available in the cache.


---

## Cache Eviction Policies

When the cache is full, old data needs to be removed to make room for new data. This process is called eviction. Common eviction policies include:

- **Least Recently Used (LRU):** Removes the data that hasn't been accessed for the longest time.
- **Least Frequently Used (LFU):** Removes the data that has been accessed the least number of times.
- **First In, First Out (FIFO):** Removes the oldest data, regardless of how often it was accessed.
- **Random Replacement:** Randomly removes data from the cache.

---

## Cache Invalidation

Cache invalidation ensures that the cache does not serve stale data. Common strategies include:

- **Time-to-Live (TTL):** Data is automatically removed from the cache after a certain period.
- **Write Invalidation:** The cache is updated or invalidated whenever the underlying data changes.
- **Manual Invalidation:** Developers manually clear or update the cache based on specific events.

---

## Distributed Caching

In large-scale systems, a single cache may not be enough. Distributed caching involves spreading the cache across multiple nodes to handle large volumes of data and traffic. Key considerations include:

- **Consistency:** Ensuring all nodes have consistent data.
- **Partitioning:** Dividing data across different cache nodes (e.g., using hashing).
- **Replication:** Replicating data across nodes to improve reliability and availability.

---

## Common Caching Tools and Technologies

## In-Memory Caching

### 🔹 Redis
- **Description:** 
  - An open-source, in-memory data structure store, often used as a distributed cache.
  - Supports various data structures like strings, hashes, lists, sets, and more.
  - Provides persistence options for saving data to disk.


### 🔹 Memcached
- **Description:** 
  - An open-source, high-performance, distributed memory caching system.
  - Simple and lightweight, designed for caching results of database queries, API calls, or page rendering


## Distributed Caching

### 🔹 Amazon ElastiCache
- **Description:**
  - A managed caching service by AWS that supports Redis and Memcached.
  - Provides easy setup, scaling, and management for distributed caching in the cloud.

### 🔹 Hazelcast
- **Description:**
  - An open-source in-memory data grid that supports distributed caching, computation, and event processing.
  - Scales horizontally and provides fault tolerance.

## Application-Specific Caching

### 🔹 Ehcache
- **Description:**
  - An open-source Java-based cache used for general-purpose caching in Java applications.
  - Offers various caching strategies, including heap, disk, and distributed caching.


### 🔹 Spring Cache (with Spring Framework)
- **Description:**
  - A caching abstraction provided by the Spring Framework.
  - Supports integration with various caching providers like Redis, Ehcache, and Caffeine.

### 🔹 Caffeine
- **Description:**
  - A high-performance caching library for Java, designed to be a near drop-in replacement for Guava's cache.
  - Provides features like asynchronous loading, automatic eviction, and time-based expiration.

---

## When not to use a cache


- When data changes too frequently and stale data could cause issues.
- When the application has minimal user interaction and caching adds unnecessary complexity.
- When data can be quickly retrieved without caching, making it redundant.
-  When strict data consistency is crucial, and stale data could lead to errors.
-  When frequent writes invalidate the cache, reducing its effectiveness.
-  When caching poses security risks, especially with sensitive information.


---

