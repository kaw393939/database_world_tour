# Redis Quick Start Tutorial (Docker Compose)

This tutorial guides you through connecting to the Redis instance running via Docker Compose and performing basic key-value operations.

**Prerequisites:**

*   Docker and Docker Compose installed.
*   The Docker Compose services are running (`docker compose up -d` in the project root).

**Connection Details (from `docker-compose.yml`):**

*   **Host:** `localhost`
*   **Port:** `6379`
*   **Password:** None set by default in this configuration.

## Connecting with `redis-cli`

You can connect using the `redis-cli` command-line interface, either installed locally or via the container:

```bash
# Option 1: If redis-cli is installed locally
redis-cli -h localhost -p 6379

# Option 2: Connect via the running container
docker exec -it redis_cache redis-cli
```

You should see a prompt like `127.0.0.1:6379>`.

## Basic Operations

1.  **Set a Key (Create/Update):**
    *   Set a simple string value:
        ```redis
        SET user:1:name "Alice"
        ```
        (Output: `OK`)
    *   Set a key with an expiration time (in seconds, e.g., 60 seconds):
        ```redis
        SET temporary:data "some value" EX 60
        ```
        (Output: `OK`)

2.  **Get a Key (Read):**
    ```redis
    GET user:1:name
    ```
    (Output: `"Alice"`)

    ```redis
    GET non_existent_key
    ```
    (Output: `(nil)`)

3.  **Check if a Key Exists:**
    ```redis
    EXISTS user:1:name
    ```
    (Output: `(integer) 1`) - 1 means true

    ```redis
    EXISTS non_existent_key
    ```
    (Output: `(integer) 0`) - 0 means false

4.  **Delete a Key:**
    ```redis
    DEL user:1:name
    ```
    (Output: `(integer) 1`) - Number of keys deleted

5.  **Working with Hashes (Object-like structures):**
    *   Set multiple fields in a hash:
        ```redis
        HSET user:2 name "Bob" email "bob@example.com"
        ```
        (Output: `(integer) 2`) - Number of fields added
    *   Get a specific field from a hash:
        ```redis
        HGET user:2 name
        ```
        (Output: `"Bob"`)
    *   Get all fields from a hash:
        ```redis
        HGETALL user:2
        ```
        (Output: `1) "name"
                 2) "Bob"
                 3) "email"
                 4) "bob@example.com"`) - Key-value pairs flattened

6.  **Working with Lists:**
    *   Add elements to the right end of a list:
        ```redis
        RPUSH mylist "item1"
        RPUSH mylist "item2"
        ```
    *   Get elements from a list (e.g., all elements):
        ```redis
        LRANGE mylist 0 -1
        ```

7.  **Exit `redis-cli`:**
    ```redis
    exit
    ```

This covers some fundamental operations in Redis.

## Further Learning & Tutorial Prompts

Use the following prompts to generate more detailed tutorials building on this foundation.

### Create Tutorial: Redis Data Structures (Sets, Sorted Sets)

**Prompt:**

```text
Create a new tutorial file named `docs/tutorials/03a_redis_data_structures.md`.

**Title:** Redis Tutorial: Working with Sets and Sorted Sets

**Content:**

Following the structure of `03_redis_tutorial.md`, create a tutorial focusing on **Redis Sets and Sorted Sets**, using the existing Docker Compose setup.

*   **Introduction:** Explain Sets (unique unordered elements) and Sorted Sets (unique elements ordered by score).
*   **Prerequisites:** Refer back to the Docker setup in `03_redis_tutorial.md`.
*   **Examples (Sets):** Provide `redis-cli` examples for:
    *   Adding members (`SADD`).
    *   Listing members (`SMEMBERS`).
    *   Checking membership (`SISMEMBER`).
    *   Set operations (`SUNION`, `SINTER`, `SDIFF`).
    *   Getting cardinality (`SCARD`).
    *   Removing members (`SREM`).
*   **Examples (Sorted Sets):** Provide `redis-cli` examples for:
    *   Adding members with scores (`ZADD`).
    *   Listing members by range/rank (`ZRANGE`, `ZREVRANGE` - with scores).
    *   Getting score (`ZSCORE`).
    *   Getting cardinality (`ZCARD`).
    *   Getting members by score range (`ZRANGEBYSCORE`).
    *   Incrementing score (`ZINCRBY`).
    *   Removing members (`ZREM`).
*   **Explanation:** Explain the syntax and purpose of each command.
*   **Use Cases:** Provide typical use cases (e.g., Sets for tagging, unique visitor tracking; Sorted Sets for leaderboards, priority queues).
*   **Link Back:** Include links to this tutorial (`03_redis_tutorial.md`) and the main Key-Value Stores doc (`../03_key_value_stores.md`).
```

### Create Tutorial: Redis Persistence

**Prompt:**

```text
Create a new tutorial file named `docs/tutorials/03b_redis_persistence.md`.

**Title:** Redis Tutorial: Understanding Persistence (RDB vs AOF)

**Content:**

Following the structure of `03_redis_tutorial.md`, create a tutorial explaining **Redis Persistence Options**, using the existing Docker Compose setup.

*   **Introduction:** Explain why persistence is needed and introduce the two main methods: RDB and AOF.
*   **Prerequisites:** Refer back to the Docker setup in `03_redis_tutorial.md`.
*   **RDB (Snapshotting):**
    *   Explain how RDB works (point-in-time snapshots).
    *   Show configuration directives (`save <seconds> <changes>`).
    *   Demonstrate manual save (`SAVE`, `BGSAVE`).
    *   Discuss Pros/Cons (compact, faster restarts vs. potential data loss).
*   **AOF (Append Only File):**
    *   Explain how AOF works (logs every write operation).
    *   Show configuration directives (`appendonly yes`, `appendfsync everysec/always/no`).
    *   Discuss Pros/Cons (more durable vs. larger file size, potentially slower restart).
*   **Configuration:** Show how to modify the `redis.conf` file (or pass config via command line/Docker) to enable and configure these options. *Note: The current docker-compose doesn't explicitly mount a config file, explain how one might do that or use `CONFIG SET` where applicable.*
*   **Which to Choose?:** Briefly discuss common strategies (e.g., using both).
*   **Link Back:** Include links to this tutorial (`03_redis_tutorial.md`) and the main Key-Value Stores doc (`../03_key_value_stores.md`).
```

### Create Tutorial: Redis Transactions

**Prompt:**

```text
Create a new tutorial file named `docs/tutorials/03c_redis_transactions.md`.

**Title:** Redis Tutorial: Using Transactions (MULTI/EXEC)

**Content:**

Following the structure of `03_redis_tutorial.md`, create a tutorial focusing on **Redis Transactions**, using the existing Docker Compose setup.

*   **Introduction:** Explain the concept of transactions in Redis (grouping commands for atomic execution).
*   **Prerequisites:** Refer back to the Docker setup in `03_redis_tutorial.md`.
*   **Examples:** Provide `redis-cli` examples demonstrating:
    *   Starting a transaction (`MULTI`).
    *   Queueing commands (e.g., `SET`, `INCR`, `RPUSH`) - show the `QUEUED` reply.
    *   Executing the transaction (`EXEC`) - show the results array.
    *   Discarding a transaction (`DISCARD`).
    *   Handling errors within a transaction (syntax errors vs. runtime errors).
    *   Using `WATCH` for optimistic locking (check-and-set behavior).
*   **Explanation:** Explain atomicity (all or nothing execution), lack of rollback on runtime errors, and the purpose of `WATCH`.
*   **Use Cases:** Discuss scenarios where grouping commands is beneficial.
*   **Link Back:** Include links to this tutorial (`03_redis_tutorial.md`) and the main Key-Value Stores doc (`../03_key_value_stores.md`).
```

*(Add similar prompts for Pub/Sub, Lua Scripting, etc. as needed)*

---
*Back to [Key-Value Stores](../03_key_value_stores.md)*
