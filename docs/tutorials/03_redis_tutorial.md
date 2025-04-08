
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
