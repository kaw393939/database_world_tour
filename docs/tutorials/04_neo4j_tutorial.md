
# Neo4j Quick Start Tutorial (Docker Compose)

This tutorial guides you through connecting to the Neo4j instance running via Docker Compose and performing basic graph operations using Cypher.

**Prerequisites:**

*   Docker and Docker Compose installed.
*   The Docker Compose services are running (`docker compose up -d` in the project root).

**Connection Details (from `docker-compose.yml`):**

*   **Bolt URL:** `neo4j://localhost:7687`
*   **HTTP URL (Browser):** `http://localhost:7474`
*   **User:** `neo4j`
*   **Password:** `examplepassword` (Remember to change this if you updated it!)

## Connecting

There are two primary ways to interact:

1.  **Neo4j Browser:** Open `http://localhost:7474` in your web browser. You'll be prompted to connect. Use the Bolt URL (`neo4j://localhost:7687`), user (`neo4j`), and password (`examplepassword`). This provides a visual interface for running queries and exploring the graph.

2.  **`cypher-shell`:** Connect using the command-line tool via the container:
    ```bash
    docker exec -it neo4j_db cypher-shell -u neo4j -p examplepassword -a neo4j://localhost:7687
    ```

## Basic Operations (Cypher Queries)

Run these queries in the Neo4j Browser or `cypher-shell`.

1.  **Create Nodes (Entities):**
    *   Create a Person node:
        ```cypher
        CREATE (p:Person {name: 'Alice', born: 1990});
        ```
    *   Create another Person node:
        ```cypher
        CREATE (p:Person {name: 'Bob', born: 1992});
        ```
    *   Create a City node:
        ```cypher
        CREATE (c:City {name: 'London'});
        ```

2.  **Create Relationships:**
    *   Create a `LIVES_IN` relationship between Alice and London:
        ```cypher
        MATCH (a:Person {name: 'Alice'}), (c:City {name: 'London'})
        CREATE (a)-[r:LIVES_IN]->(c);
        ```
    *   Create a `KNOWS` relationship between Alice and Bob:
        ```cypher
        MATCH (a:Person {name: 'Alice'}), (b:Person {name: 'Bob'})
        CREATE (a)-[r:KNOWS {since: 2015}]->(b);
        ```

3.  **Query Data (Read):**
    *   Find all Person nodes:
        ```cypher
        MATCH (p:Person) RETURN p;
        ```
    *   Find the person named 'Alice':
        ```cypher
        MATCH (p:Person {name: 'Alice'}) RETURN p;
        ```
    *   Find who Alice knows:
        ```cypher
        MATCH (a:Person {name: 'Alice'})-[:KNOWS]->(friend)
        RETURN friend.name;
        ```
    *   Find who lives in London:
        ```cypher
        MATCH (p:Person)-[:LIVES_IN]->(c:City {name: 'London'})
        RETURN p.name;
        ```

4.  **Update Data:**
    *   Add a property to Bob:
        ```cypher
        MATCH (p:Person {name: 'Bob'})
        SET p.email = 'bob@example.com';
        ```

5.  **Delete Data:**
    *   Delete the `KNOWS` relationship between Alice and Bob:
        ```cypher
        MATCH (a:Person {name: 'Alice'})-[r:KNOWS]->(b:Person {name: 'Bob'})
        DELETE r;
        ```
    *   Delete Bob (Note: Must delete relationships first):
        ```cypher
        // First, delete any remaining relationships connected to Bob
        // MATCH (p:Person {name: 'Bob'})-[r]-() DELETE r;
        // Then, delete the node itself
        MATCH (p:Person {name: 'Bob'}) DELETE p;
        ```
        *Simplified delete (Neo4j 4.x+):*
        ```cypher
        MATCH (p:Person {name: 'Bob'}) DETACH DELETE p;
        ```

6.  **Exit `cypher-shell`:**
    Type `:exit`

This covers fundamental graph creation and querying operations in Neo4j using Cypher.
