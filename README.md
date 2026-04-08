# Gemini CLI Extension - AlloyDB Omni

> [!NOTE]
> This extension is currently in beta (pre-v1.0), and may see breaking changes until the first stable release (v1.0).

Instantly manage and query your [AlloyDB Omni](https://docs.cloud.google.com/alloydb/omni/docs) databases using the power of natural language, directly from your command line. Go from an idea to a running cluster and queryable data in minutes, without ever leaving your terminal.

Learn more about [Gemini CLI Extensions](https://github.com/google-gemini/gemini-cli/blob/main/docs/extensions/index.md).
> [!IMPORTANT]
> **We Want Your Feedback!**
> Please share your thoughts with us by filling out our feedback [form][form].
> Your input is invaluable and helps us improve the project for everyone.

[form]: https://docs.google.com/forms/d/e/1FAIpQLSfEGmLR46iipyNTgwTmIDJqzkAwDPXxbocpXpUbHXydiN1RTw/viewform?usp=pp_url&entry.157487=alloydb-omni

## Why Use the AlloyDB Omni Extension?

* **Natural Language Management:** Stop wrestling with complex commands. Provision infrastructure, manage users, and query data by describing what you want in plain English.
* **Seamless Workflow:** Stay in your CLI. No need to constantly switch contexts to the GCP console for common database tasks.
* **Full Lifecycle Control:** Manage the entire lifecycle of your database, from creating clusters and instances to exploring schemas and running queries.
* **Code Generation:** Accelerate development by asking Gemini to generate data classes and other code snippets based on your table schemas.


## Prerequisites

Before you begin, ensure you have the following:

* [Gemini CLI](https://github.com/google-gemini/gemini-cli) installed with version **+v0.6.0**.
* Setup Gemini CLI [Authentication](https://github.com/google-gemini/gemini-cli/tree/main?tab=readme-ov-file#-authentication-options).

## Getting Started

### Installation

To install the extension, use the following command before starting the Gemini CLI:

```bash
gemini extensions install https://github.com/gemini-cli-extensions/alloydb-omni
```

### Configuration

You will be prompted to configure the following settings during installation. These settings are saved in an `.env` file within the extension's directory.

*   `ALLOYDB_OMNI_HOST`: The host of your AlloyDB cluster.
*   `ALLOYDB_OMNI_PORT`: The port of your AlloyDB cluster.
*   `ALLOYDB_OMNI_DATABASE`: The name of the database to connect to.
*   `ALLOYDB_OMNI_USER`: (Optional) The database username.
*   `ALLOYDB_OMNI_PASSWORD`: (Optional) The password for the database user.

To view or update your configuration:

**List Settings:**
*   Terminal: `gemini extensions list`
*   Gemini CLI: `/extensions list`

**Update Settings:**
*   Terminal: `gemini extensions config alloydb-omni [setting name] [--scope <scope>]`
    *   `setting name`: (Optional) The single setting to configure.
    *   `scope`: (Optional) The scope of the setting in (`user` or `workspace`). Defaults to `user`.
*   Currently, you must restart the Gemini CLI for changes to take effect. We recommend using `gemini --resume` to resume your session.

Alternatively, you can manually set these environment variables before starting the Gemini CLI:

```bash
export ALLOYDB_OMNI_HOST="<your-alloydb-host>"
export ALLOYDB_OMNI_PORT="<your-alloydb-port>"
export ALLOYDB_OMNI_DATABASE="<your-alloydb-database>"
export ALLOYDB_OMNI_USER="<your-alloydb-user>"
export ALLOYDB_OMNI_PASSWORD="<your-alloydb-password>"
```

> [!NOTE]
> * See [Troubleshooting](#troubleshooting) for debugging your configuration.

### Start Gemini CLI

To start the Gemini CLI, use the following command:

```bash
gemini
```

> [!WARNING]
> **Changing Instance & Database Connections**
> Currently, the database connection must be configured before starting the Gemini CLI and can not be changed during a session.
> To save and resume conversation history use command: `/chat save <tag>` and `/chat resume <tag>`.

## Usage Examples

Interact with AlloyDB Omni using natural language right from your IDE:

* **Provision Infrastructure:**
    * "Create a new AlloyDB Omni container with Docker."
    * "Show me all the AlloyDB Omni DBClusters on my Kubernetes cluster."

* **Explore Schemas and Data:**
    * "Show me all tables in the 'orders' database."
    * "What are the columns in the 'products' table?"
    * "How many orders were placed in the last 30 days, and what were the top 5 most purchased items?"

* **Generate Code:**
    * "Generate a Python dataclass to represent the 'customers' table."

## Supported Tools

This extension provides a comprehensive set of tools:

* **Data:**
    * `list_tables`: Use this tool to lists tables in the database.
    * `database_overview`: Use this tool to fetches the current state of the PostgreSQL server.
    * `execute_sql`: Use this tool to executes a SQL query.
    * `list_active_queries`: Use this tool to list currently running queries.
    * `list_available_extensions`: Use this tool to list available extensions for installation.
    * `list_installed_extensions`: Use this tool to list installed extensions.
    * `get_query_plan`: Use this tool to get query plan.
    * `list_autovacuum_configurations`: Use this tool to list autovacuum configurations and its value.
    * `list_columnar_configurations`: List AlloyDB Omni columnar-related configurations.
    * `list_columnar_recommended_columns`: Lists columns that AlloyDB Omni recommends adding to the columnar engine.
    * `list_database_stats`: Use this tool to lists the key performance and activity statistics for each database in the AlloyDB Omni instance.
    * `list_indexes`: Use this tool to list available user indexes in a PostgreSQL database.
    * `list_memory_configurations`: Use this tool to list memory configurations and its value.
    * `list_pg_settings`: Use this tool to list configuration parameters for the PostgreSQL server.
    * `list_publication_tables`: Use this tool to list publication tables in a PostgreSQL database.
    * `list_replication_slots`: Use this tool to list replication slots.
    * `list_roles`: Use this tool to lists all the user-created roles in PostgreSQL database.
    * `list_schemas`: Use this tool to lists schemas in the database.
    * `list_sequences`: Use this tool to list sequences in a PostgreSQL database.
    * `list_tablespaces`: Use this tool to lists tablespaces in the database.
    * `list_top_bloated_tables`: Use this tool to list top bloated tables.
    * `list_triggers`: Use this tool to lists triggers in the database.
    * `list_views`: Use this tool to lists views in the database from pg_views with a default limit of 50 rows.
    * `list_invalid_indexes`: Use this tool to list invalid indexes.

## Troubleshooting

Use `gemini --debug` to enable debugging.

Common issues:

* "✖ Error during discovery for server: MCP error -32000: Connection closed": The database connection has not been established. Ensure your configuration is set via environment variables.
* "✖ MCP ERROR: Error: spawn /Users/USER/.gemini/extensions/alloydb-omni/toolbox ENOENT": The Toolbox binary did not download correctly. Ensure you are using Gemini CLI v0.33.0+.
* "cannot execute binary file": The Toolbox binary did not download correctly. Ensure the correct binary for your OS/Architecture has been downloaded. See [Installing the server](https://mcp-toolbox.dev/documentation/introduction/#install-toolbox) for more information.
