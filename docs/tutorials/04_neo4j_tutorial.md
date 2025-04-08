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

## Further Learning & Tutorial Prompts

Use the following prompts to generate more detailed tutorials building on this foundation.

### Create Tutorial: Advanced Cypher Querying

**Prompt:**

```text
Create a new tutorial file named `docs/tutorials/04a_neo4j_advanced_cypher.md`.

**Title:** Neo4j Tutorial: Advanced Cypher Querying

**Content:**

Following the structure of `04_neo4j_tutorial.md`, create a tutorial focusing on **Advanced Cypher Clauses and Patterns**, using the existing Docker Compose setup and the graph created previously.

*   **Introduction:** Explain how advanced Cypher enables more complex graph traversals and manipulations.
*   **Prerequisites:** Refer back to the Docker setup and the graph created in `04_neo4j_tutorial.md`. Add more nodes and relationships (e.g., more people, cities, relationships like `WORKS_AT`, `VISITED`) for richer examples.
*   **Examples:** Provide Cypher examples (for Neo4j Browser or `cypher-shell`) demonstrating:
    *   Variable-length paths (`MATCH (a)-[:KNOWS*1..3]->(b)`).
    *   Optional matching (`OPTIONAL MATCH`).
    *   Conditional expressions (`CASE WHEN ... THEN ... ELSE ... END`).
    *   Working with lists and aggregations (`collect()`, `count()`, `avg()`, `sum()`).
    *   Merging data (`MERGE`) - creating nodes/relationships if they don't exist.
    *   Combining results (`UNION`, `UNION ALL`).
    *   Using parameters (`$paramName`).
*   **Explanation:** Explain the syntax and purpose of each clause/function.
*   **Use Cases:** Provide scenarios where these advanced features are useful.
*   **Link Back:** Include links to this tutorial (`04_neo4j_tutorial.md`) and the main Graph Databases doc (`../04_graph_databases.md`).
```

### Create Tutorial: Neo4j Indexing and Constraints

**Prompt:**

```text
Create a new tutorial file named `docs/tutorials/04b_neo4j_indexing_constraints.md`.

**Title:** Neo4j Tutorial: Indexing and Constraints

**Content:**

Following the structure of `04_neo4j_tutorial.md`, create a tutorial focusing on **Indexes and Constraints in Neo4j**, using the existing Docker Compose setup.

*   **Introduction:** Explain the role of indexes for performance and constraints for data integrity.
*   **Prerequisites:** Refer back to the Docker setup and the graph created in `04_neo4j_tutorial.md`.
*   **Examples (Indexes):** Provide Cypher examples demonstrating:
    *   Creating single-property indexes (`CREATE INDEX ON :Label(property)`).
    *   Creating composite indexes (`CREATE INDEX ON :Label(prop1, prop2)`).
    *   Using `EXPLAIN` or `PROFILE` to see index usage in queries.
    *   Showing existing indexes (`SHOW INDEXES`).
    *   Dropping indexes (`DROP INDEX`).
*   **Examples (Constraints):** Provide Cypher examples demonstrating:
    *   Creating unique property constraints (`CREATE CONSTRAINT ON (n:Label) ASSERT n.property IS UNIQUE`).
    *   Creating node key constraints (`CREATE CONSTRAINT ON (n:Label) ASSERT (n.prop1, n.prop2) IS NODE KEY`).
    *   Creating relationship property existence constraints.
    *   Showing existing constraints (`SHOW CONSTRAINTS`).
    *   Dropping constraints (`DROP CONSTRAINT`).
*   **Explanation:** Explain the syntax, purpose, and implications of different index and constraint types (especially how constraints often create backing indexes).
*   **Link Back:** Include links to this tutorial (`04_neo4j_tutorial.md`) and the main Graph Databases doc (`../04_graph_databases.md`).
```

### Create Tutorial: Neo4j Graph Data Modeling

**Prompt:**

```text
Create a new tutorial file named `docs/tutorials/04c_neo4j_data_modeling.md`.

**Title:** Neo4j Tutorial: Basic Graph Data Modeling

**Content:**

Following the structure of `04_neo4j_tutorial.md`, create a conceptual tutorial focusing on **Graph Data Modeling Best Practices in Neo4j**.

*   **Introduction:** Explain that effective graph querying starts with good modeling. Contrast with relational modeling.
*   **Prerequisites:** Refer back to the Docker setup for potential experimentation.
*   **Core Concepts:**
    *   Nodes as Entities, Relationships as Connections/Verbs.
    *   Properties on Nodes and Relationships.
    *   Using Labels effectively.
    *   Relationship Directionality.
*   **Modeling Examples/Patterns:** Discuss and potentially show Cypher stubs for common scenarios:
    *   Representing Hierarchies (e.g., reports-to structure).
    *   Modeling Many-to-Many relationships (directly, or using intermediate nodes).
    *   Handling Time (e.g., properties on relationships, time-tree models).
    *   Versioning Data.
*   **Anti-Patterns:** Briefly mention common pitfalls (e.g., overly generic relationships, treating nodes like relational tables).
*   **Link Back:** Include links to this tutorial (`04_neo4j_tutorial.md`) and the main Graph Databases doc (`../04_graph_databases.md`).
```

*(Add similar prompts for APOC, Graph Algorithms, Drivers, etc. as needed)*

---
*Back to [Graph Databases](../04_graph_databases.md)*
