# SQLite MCP Server

## Overview
A Model Context Protocol (MCP) server implementation that provides database interaction and business intelligence capabilities through SQLite. This server enables running SQL queries, analyzing business data, and automatically generating business insight memos.

[![Install with NPM in VS Code](https://img.shields.io/badge/VS_Code-NPM-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/redirect?url=vscode:mcp/install?%7B%22name%22%3A%22sqlite%22%2C%22command%22%3A%22npx%22%2C%22args%22%3A%5B%22-y%22%2C%22%40modelcontextprotocol%2Fserver-sqlite%22%5D%2C%22env%22%3A%7B%22SQLITE_DATABASE_PATH%22%3A%22%24%7Binput%3Asqlite_database_path%7D%22%7D%2C%22inputs%22%3A%5B%7B%22id%22%3A%22sqlite_database_path%22%2C%22description%22%3A%22Path%20to%20SQLite%20database%20file%22%7D%5D%7D) [![Install with NPM in VS Code Insiders](https://img.shields.io/badge/VS_Code_Insiders-NPM-24bfa5?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect?url=vscode-insiders:mcp/install?%7B%22name%22%3A%22sqlite%22%2C%22command%22%3A%22npx%22%2C%22args%22%3A%5B%22-y%22%2C%22%40modelcontextprotocol%2Fserver-sqlite%22%5D%2C%22env%22%3A%7B%22SQLITE_DATABASE_PATH%22%3A%22%24%7Binput%3Asqlite_database_path%7D%22%7D%2C%22inputs%22%3A%5B%7B%22id%22%3A%22sqlite_database_path%22%2C%22description%22%3A%22Path%20to%20SQLite%20database%20file%22%7D%5D%7D)

[![Install with Docker in VS Code](https://img.shields.io/badge/VS_Code-Docker-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/redirect?url=vscode:mcp/install?%7B%22name%22%3A%22sqlite%22%2C%22command%22%3A%22docker%22%2C%22args%22%3A%5B%22run%22%2C%22--rm%22%2C%22-i%22%2C%22-v%22%2C%22mcp-sqlite%3A%2Fmcp%22%2C%22mcp%2Fsqlite%22%2C%22--db-path%22%2C%22%2Fmcp%2F%24%7Binput%3Asqlite_database_filename%7D%22%5D%2C%22inputs%22%3A%5B%7B%22id%22%3A%22sqlite_database_filename%22%2C%22description%22%3A%22SQLite%20database%20filename%20(created%20in%20persistent%20volume)%22%2C%22default%22%3A%22database.db%22%7D%5D%7D) [![Install with Docker in VS Code Insiders](https://img.shields.io/badge/VS_Code_Insiders-Docker-24bfa5?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect?url=vscode-insiders:mcp/install?%7B%22name%22%3A%22sqlite%22%2C%22command%22%3A%22docker%22%2C%22args%22%3A%5B%22run%22%2C%22--rm%22%2C%22-i%22%2C%22-v%22%2C%22mcp-sqlite%3A%2Fmcp%22%2C%22mcp%2Fsqlite%22%2C%22--db-path%22%2C%22%2Fmcp%2F%24%7Binput%3Asqlite_database_filename%7D%22%5D%2C%22inputs%22%3A%5B%7B%22id%22%3A%22sqlite_database_filename%22%2C%22description%22%3A%22SQLite%20database%20filename%20(created%20in%20persistent%20volume)%22%2C%22default%22%3A%22database.db%22%7D%5D%7D)

## Components

### Resources
The server exposes a single dynamic resource:
- `memo://insights`: A continuously updated business insights memo that aggregates discovered insights during analysis
  - Auto-updates as new insights are discovered via the append-insight tool

### Prompts
The server provides a demonstration prompt:
- `mcp-demo`: Interactive prompt that guides users through database operations
  - Required argument: `topic` - The business domain to analyze
  - Generates appropriate database schemas and sample data
  - Guides users through analysis and insight generation
  - Integrates with the business insights memo

### Tools
The server offers six core tools:

#### Query Tools
- `read_query`
   - Execute SELECT queries to read data from the database
   - Input:
     - `query` (string): The SELECT SQL query to execute
   - Returns: Query results as array of objects

- `write_query`
   - Execute INSERT, UPDATE, or DELETE queries
   - Input:
     - `query` (string): The SQL modification query
   - Returns: `{ affected_rows: number }`

- `create_table`
   - Create new tables in the database
   - Input:
     - `query` (string): CREATE TABLE SQL statement
   - Returns: Confirmation of table creation

#### Schema Tools
- `list_tables`
   - Get a list of all tables in the database
   - No input required
   - Returns: Array of table names

- `describe-table`
   - View schema information for a specific table
   - Input:
     - `table_name` (string): Name of table to describe
   - Returns: Array of column definitions with names and types

#### Analysis Tools
- `append_insight`
   - Add new business insights to the memo resource
   - Input:
     - `insight` (string): Business insight discovered from data analysis
   - Returns: Confirmation of insight addition
   - Triggers update of memo://insights resource


## Usage with Claude Desktop

### uv

```bash
# Add the server to your claude_desktop_config.json
"mcpServers": {
  "sqlite": {
    "command": "uv",
    "args": [
      "--directory",
      "parent_of_servers_repo/servers/src/sqlite",
      "run",
      "mcp-server-sqlite",
      "--db-path",
      "~/test.db"
    ]
  }
}
```

### Docker

```json
# Add the server to your claude_desktop_config.json
"mcpServers": {
  "sqlite": {
    "command": "docker",
    "args": [
      "run",
      "--rm",
      "-i",
      "-v",
      "mcp-test:/mcp",
      "mcp/sqlite",
      "--db-path",
      "/mcp/test.db"
    ]
  }
}
```

## Building

Docker:

```bash
docker build -t mcp/sqlite .
```

## VS Code Installation

### Manual Installation

Add the following to your `.vscode/mcp.json` file:

#### Using NPM

```json
{
  "sqlite": {
    "inputs": [
      {
        "id": "sqlite_database_path",
        "description": "Path to SQLite database file"
      }
    ],
    "command": "npx",
    "args": [
      "-y",
      "@modelcontextprotocol/server-sqlite"
    ],
    "env": {
      "SQLITE_DATABASE_PATH": "${input:sqlite_database_path}"
    }
  }
}
```

#### Using Docker

```json
{
  "sqlite": {
    "inputs": [
      {
        "id": "sqlite_database_filename",
        "description": "SQLite database filename (created in persistent volume)",
        "default": "database.db"
      }
    ],
    "command": "docker",
    "args": [
      "run",
      "--rm",
      "-i",
      "-v",
      "mcp-sqlite:/mcp",
      "mcp/sqlite",
      "--db-path",
      "/mcp/${input:sqlite_database_filename}"
    ]
  }
}
```

## License

This MCP server is licensed under the MIT License. This means you are free to use, modify, and distribute the software, subject to the terms and conditions of the MIT License. For more details, please see the LICENSE file in the project repository.
