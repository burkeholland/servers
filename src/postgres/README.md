# PostgreSQL
A Model Context Protocol server that provides read-only access to PostgreSQL databases. This server enables LLMs to inspect database schemas and execute read-only queries.

[![Install with NPM in VS Code](https://img.shields.io/badge/VS_Code-NPM-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/redirect?url=vscode:mcp/install?%7B%22name%22%3A%22postgres%22%2C%22command%22%3A%22npx%22%2C%22args%22%3A%5B%22-y%22%2C%22%40modelcontextprotocol%2Fserver-postgres%22%5D%2C%22env%22%3A%7B%22POSTGRES_CONNECTION_STRING%22%3A%22%24%7Binput%3Apostgres_connection_string%7D%22%7D%2C%22inputs%22%3A%5B%7B%22id%22%3A%22postgres_connection_string%22%2C%22description%22%3A%22PostgreSQL%20Connection%20String%22%2C%22password%22%3Atrue%7D%5D%7D) [![Install with NPM in VS Code Insiders](https://img.shields.io/badge/VS_Code_Insiders-NPM-24bfa5?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect?url=vscode-insiders:mcp/install?%7B%22name%22%3A%22postgres%22%2C%22command%22%3A%22npx%22%2C%22args%22%3A%5B%22-y%22%2C%22%40modelcontextprotocol%2Fserver-postgres%22%5D%2C%22env%22%3A%7B%22POSTGRES_CONNECTION_STRING%22%3A%22%24%7Binput%3Apostgres_connection_string%7D%22%7D%2C%22inputs%22%3A%5B%7B%22id%22%3A%22postgres_connection_string%22%2C%22description%22%3A%22PostgreSQL%20Connection%20String%22%2C%22password%22%3Atrue%7D%5D%7D)

[![Install with Docker in VS Code](https://img.shields.io/badge/VS_Code-Docker-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/redirect?url=vscode:mcp/install?%7B%22name%22%3A%22postgres%22%2C%22command%22%3A%22docker%22%2C%22args%22%3A%5B%22run%22%2C%22-i%22%2C%22--rm%22%2C%22mcp%2Fpostgres%22%2C%22%24%7Binput%3Apostgres_connection_string%7D%22%5D%2C%22env%22%3A%7B%7D%2C%22inputs%22%3A%5B%7B%22id%22%3A%22postgres_connection_string%22%2C%22description%22%3A%22PostgreSQL%20Connection%20String%22%2C%22password%22%3Atrue%7D%5D%7D) [![Install with Docker in VS Code Insiders](https://img.shields.io/badge/VS_Code_Insiders-Docker-24bfa5?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect?url=vscode-insiders:mcp/install?%7B%22name%22%3A%22postgres%22%2C%22command%22%3A%22docker%22%2C%22args%22%3A%5B%22run%22%2C%22-i%22%2C%22--rm%22%2C%22mcp%2Fpostgres%22%2C%22%24%7Binput%3Apostgres_connection_string%7D%22%5D%2C%22env%22%3A%7B%7D%2C%22inputs%22%3A%5B%7B%22id%22%3A%22postgres_connection_string%22%2C%22description%22%3A%22PostgreSQL%20Connection%20String%22%2C%22password%22%3Atrue%7D%5D%7D)

## Components

### Tools

- **query**
  - Execute read-only SQL queries against the connected database
  - Input: `sql` (string): The SQL query to execute
  - All queries are executed within a READ ONLY transaction

### Resources

The server provides schema information for each table in the database:

- **Table Schemas** (`postgres://<host>/<table>/schema`)
  - JSON schema information for each table
  - Includes column names and data types
  - Automatically discovered from database metadata

## Usage with Claude Desktop

To use this server with the Claude Desktop app, add the following configuration to the "mcpServers" section of your `claude_desktop_config.json`:

### Docker

* when running docker on macos, use host.docker.internal if the server is running on the host network (eg localhost)
* username/password can be added to the postgresql url with `postgresql://user:password@host:port/db-name`

```json
{
  "mcpServers": {
    "postgres": {
      "command": "docker",
      "args": [
        "run", 
        "-i", 
        "--rm", 
        "mcp/postgres", 
        "postgresql://host.docker.internal:5432/mydb"]
    }
  }
}
```

### NPX

```json
{
  "mcpServers": {
    "postgres": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-postgres",
        "postgresql://localhost/mydb"
      ]
    }
  }
}
```

Replace `/mydb` with your database name.

## Building

Docker:

```sh
docker build -t mcp/postgres -f src/postgres/Dockerfile . 
```

## VS Code Installation

### Manual Installation

Add the following to your `.vscode/mcp.json` file:

#### Using NPM

```json
{
  "postgres": {
    "inputs": [
      {
        "id": "postgres_connection_string",
        "description": "PostgreSQL Connection String",
        "password": true
      }
    ],
    "command": "npx",
    "args": [
      "-y",
      "@modelcontextprotocol/server-postgres"
    ],
    "env": {
      "POSTGRES_CONNECTION_STRING": "${input:postgres_connection_string}"
    }
  }
}
```

#### Using Docker

```json
{
  "postgres": {
    "inputs": [
      {
        "id": "postgres_connection_string",
        "description": "PostgreSQL Connection String",
        "password": true
      }
    ],
    "command": "docker",
    "args": [
      "run",
      "-i",
      "--rm",
      "mcp/postgres",
      "${input:postgres_connection_string}"
    ]
  }
}
```

## License

This MCP server is licensed under the MIT License. This means you are free to use, modify, and distribute the software, subject to the terms and conditions of the MIT License. For more details, please see the LICENSE file in the project repository.
