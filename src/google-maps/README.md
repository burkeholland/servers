# Google Maps MCP Server

MCP Server for the Google Maps API.

[![Install with NPM in VS Code](https://img.shields.io/badge/VS_Code-NPM-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/redirect?url=vscode:mcp/install?%7B%22name%22%3A%22google-maps%22%2C%22command%22%3A%22npx%22%2C%22args%22%3A%5B%22-y%22%2C%22%40modelcontextprotocol%2Fserver-google-maps%22%5D%2C%22env%22%3A%7B%22GOOGLE_MAPS_API_KEY%22%3A%22%24%7Binput%3Agoogle_maps_api_key%7D%22%7D%2C%22inputs%22%3A%5B%7B%22id%22%3A%22google_maps_api_key%22%2C%22description%22%3A%22Google%20Maps%20API%20Key%22%2C%22password%22%3Atrue%7D%5D%7D) [![Install with NPM in VS Code Insiders](https://img.shields.io/badge/VS_Code_Insiders-NPM-24bfa5?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect?url=vscode-insiders:mcp/install?%7B%22name%22%3A%22google-maps%22%2C%22command%22%3A%22npx%22%2C%22args%22%3A%5B%22-y%22%2C%22%40modelcontextprotocol%2Fserver-google-maps%22%5D%2C%22env%22%3A%7B%22GOOGLE_MAPS_API_KEY%22%3A%22%24%7Binput%3Agoogle_maps_api_key%7D%22%7D%2C%22inputs%22%3A%5B%7B%22id%22%3A%22google_maps_api_key%22%2C%22description%22%3A%22Google%20Maps%20API%20Key%22%2C%22password%22%3Atrue%7D%5D%7D)

[![Install with Docker in VS Code](https://img.shields.io/badge/VS_Code-Docker-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/redirect?url=vscode:mcp/install?%7B%22name%22%3A%22google-maps%22%2C%22command%22%3A%22docker%22%2C%22args%22%3A%5B%22run%22%2C%22-i%22%2C%22--rm%22%2C%22-e%22%2C%22GOOGLE_MAPS_API_KEY%22%2C%22mcp%2Fgoogle-maps%22%5D%2C%22env%22%3A%7B%22GOOGLE_MAPS_API_KEY%22%3A%22%24%7Binput%3Agoogle_maps_api_key%7D%22%7D%2C%22inputs%22%3A%5B%7B%22id%22%3A%22google_maps_api_key%22%2C%22description%22%3A%22Google%20Maps%20API%20Key%22%2C%22password%22%3Atrue%7D%5D%7D) [![Install with Docker in VS Code Insiders](https://img.shields.io/badge/VS_Code_Insiders-Docker-24bfa5?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect?url=vscode-insiders:mcp/install?%7B%22name%22%3A%22google-maps%22%2C%22command%22%3A%22docker%22%2C%22args%22%3A%5B%22run%22%2C%22-i%22%2C%22--rm%22%2C%22-e%22%2C%22GOOGLE_MAPS_API_KEY%22%2C%22mcp%2Fgoogle-maps%22%5D%2C%22env%22%3A%7B%22GOOGLE_MAPS_API_KEY%22%3A%22%24%7Binput%3Agoogle_maps_api_key%7D%22%7D%2C%22inputs%22%3A%5B%7B%22id%22%3A%22google_maps_api_key%22%2C%22description%22%3A%22Google%20Maps%20API%20Key%22%2C%22password%22%3Atrue%7D%5D%7D)

## Tools

1. `maps_geocode`
   - Convert address to coordinates
   - Input: `address` (string)
   - Returns: location, formatted_address, place_id

2. `maps_reverse_geocode`
   - Convert coordinates to address
   - Inputs:
     - `latitude` (number)
     - `longitude` (number)
   - Returns: formatted_address, place_id, address_components

3. `maps_search_places`
   - Search for places using text query
   - Inputs:
     - `query` (string)
     - `location` (optional): { latitude: number, longitude: number }
     - `radius` (optional): number (meters, max 50000)
   - Returns: array of places with names, addresses, locations

4. `maps_place_details`
   - Get detailed information about a place
   - Input: `place_id` (string)
   - Returns: name, address, contact info, ratings, reviews, opening hours

5. `maps_distance_matrix`
   - Calculate distances and times between points
   - Inputs:
     - `origins` (string[])
     - `destinations` (string[])
     - `mode` (optional): "driving" | "walking" | "bicycling" | "transit"
   - Returns: distances and durations matrix

6. `maps_elevation`
   - Get elevation data for locations
   - Input: `locations` (array of {latitude, longitude})
   - Returns: elevation data for each point

7. `maps_directions`
   - Get directions between points
   - Inputs:
     - `origin` (string)
     - `destination` (string)
     - `mode` (optional): "driving" | "walking" | "bicycling" | "transit"
   - Returns: route details with steps, distance, duration

## Setup

### API Key
Get a Google Maps API key by following the instructions [here](https://developers.google.com/maps/documentation/javascript/get-api-key#create-api-keys).

### Usage with Claude Desktop

Add the following to your `claude_desktop_config.json`:

#### Docker

```json
{
  "mcpServers": {
    "google-maps": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "-e",
        "GOOGLE_MAPS_API_KEY",
        "mcp/google-maps"
      ],
      "env": {
        "GOOGLE_MAPS_API_KEY": "<YOUR_API_KEY>"
      }
    }
  }
}
```

### NPX

```json
{
  "mcpServers": {
    "google-maps": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-google-maps"
      ],
      "env": {
        "GOOGLE_MAPS_API_KEY": "<YOUR_API_KEY>"
      }
    }
  }
}
```

## Build

Docker build:

```bash
docker build -t mcp/google-maps -f src/google-maps/Dockerfile .
```

## VS Code Installation

### Manual Installation

Add the following to your `.vscode/mcp.json` file:

#### Using NPM

```json
{
  "google-maps": {
    "inputs": [
      {
        "id": "google_maps_api_key",
        "description": "Google Maps API Key",
        "password": true
      }
    ],
    "command": "npx",
    "args": [
      "-y",
      "@modelcontextprotocol/server-google-maps"
    ],
    "env": {
      "GOOGLE_MAPS_API_KEY": "${input:google_maps_api_key}"
    }
  }
}
```

#### Using Docker

```json
{
  "google-maps": {
    "inputs": [
      {
        "id": "google_maps_api_key",
        "description": "Google Maps API Key",
        "password": true
      }
    ],
    "command": "docker",
    "args": [
      "run",
      "-i",
      "--rm",
      "-e",
      "GOOGLE_MAPS_API_KEY",
      "mcp/google-maps"
    ],
    "env": {
      "GOOGLE_MAPS_API_KEY": "${input:google_maps_api_key}"
    }
  }
}
```

## License

This MCP server is licensed under the MIT License. This means you are free to use, modify, and distribute the software, subject to the terms and conditions of the MIT License. For more details, please see the LICENSE file in the project repository.
