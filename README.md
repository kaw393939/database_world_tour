# Database World Tour: A Graduate Text

Welcome to the Database World Tour! This project serves as a comprehensive overview of various database models, designed as a reference text for Computer Science graduate students.

We explore the fundamental concepts, use cases, popular implementations, strengths, and weaknesses of different database paradigms. Understanding these diverse approaches is crucial for selecting the right tool for the job in modern software architecture.

## Getting Started

This repository includes Docker configurations to quickly spin up instances of the discussed databases.

1.  **Prerequisites:** Ensure you have [Docker](https://docs.docker.com/get-docker/) and [Docker Compose](https://docs.docker.com/compose/install/) installed on your system.
2.  **Launch Databases:** Navigate to the root directory of this repository in your terminal and run:
    ```bash
    docker compose up -d
    ```
    This command will download the necessary images (if not already present) and start containers for PostgreSQL, MongoDB, Redis, and Neo4j in the background. Default connection details and credentials can be found in the `docker-compose.yml` file (remember to change default passwords for secure environments!).
3.  **Explore Documentation:**
    *   The `docs` directory contains detailed explanations for each database model covered.
    *   Inside `docs/tutorials`, you'll find quick-start guides with basic commands for interacting with the running database containers. These are linked from the main documentation files.

## Database Types Explored

Below is a summary of the database models covered in this text. Click the links to dive deeper into each type:

*   **[Relational Databases (SQL)](./docs/01_relational_databases.md)**
    *   *Teaser*: The bedrock of structured data management for decades. Learn about tables, rows, schemas, ACID transactions, and the power of SQL for ensuring data integrity and complex querying. Essential for ERP, CRM, and financial systems.

*   **[Document Databases](./docs/02_document_databases.md)**
    *   *Teaser*: Embrace flexibility with databases that store data in JSON-like documents. Ideal for evolving schemas, content management, product catalogs, and user profiles where data structures vary.

*   **[Key-Value Stores](./docs/03_key_value_stores.md)**
    *   *Teaser*: Simplicity and speed are paramount. Discover how these databases excel at lightning-fast lookups using unique keys, making them perfect for caching, session management, and real-time leaderboards.

*   **[Graph Databases](./docs/04_graph_databases.md)**
    *   *Teaser*: Focus on the connections! Explore how graph databases model and query complex relationships efficiently using nodes and edges. The go-to choice for social networks, recommendation engines, and fraud detection.

*   **[Column-Family Databases (Wide-Column)](./docs/05_column_family_databases.md)**
    *   *Teaser*: Built for big data and high write throughput. Understand how storing data by columns enables massive scalability and efficient analytics over vast datasets, common in logging, time-series, and IoT applications.

## Branding Guidelines

Consistency in presentation enhances clarity. Refer to the `branding` directory for guidelines on:
*   [Typography](./branding/01_typography.md)
*   [Layout](./branding/02_layout.md)
*   [Content Strategy](./branding/03_content_strategy.md)
*   [Brand Story](./branding/04_brand_story.md)
