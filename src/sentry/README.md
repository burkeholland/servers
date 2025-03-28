# mcp-server-sentry: A Sentry MCP server

## Overview
A Model Context Protocol server for retrieving and analyzing issues from Sentry.io. This server provides tools to inspect error reports, stacktraces, and other debugging information from your Sentry account.

[![Install with Python in VS Code](https://img.shields.io/badge/VS_Code-Python-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/redirect?url=vscode:mcp/install?%7B%22name%22%3A%22sentry%22%2C%22command%22%3A%22python%22%2C%22args%22%3A%5B%22-m%22%2C%22mcp_server_sentry%22%2C%22--auth-token%22%2C%22%24%7Binput%3Asentry_auth_token%7D%22%5D%2C%22env%22%3A%7B%7D%2C%22inputs%22%3A%5B%7B%22id%22%3A%22sentry_auth_token%22%2C%22description%22%3A%22Sentry%20Authentication%20Token%22%2C%22password%22%3Atrue%7D%5D%7D) [![Install with Python in VS Code Insiders](https://img.shields.io/badge/VS_Code_Insiders-Python-24bfa5?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect?url=vscode-insiders:mcp/install?%7B%22name%22%3A%22sentry%22%2C%22command%22%3A%22python%22%2C%22args%22%3A%5B%22-m%22%2C%22mcp_server_sentry%22%2C%22--auth-token%22%2C%22%24%7Binput%3Asentry_auth_token%7D%22%5D%2C%22env%22%3A%7B%7D%2C%22inputs%22%3A%5B%7B%22id%22%3A%22sentry_auth_token%22%2C%22description%22%3A%22Sentry%20Authentication%20Token%22%2C%22password%22%3Atrue%7D%5D%7D)

[![Install with Docker in VS Code](https://img.shields.io/badge/VS_Code-Docker-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/redirect?url=vscode:mcp/install?%7B%22name%22%3A%22sentry%22%2C%22command%22%3A%22docker%22%2C%22args%22%3A%5B%22run%22%2C%22-i%22%2C%22--rm%22%2C%22mcp%2Fsentry%22%2C%22--auth-token%22%2C%22%24%7Binput%3Asentry_auth_token%7D%22%5D%2C%22env%22%3A%7B%7D%2C%22inputs%22%3A%5B%7B%22id%22%3A%22sentry_auth_token%22%2C%22description%22%3A%22Sentry%20Authentication%20Token%22%2C%22password%22%3Atrue%7D%5D%7D) [![Install with Docker in VS Code Insiders](https://img.shields.io/badge/VS_Code_Insiders-Docker-24bfa5?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect?url=vscode-insiders:mcp/install?%7B%22name%22%3A%22sentry%22%2C%22command%22%3A%22docker%22%2C%22args%22%3A%5B%22run%22%2C%22-i%22%2C%22--rm%22%2C%22mcp%2Fsentry%22%2C%22--auth-token%22%2C%22%24%7Binput%3Asentry_auth_token%7D%22%5D%2C%22env%22%3A%7B%7D%2C%22inputs%22%3A%5B%7B%22id%22%3A%22sentry_auth_token%22%2C%22description%22%3A%22Sentry%20Authentication%20Token%22%2C%22password%22%3Atrue%7D%5D%7D)

### Tools

1. `get_sentry_issue`
   - Retrieve and analyze a Sentry issue by ID or URL
   - Input:
     - `issue_id_or_url` (string): Sentry issue ID or URL to analyze
   - Returns: Issue details including:
     - Title
     - Issue ID
     - Status
     - Level
     - First seen timestamp
     - Last seen timestamp
     - Event count
     - Full stacktrace

### Prompts

1. `sentry-issue`
   - Retrieve issue details from Sentry
   - Input:
     - `issue_id_or_url` (string): Sentry issue ID or URL
   - Returns: Formatted issue details as conversation context

## Installation

### Using uv (recommended)

When using [`uv`](https://docs.astral.sh/uv/) no specific installation is needed. We will
use [`uvx`](https://docs.astral.sh/uv/guides/tools/) to directly run *mcp-server-sentry*.

### Using PIP

Alternatively you can install `mcp-server-sentry` via pip:

```
pip install mcp-server-sentry
```

After installation, you can run it as a script using:

```
python -m mcp_server_sentry
```

## Configuration

### Usage with Claude Desktop

Add this to your `claude_desktop_config.json`:

<details>
<summary>Using uvx</summary>

```json
"mcpServers": {
  "sentry": {
    "command": "uvx",
    "args": ["mcp-server-sentry", "--auth-token", "YOUR_SENTRY_TOKEN"]
  }
}
```
</details>

<details>

<details>
<summary>Using docker</summary>

```json
"mcpServers": {
  "sentry": {
    "command": "docker",
    "args": ["run", "-i", "--rm", "mcp/sentry", "--auth-token", "YOUR_SENTRY_TOKEN"]
  }
}
```
</details>

<details>

<summary>Using pip installation</summary>

```json
"mcpServers": {
  "sentry": {
    "command": "python",
    "args": ["-m", "mcp_server_sentry", "--auth-token", "YOUR_SENTRY_TOKEN"]
  }
}
```
</details>

### Usage with [Zed](https://github.com/zed-industries/zed)

Add to your Zed settings.json:

<details>
<summary>Using uvx</summary>

```json
"context_servers": [
  "mcp-server-sentry": {
    "command": {
      "path": "uvx",
      "args": ["mcp-server-sentry", "--auth-token", "YOUR_SENTRY_TOKEN"]
    }
  }
],
```
</details>

<details>
<summary>Using pip installation</summary>

```json
"context_servers": {
  "mcp-server-sentry": {
    "command": "python",
    "args": ["-m", "mcp_server_sentry", "--auth-token", "YOUR_SENTRY_TOKEN"]
  }
},
```
</details>

## Debugging

You can use the MCP inspector to debug the server. For uvx installations:

```
npx @modelcontextprotocol/inspector uvx mcp-server-sentry --auth-token YOUR_SENTRY_TOKEN
```

Or if you've installed the package in a specific directory or are developing on it:

```
cd path/to/servers/src/sentry
npx @modelcontextprotocol/inspector uv run mcp-server-sentry --auth-token YOUR_SENTRY_TOKEN
```

## VS Code Installation

### Manual Installation

Add the following to your `.vscode/mcp.json` file:

#### Using Python

```json
{
  "sentry": {
    "inputs": [
      {
        "id": "sentry_auth_token",
        "description": "Sentry Authentication Token",
        "password": true
      }
    ],
    "command": "python",
    "args": [
      "-m",
      "mcp_server_sentry",
      "--auth-token",
      "${input:sentry_auth_token}"
    ]
  }
}
```

#### Using Docker

```json
{
  "sentry": {
    "inputs": [
      {
        "id": "sentry_auth_token",
        "description": "Sentry Authentication Token",
        "password": true
      }
    ],
    "command": "docker",
    "args": [
      "run",
      "-i",
      "--rm",
      "mcp/sentry",
      "--auth-token",
      "${input:sentry_auth_token}"
    ]
  }
}
```

## License

This MCP server is licensed under the MIT License. This means you are free to use, modify, and distribute the software, subject to the terms and conditions of the MIT License. For more details, please see the LICENSE file in the project repository.
