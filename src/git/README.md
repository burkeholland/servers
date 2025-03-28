# mcp-server-git: A git MCP server

## Overview
A Model Context Protocol server for Git repository interaction and automation. This server provides tools to read, search, and manipulate Git repositories via Large Language Models.

[![Install with Python in VS Code](https://img.shields.io/badge/VS_Code-Python-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/redirect?url=vscode:mcp/install?%7B%22name%22%3A%22git%22%2C%22command%22%3A%22python%22%2C%22args%22%3A%5B%22-m%22%2C%22mcp_server_git%22%2C%22--repository%22%2C%22%24%7Binput%3Agit_repository_path%7D%22%5D%2C%22env%22%3A%7B%7D%2C%22inputs%22%3A%5B%7B%22id%22%3A%22git_repository_path%22%2C%22description%22%3A%22Path%20to%20Git%20repository%22%7D%5D%7D) [![Install with Python in VS Code Insiders](https://img.shields.io/badge/VS_Code_Insiders-Python-24bfa5?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect?url=vscode-insiders:mcp/install?%7B%22name%22%3A%22git%22%2C%22command%22%3A%22python%22%2C%22args%22%3A%5B%22-m%22%2C%22mcp_server_git%22%2C%22--repository%22%2C%22%24%7Binput%3Agit_repository_path%7D%22%5D%2C%22env%22%3A%7B%7D%2C%22inputs%22%3A%5B%7B%22id%22%3A%22git_repository_path%22%2C%22description%22%3A%22Path%20to%20Git%20repository%22%7D%5D%7D)

[![Install with Docker in VS Code](https://img.shields.io/badge/VS_Code-Docker-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/redirect?url=vscode:mcp/install?%7B%22name%22%3A%22git%22%2C%22command%22%3A%22docker%22%2C%22args%22%3A%5B%22run%22%2C%22--rm%22%2C%22-i%22%2C%22--mount%22%2C%22type%3Dbind%2Csrc%3D%24%7Binput%3Aworkspace_path%7D%2Cdst%3D%2Fmounted-workspace%22%2C%22mcp%2Fgit%22%5D%2C%22env%22%3A%7B%7D%2C%22inputs%22%3A%5B%7B%22id%22%3A%22workspace_path%22%2C%22description%22%3A%22Path%20to%20directory%20containing%20Git%20repositories%22%2C%22default%22%3A%22%24%7BworkspaceFolder%7D%22%7D%5D%7D) [![Install with Docker in VS Code Insiders](https://img.shields.io/badge/VS_Code_Insiders-Docker-24bfa5?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect?url=vscode-insiders:mcp/install?%7B%22name%22%3A%22git%22%2C%22command%22%3A%22docker%22%2C%22args%22%3A%5B%22run%22%2C%22--rm%22%2C%22-i%22%2C%22--mount%22%2C%22type%3Dbind%2Csrc%3D%24%7Binput%3Aworkspace_path%7D%2Cdst%3D%2Fmounted-workspace%22%2C%22mcp%2Fgit%22%5D%2C%22env%22%3A%7B%7D%2C%22inputs%22%3A%5B%7B%22id%22%3A%22workspace_path%22%2C%22description%22%3A%22Path%20to%20directory%20containing%20Git%20repositories%22%2C%22default%22%3A%22%24%7BworkspaceFolder%7D%22%7D%5D%7D)

Please note that mcp-server-git is currently in early development. The functionality and available tools are subject to change and expansion as we continue to develop and improve the server.

### Tools

1. `git_status`
   - Shows the working tree status
   - Input:
     - `repo_path` (string): Path to Git repository
   - Returns: Current status of working directory as text output

2. `git_diff_unstaged`
   - Shows changes in working directory not yet staged
   - Input:
     - `repo_path` (string): Path to Git repository
   - Returns: Diff output of unstaged changes

3. `git_diff_staged`
   - Shows changes that are staged for commit
   - Input:
     - `repo_path` (string): Path to Git repository
   - Returns: Diff output of staged changes

4. `git_diff`
   - Shows differences between branches or commits
   - Inputs:
     - `repo_path` (string): Path to Git repository
     - `target` (string): Target branch or commit to compare with
   - Returns: Diff output comparing current state with target

5. `git_commit`
   - Records changes to the repository
   - Inputs:
     - `repo_path` (string): Path to Git repository
     - `message` (string): Commit message
   - Returns: Confirmation with new commit hash

6. `git_add`
   - Adds file contents to the staging area
   - Inputs:
     - `repo_path` (string): Path to Git repository
     - `files` (string[]): Array of file paths to stage
   - Returns: Confirmation of staged files

7. `git_reset`
   - Unstages all staged changes
   - Input:
     - `repo_path` (string): Path to Git repository
   - Returns: Confirmation of reset operation

8. `git_log`
   - Shows the commit logs
   - Inputs:
     - `repo_path` (string): Path to Git repository
     - `max_count` (number, optional): Maximum number of commits to show (default: 10)
   - Returns: Array of commit entries with hash, author, date, and message

9. `git_create_branch`
   - Creates a new branch
   - Inputs:
     - `repo_path` (string): Path to Git repository
     - `branch_name` (string): Name of the new branch
     - `start_point` (string, optional): Starting point for the new branch
   - Returns: Confirmation of branch creation
10. `git_checkout`
   - Switches branches
   - Inputs:
     - `repo_path` (string): Path to Git repository
     - `branch_name` (string): Name of branch to checkout
   - Returns: Confirmation of branch switch
11. `git_show`
   - Shows the contents of a commit
   - Inputs:
     - `repo_path` (string): Path to Git repository
     - `revision` (string): The revision (commit hash, branch name, tag) to show
   - Returns: Contents of the specified commit
12. `git_init`
   - Initializes a Git repository
   - Inputs:
     - `repo_path` (string): Path to directory to initialize git repo
   - Returns: Confirmation of repository initialization

## Installation

### Using uv (recommended)

When using [`uv`](https://docs.astral.sh/uv/) no specific installation is needed. We will
use [`uvx`](https://docs.astral.sh/uv/guides/tools/) to directly run *mcp-server-git*.

### Using PIP

Alternatively you can install `mcp-server-git` via pip:

```
pip install mcp-server-git
```

After installation, you can run it as a script using:

```
python -m mcp_server_git
```

## Configuration

### Usage with Claude Desktop

Add this to your `claude_desktop_config.json`:

<details>
<summary>Using uvx</summary>

```json
"mcpServers": {
  "git": {
    "command": "uvx",
    "args": ["mcp-server-git", "--repository", "path/to/git/repo"]
  }
}
```
</details>

<details>
<summary>Using docker</summary>

* Note: replace '/Users/username' with the a path that you want to be accessible by this tool

```json
"mcpServers": {
  "git": {
    "command": "docker",
    "args": ["run", "--rm", "-i", "--mount", "type=bind,src=/Users/username,dst=/Users/username", "mcp/git"]
  }
}
```
</details>

<details>
<summary>Using pip installation</summary>

```json
"mcpServers": {
  "git": {
    "command": "python",
    "args": ["-m", "mcp_server_git", "--repository", "path/to/git/repo"]
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
  "mcp-server-git": {
    "command": {
      "path": "uvx",
      "args": ["mcp-server-git"]
    }
  }
],
```
</details>

<details>
<summary>Using pip installation</summary>

```json
"context_servers": {
  "mcp-server-git": {
    "command": {
      "path": "python",
      "args": ["-m", "mcp_server_git"]
    }
  }
},
```
</details>

## Debugging

You can use the MCP inspector to debug the server. For uvx installations:

```
npx @modelcontextprotocol/inspector uvx mcp-server-git
```

Or if you've installed the package in a specific directory or are developing on it:

```
cd path/to/servers/src/git
npx @modelcontextprotocol/inspector uv run mcp-server-git
```

Running `tail -n 20 -f ~/Library/Logs/Claude/mcp*.log` will show the logs from the server and may
help you debug any issues.

## Development

If you are doing local development, there are two ways to test your changes:

1. Run the MCP inspector to test your changes. See [Debugging](#debugging) for run instructions.

2. Test using the Claude desktop app. Add the following to your `claude_desktop_config.json`:

### Docker

```json
{
  "mcpServers": {
    "git": {
      "command": "docker",
      "args": [
        "run",
        "--rm",
        "-i",
        "--mount", "type=bind,src=/Users/username/Desktop,dst=/projects/Desktop",
        "--mount", "type=bind,src=/path/to/other/allowed/dir,dst=/projects/other/allowed/dir,ro",
        "--mount", "type=bind,src=/path/to/file.txt,dst=/projects/path/to/file.txt",
        "mcp/git"
      ]
    }
  }
}
```

### UVX
```json
{
"mcpServers": {
  "git": {
    "command": "uv",
    "args": [ 
      "--directory",
      "/<path to mcp-servers>/mcp-servers/src/git",
      "run",
      "mcp-server-git"
    ]
  }
}
```

## Build

Docker build:

```bash
cd src/git
docker build -t mcp/git .
```

## VS Code Installation

### Manual Installation

Add the following to your `.vscode/mcp.json` file:

#### Using Python

```json
{
  "git": {
    "inputs": [
      {
        "id": "git_repository_path",
        "description": "Path to Git repository"
      }
    ],
    "command": "python",
    "args": [
      "-m",
      "mcp_server_git",
      "--repository",
      "${input:git_repository_path}"
    ]
  }
}
```

#### Using Docker

```json
{
  "git": {
    "inputs": [
      {
        "id": "workspace_path",
        "description": "Path to directory containing Git repositories",
        "default": "${workspaceFolder}"
      }
    ],
    "command": "docker",
    "args": [
      "run",
      "--rm",
      "-i",
      "--mount",
      "type=bind,src=${input:workspace_path},dst=/mounted-workspace",
      "mcp/git"
    ]
  }
}
```

## License
