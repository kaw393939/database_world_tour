
# PostgreSQL Quick Start Tutorial (Docker Compose)

This tutorial guides you through connecting to the PostgreSQL instance running via Docker Compose and performing basic operations.

**Prerequisites:**

*   Docker and Docker Compose installed.
*   The Docker Compose services are running (`docker compose up -d` in the project root).

**Connection Details (from `docker-compose.yml`):**

*   **Host:** `localhost`
*   **Port:** `5432`
*   **Database:** `tourdb`
*   **User:** `user`
*   **Password:** `examplepassword` (Remember to change this if you updated it!)

## Connecting with `psql`

You can connect using the `psql` command-line tool, either installed locally or via the container:

```bash
# Option 1: If psql is installed locally
psql -h localhost -p 5432 -U user -d tourdb

# Option 2: Connect via the running container
docker exec -it postgres_db psql -U user -d tourdb
```

Enter the password (`examplepassword`) when prompted.

## Basic Operations

Once connected:

1.  **Create a Table:**
    ```sql
    CREATE TABLE cities (
        id SERIAL PRIMARY KEY,
        name VARCHAR(100),
        country VARCHAR(100)
    );
    ```

2.  **Insert Data (Create):**
    ```sql
    INSERT INTO cities (name, country) VALUES
    ('London', 'UK'),
    ('Tokyo', 'Japan'),
    ('New York', 'USA');
    ```

3.  **Query Data (Read):**
    ```sql
    SELECT * FROM cities;

    SELECT name FROM cities WHERE country = 'UK';
    ```

4.  **Update Data:**
    ```sql
    UPDATE cities SET country = 'United Kingdom' WHERE country = 'UK';
    ```

5.  **Delete Data:**
    ```sql
    DELETE FROM cities WHERE name = 'New York';
    ```

6.  **Exit `psql`:**
    ```sql
    \q
    ```

This covers the fundamental CRUD operations in PostgreSQL.
