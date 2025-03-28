# AWS Knowledge Base Retrieval MCP Server
An MCP server implementation for retrieving information from the AWS Knowledge Base using the Bedrock Agent Runtime.

[![Install with NPM in VS Code](https://img.shields.io/badge/VS_Code-NPM-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/redirect?url=vscode:mcp/install?%7B%22name%22%3A%22aws-kb-retrieval%22%2C%22command%22%3A%22npx%22%2C%22args%22%3A%5B%22-y%22%2C%22%40modelcontextprotocol%2Fserver-aws-kb-retrieval%22%5D%2C%22env%22%3A%7B%22AWS_ACCESS_KEY_ID%22%3A%22%24%7Binput%3Aaws_access_key_id%7D%22%2C%22AWS_SECRET_ACCESS_KEY%22%3A%22%24%7Binput%3Aaws_secret_access_key%7D%22%2C%22AWS_REGION%22%3A%22%24%7Binput%3Aaws_region%7D%22%7D%2C%22inputs%22%3A%5B%7B%22id%22%3A%22aws_access_key_id%22%2C%22description%22%3A%22AWS%20Access%20Key%20ID%22%2C%22password%22%3Atrue%7D%2C%7B%22id%22%3A%22aws_secret_access_key%22%2C%22description%22%3A%22AWS%20Secret%20Access%20Key%22%2C%22password%22%3Atrue%7D%2C%7B%22id%22%3A%22aws_region%22%2C%22description%22%3A%22AWS%20Region%22%7D%5D%7D) [![Install with NPM in VS Code Insiders](https://img.shields.io/badge/VS_Code_Insiders-NPM-24bfa5?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect?url=vscode-insiders:mcp/install?%7B%22name%22%3A%22aws-kb-retrieval%22%2C%22command%22%3A%22npx%22%2C%22args%22%3A%5B%22-y%22%2C%22%40modelcontextprotocol%2Fserver-aws-kb-retrieval%22%5D%2C%22env%22%3A%7B%22AWS_ACCESS_KEY_ID%22%3A%22%24%7Binput%3Aaws_access_key_id%7D%22%2C%22AWS_SECRET_ACCESS_KEY%22%3A%22%24%7Binput%3Aaws_secret_access_key%7D%22%2C%22AWS_REGION%22%3A%22%24%7Binput%3Aaws_region%7D%22%7D%2C%22inputs%22%3A%5B%7B%22id%22%3A%22aws_access_key_id%22%2C%22description%22%3A%22AWS%20Access%20Key%20ID%22%2C%22password%22%3Atrue%7D%2C%7B%22id%22%3A%22aws_secret_access_key%22%2C%22description%22%3A%22AWS%20Secret%20Access%20Key%22%2C%22password%22%3Atrue%7D%2C%7B%22id%22%3A%22aws_region%22%2C%22description%22%3A%22AWS%20Region%22%7D%5D%7D)

[![Install with Docker in VS Code](https://img.shields.io/badge/VS_Code-Docker-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/redirect?url=vscode:mcp/install?%7B%22name%22%3A%22aws-kb-retrieval%22%2C%22command%22%3A%22docker%22%2C%22args%22%3A%5B%22run%22%2C%22-i%22%2C%22--rm%22%2C%22-e%22%2C%22AWS_ACCESS_KEY_ID%22%2C%22-e%22%2C%22AWS_SECRET_ACCESS_KEY%22%2C%22-e%22%2C%22AWS_REGION%22%2C%22mcp%2Faws-kb-retrieval%22%5D%2C%22env%22%3A%7B%22AWS_ACCESS_KEY_ID%22%3A%22%24%7Binput%3Aaws_access_key_id%7D%22%2C%22AWS_SECRET_ACCESS_KEY%22%3A%22%24%7Binput%3Aaws_secret_access_key%7D%22%2C%22AWS_REGION%22%3A%22%24%7Binput%3Aaws_region%7D%22%7D%2C%22inputs%22%3A%5B%7B%22id%22%3A%22aws_access_key_id%22%2C%22description%22%3A%22AWS%20Access%20Key%20ID%22%2C%22password%22%3Atrue%7D%2C%7B%22id%22%3A%22aws_secret_access_key%22%2C%22description%22%3A%22AWS%20Secret%20Access%20Key%22%2C%22password%22%3Atrue%7D%2C%7B%22id%22%3A%22aws_region%22%2C%22description%22%3A%22AWS%20Region%22%7D%5D%7D) [![Install with Docker in VS Code Insiders](https://img.shields.io/badge/VS_Code_Insiders-Docker-24bfa5?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect?url=vscode-insiders:mcp/install?%7B%22name%22%3A%22aws-kb-retrieval%22%2C%22command%22%3A%22docker%22%2C%22args%22%3A%5B%22run%22%2C%22-i%22%2C%22--rm%22%2C%22-e%22%2C%22AWS_ACCESS_KEY_ID%22%2C%22-e%22%2C%22AWS_SECRET_ACCESS_KEY%22%2C%22-e%22%2C%22AWS_REGION%22%2C%22mcp%2Faws-kb-retrieval%22%5D%2C%22env%22%3A%7B%22AWS_ACCESS_KEY_ID%22%3A%22%24%7Binput%3Aaws_access_key_id%7D%22%2C%22AWS_SECRET_ACCESS_KEY%22%3A%22%24%7Binput%3Aaws_secret_access_key%7D%22%2C%22AWS_REGION%22%3A%22%24%7Binput%3Aaws_region%7D%22%7D%2C%22inputs%22%3A%5B%7B%22id%22%3A%22aws_access_key_id%22%2C%22description%22%3A%22AWS%20Access%20Key%20ID%22%2C%22password%22%3Atrue%7D%2C%7B%22id%22%3A%22aws_secret_access_key%22%2C%22description%22%3A%22AWS%20Secret%20Access%20Key%22%2C%22password%22%3Atrue%7D%2C%7B%22id%22%3A%22aws_region%22%2C%22description%22%3A%22AWS%20Region%22%7D%5D%7D)

## Features

- **RAG (Retrieval-Augmented Generation)**: Retrieve context from the AWS Knowledge Base based on a query and a Knowledge Base ID.
- **Supports multiple results retrieval**: Option to retrieve a customizable number of results.

## Tools

- **retrieve_from_aws_kb**
  - Perform retrieval operations using the AWS Knowledge Base.
  - Inputs:
    - `query` (string): The search query for retrieval.
    - `knowledgeBaseId` (string): The ID of the AWS Knowledge Base.
    - `n` (number, optional): Number of results to retrieve (default: 3).

## Configuration

### Setting up AWS Credentials

1. Obtain AWS access key ID, secret access key, and region from the AWS Management Console.
2. Ensure these credentials have appropriate permissions for Bedrock Agent Runtime operations.

### Usage with Claude Desktop

Add this to your `claude_desktop_config.json`:

#### Docker

```json
{
  "mcpServers": {
    "aws-kb-retrieval": {
      "command": "docker",
      "args": [ "run", "-i", "--rm", "-e", "AWS_ACCESS_KEY_ID", "-e", "AWS_SECRET_ACCESS_KEY", "-e", "AWS_REGION", "mcp/aws-kb-retrieval-server" ],
      "env": {
        "AWS_ACCESS_KEY_ID": "YOUR_ACCESS_KEY_HERE",
        "AWS_SECRET_ACCESS_KEY": "YOUR_SECRET_ACCESS_KEY_HERE",
        "AWS_REGION": "YOUR_AWS_REGION_HERE"
      }
    }
  }
}
```

```json
{
  "mcpServers": {
    "aws-kb-retrieval": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-aws-kb-retrieval"
      ],
      "env": {
        "AWS_ACCESS_KEY_ID": "YOUR_ACCESS_KEY_HERE",
        "AWS_SECRET_ACCESS_KEY": "YOUR_SECRET_ACCESS_KEY_HERE",
        "AWS_REGION": "YOUR_AWS_REGION_HERE"
      }
    }
  }
}
```

## Building

Docker: 

```sh
docker build -t mcp/aws-kb-retrieval -f src/aws-kb-retrieval-server/Dockerfile . 
```

## VS Code Installation

### Manual Installation

Add the following to your `.vscode/mcp.json` file:

#### Using NPM

```json
{
  "aws-kb-retrieval": {
    "inputs": [
      {
        "id": "aws_access_key_id",
        "description": "AWS Access Key ID",
        "password": true
      },
      {
        "id": "aws_secret_access_key",
        "description": "AWS Secret Access Key",
        "password": true
      },
      {
        "id": "aws_region",
        "description": "AWS Region"
      }
    ],
    "command": "npx",
    "args": [
      "-y",
      "@modelcontextprotocol/server-aws-kb-retrieval"
    ],
    "env": {
      "AWS_ACCESS_KEY_ID": "${input:aws_access_key_id}",
      "AWS_SECRET_ACCESS_KEY": "${input:aws_secret_access_key}",
      "AWS_REGION": "${input:aws_region}"
    }
  }
}
```

#### Using Docker

```json
{
  "aws-kb-retrieval": {
    "inputs": [
      {
        "id": "aws_access_key_id",
        "description": "AWS Access Key ID",
        "password": true
      },
      {
        "id": "aws_secret_access_key",
        "description": "AWS Secret Access Key",
        "password": true
      },
      {
        "id": "aws_region",
        "description": "AWS Region"
      }
    ],
    "command": "docker",
    "args": [
      "run",
      "-i",
      "--rm",
      "-e",
      "AWS_ACCESS_KEY_ID",
      "-e",
      "AWS_SECRET_ACCESS_KEY",
      "-e",
      "AWS_REGION",
      "mcp/aws-kb-retrieval"
    ],
    "env": {
      "AWS_ACCESS_KEY_ID": "${input:aws_access_key_id}",
      "AWS_SECRET_ACCESS_KEY": "${input:aws_secret_access_key}",
      "AWS_REGION": "${input:aws_region}"
    }
  }
}
```

## License

This MCP server is licensed under the MIT License. This means you are free to use, modify, and distribute the software, subject to the terms and conditions of the MIT License. For more details, please see the LICENSE file in the project repository.

This README assumes that your server package is named `@modelcontextprotocol/server-aws-kb-retrieval`. Adjust the package name and installation details if they differ in your setup. Also, ensure that your server script is correctly built and that all dependencies are properly managed in your `package.json`.
