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

## Further Learning & Tutorial Prompts

Use the following prompts to generate more detailed tutorials building on this foundation.

### Create Tutorial: PostgreSQL Data Types

**Prompt:**

```text
Create a new tutorial file named `docs/tutorials/01a_postgres_data_types.md`.

**Title:** PostgreSQL Tutorial: Data Types

**Content:**

Following the structure of `01_postgres_tutorial.md`, create a tutorial focusing on **Common PostgreSQL Data Types**, using the existing Docker Compose setup.

*   **Introduction:** Briefly explain the importance of choosing correct data types.
*   **Prerequisites:** Refer back to the Docker setup in `01_postgres_tutorial.md`.
*   **Examples:** Provide `psql` examples for creating tables and inserting data using various types:
    *   Numeric types (`INTEGER`, `BIGINT`, `NUMERIC`/`DECIMAL`, `REAL`, `DOUBLE PRECISION`, `SERIAL`)
    *   Character types (`VARCHAR(n)`, `CHAR(n)`, `TEXT`)
    *   Date/Time types (`TIMESTAMP`, `DATE`, `TIME`, `INTERVAL`)
    *   Boolean type (`BOOLEAN`)
    *   JSON types (`JSON`, `JSONB` - highlight differences)
    *   Array types (e.g., `INTEGER[]`)
*   **Explanation:** Explain the purpose and common use cases for each type demonstrated.
*   **Link Back:** Include links to this tutorial (`01_postgres_tutorial.md`) and the main Relational Databases doc (`../01_relational_databases.md`).
```

### Create Tutorial: PostgreSQL Indexing

**Prompt:**

```text
Create a new tutorial file named `docs/tutorials/01b_postgres_indexing.md`.

**Title:** PostgreSQL Tutorial: Indexing Basics

**Content:**

Following the structure of `01_postgres_tutorial.md`, create a tutorial focusing on **Basic Indexing in PostgreSQL**, using the existing Docker Compose setup and the `cities` table example.

*   **Introduction:** Explain why indexing is crucial for query performance.
*   **Prerequisites:** Refer back to the Docker setup and the table created in `01_postgres_tutorial.md`.
*   **Examples:** Provide `psql` examples demonstrating:
    *   Creating a simple B-tree index (`CREATE INDEX`).
    *   Analyzing query performance before and after indexing (using `EXPLAIN ANALYZE`).
    *   Creating a multi-column index.
    *   Creating a unique index.
    *   Listing existing indexes.
    *   Dropping an index (`DROP INDEX`).
*   **Explanation:** Explain the syntax and purpose of each command.
*   **Use Cases:** Briefly discuss when to use different index types (mentioning others like Hash, GiST, GIN briefly).
*   **Link Back:** Include links to this tutorial (`01_postgres_tutorial.md`) and the main Relational Databases doc (`../01_relational_databases.md`).
```

### Create Tutorial: PostgreSQL Transactions

**Prompt:**

```text
Create a new tutorial file named `docs/tutorials/01c_postgres_transactions.md`.

**Title:** PostgreSQL Tutorial: ACID Transactions

**Content:**

Following the structure of `01_postgres_tutorial.md`, create a tutorial focusing on **ACID Transactions in PostgreSQL**, using the existing Docker Compose setup.

*   **Introduction:** Explain the concept of ACID properties (Atomicity, Consistency, Isolation, Durability) and why transactions are important.
*   **Prerequisites:** Refer back to the Docker setup in `01_postgres_tutorial.md`.
*   **Examples:** Provide `psql` examples demonstrating:
    *   Starting a transaction (`BEGIN` or `START TRANSACTION`).
    *   Performing multiple operations (e.g., INSERT, UPDATE).
    *   Committing a transaction (`COMMIT`).
    *   Rolling back a transaction (`ROLLBACK`).
    *   Using savepoints (`SAVEPOINT`, `ROLLBACK TO SAVEPOINT`, `RELEASE SAVEPOINT`).
*   **Explanation:** Explain the behavior of operations within a transaction block and the effect of commit/rollback.
*   **Use Cases:** Discuss scenarios where explicit transaction control is essential.
*   **Link Back:** Include links to this tutorial (`01_postgres_tutorial.md`) and the main Relational Databases doc (`../01_relational_databases.md`).
```

*(Add similar prompts for Joins, User Management, Backup/Restore as needed)*

---
*Back to [Relational Databases](../01_relational_databases.md)*
