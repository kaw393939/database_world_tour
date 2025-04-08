
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
