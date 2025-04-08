# MongoDB Quick Start Tutorial (Docker Compose)

This tutorial guides you through connecting to the MongoDB instance running via Docker Compose and performing basic operations.

**Prerequisites:**

*   Docker and Docker Compose installed.
*   The Docker Compose services are running (`docker compose up -d` in the project root).

**Connection Details (from `docker-compose.yml`):**

*   **Host:** `localhost`
*   **Port:** `27017`
*   **Authentication Database:** `admin`
*   **User:** `root`
*   **Password:** `examplepassword` (Remember to change this if you updated it!)

## Connecting with `mongosh`

You can connect using the `mongosh` command-line shell, either installed locally or via the container:

```bash
# Option 1: If mongosh is installed locally
mongosh mongodb://root:examplepassword@localhost:27017/admin

# Option 2: Connect via the running container
docker exec -it mongo_db mongosh mongodb://root:examplepassword@localhost:27017/admin
```

## Basic Operations

Once connected:

1.  **Switch to a Database (or create it):**
    ```javascript
    use worldTourDB;
    ```

2.  **Insert Data (Create):**
    *   Insert a single document into a collection named `landmarks`:
        ```javascript
        db.landmarks.insertOne({ name: "Eiffel Tower", city: "Paris", type: "Tower" });
        ```
    *   Insert multiple documents:
        ```javascript
        db.landmarks.insertMany([
          { name: "Colosseum", city: "Rome", type: "Amphitheater" },
          { name: "Statue of Liberty", city: "New York", type: "Statue" }
        ]);
        ```

3.  **Query Data (Read):**
    *   Find all documents in the collection:
        ```javascript
        db.landmarks.find();
        ```
    *   Find specific documents (e.g., landmarks in Rome):
        ```javascript
        db.landmarks.find({ city: "Rome" });
        ```
    *   Find one specific document:
        ```javascript
        db.landmarks.findOne({ name: "Eiffel Tower" });
        ```

4.  **Update Data:**
    *   Update one document (add a country field):
        ```javascript
        db.landmarks.updateOne(
          { name: "Eiffel Tower" },
          { $set: { country: "France" } }
        );
        ```
    *   Update multiple documents (change type for specific city):
        ```javascript
        // Note: This example might not be logical, just demonstrating syntax
        db.landmarks.updateMany(
          { city: "New York" },
          { $set: { type: "Monument" } }
        );
        ```

5.  **Delete Data:**
    *   Delete one document:
        ```javascript
        db.landmarks.deleteOne({ name: "Colosseum" });
        ```
    *   Delete multiple documents:
        ```javascript
        // db.landmarks.deleteMany({ type: "Monument" }); // Example
        ```

6.  **Exit `mongosh`:**
    ```javascript
    exit
    ```

This covers fundamental CRUD operations in MongoDB.

## Further Learning & Tutorial Prompts

Use the following prompts to generate more detailed tutorials building on this foundation.

### Create Tutorial: MongoDB Query Operators

**Prompt:**

```text
Create a new tutorial file named `docs/tutorials/02a_mongodb_query_operators.md`.

**Title:** MongoDB Tutorial: Advanced Query Operators

**Content:**

Following the structure of `02_mongodb_tutorial.md`, create a tutorial focusing on **Advanced Query Operators in MongoDB**, using the existing Docker Compose setup and the `landmarks` collection example.

*   **Introduction:** Explain how query operators allow for more specific document retrieval.
*   **Prerequisites:** Refer back to the Docker setup and the collection created in `02_mongodb_tutorial.md`. Add more diverse data to the `landmarks` collection (e.g., add `visitor_count`, `year_built` fields) to support varied queries.
*   **Examples:** Provide `mongosh` examples demonstrating:
    *   Comparison Operators (`$eq`, `$ne`, `$gt`, `$gte`, `$lt`, `$lte`, `$in`, `$nin`).
    *   Logical Operators (`$and`, `$or`, `$not`, `$nor`).
    *   Element Operators (`$exists`, `$type`).
    *   Array Operators (`$all`, `$elemMatch`, `$size`).
*   **Explanation:** Explain the syntax and purpose of each operator group.
*   **Use Cases:** Provide practical scenarios for using these operators.
*   **Link Back:** Include links to this tutorial (`02_mongodb_tutorial.md`) and the main Document Databases doc (`../02_document_databases.md`).
```

### Create Tutorial: MongoDB Indexing

**Prompt:**

```text
Create a new tutorial file named `docs/tutorials/02b_mongodb_indexing.md`.

**Title:** MongoDB Tutorial: Indexing Fundamentals

**Content:**

Following the structure of `02_mongodb_tutorial.md`, create a tutorial focusing on **Basic Indexing in MongoDB**, using the existing Docker Compose setup and the `landmarks` collection example.

*   **Introduction:** Explain the importance of indexing for query performance in MongoDB.
*   **Prerequisites:** Refer back to the Docker setup and the collection created in `02_mongodb_tutorial.md`.
*   **Examples:** Provide `mongosh` examples demonstrating:
    *   Creating a single-field index (`createIndex`).
    *   Analyzing query performance using `.explain("executionStats")` before and after indexing.
    *   Creating a compound index.
    *   Creating indexes in the background.
    *   Listing existing indexes (`getIndexes`).
    *   Dropping an index (`dropIndex`).
*   **Explanation:** Explain the syntax and purpose of each command.
*   **Use Cases:** Briefly discuss when to use single-field vs. compound indexes.
*   **Link Back:** Include links to this tutorial (`02_mongodb_tutorial.md`) and the main Document Databases doc (`../02_document_databases.md`).
```

### Create Tutorial: MongoDB Aggregation Basics

**Prompt:**

```text
Create a new tutorial file named `docs/tutorials/02c_mongodb_aggregation.md`.

**Title:** MongoDB Tutorial: Aggregation Framework Basics

**Content:**

Following the structure of `02_mongodb_tutorial.md`, create a tutorial introducing the **MongoDB Aggregation Framework**, using the existing Docker Compose setup and the `landmarks` collection example (ensure it has numeric fields like `visitor_count`).

*   **Introduction:** Explain the purpose of the aggregation framework for data processing and analysis.
*   **Prerequisites:** Refer back to the Docker setup and the collection created in `02_mongodb_tutorial.md`. Ensure the collection has suitable data for aggregation.
*   **Examples:** Provide `mongosh` examples using `db.collection.aggregate([...])` demonstrating basic stages:
    *   `$match`: Filtering documents before aggregation.
    *   `$group`: Grouping documents (e.g., group landmarks by city, calculate average `visitor_count` per city using `$avg`).
    *   `$sort`: Sorting the results.
    *   `$project`: Reshaping documents (selecting, renaming, adding fields).
    *   `$limit`: Limiting the number of output documents.
    *   `$count`: Counting the documents in a stage.
*   **Explanation:** Explain the concept of the aggregation pipeline and the purpose of each demonstrated stage.
*   **Use Cases:** Discuss scenarios where aggregation is useful.
*   **Link Back:** Include links to this tutorial (`02_mongodb_tutorial.md`) and the main Document Databases doc (`../02_document_databases.md`).
```

*(Add similar prompts for Data Modeling, Schema Validation, etc. as needed)*

---
*Back to [Document Databases](../02_document_databases.md)*
