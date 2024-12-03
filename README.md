# Video Jungle MCP server

Upload, edit, and generate videos from your LLM

## Components

### Resources

The server implements a simple note storage system with:
- Custom vj:// URI scheme for accessing individual videos and project
- Each project resource has a name, description

### Prompts

WIP

### Tools

The server implements a few tools:
- list-videos: List all your Videos on Video Jungle
  - Returns a list of all videos available
- add-video: Add a video from a URL
  - Returns an vj:// URI to reference the Video file
- search-videos: Search videos using embeddings
  - Returns video matches based upon embeddings and keywords
- generate-edit: Generate an edit based upon Video Files
  - Returns a URI for finished video edit

## Configuration

You must login to [Video Jungle settings](https://app.video-jungle.com/profile/settings), and get your API key. Set this as an environment variable named `VJ_API_KEY`.

```bash
$ export VJ_API_KEY=yourapikey
```

## Quickstart

### Install

#### Claude Desktop

On MacOS: `~/Library/Application\ Support/Claude/claude_desktop_config.json`
On Windows: `%APPDATA%/Claude/claude_desktop_config.json`

<details>
  <summary>Development/Unpublished Servers Configuration</summary>
  ```
  "mcpServers": {
    "video-jungle-mcp": {
      "command": "uv",
      "args": [
        "--directory",
        "/Users/stankley/Development/video-jungle-mcp",
        "run",
        "video-jungle-mcp"
      ]
    }
  }
  ```
</details>

<details>
  <summary>Published Servers Configuration</summary>
  ```
  "mcpServers": {
    "video-jungle-mcp": {
      "command": "uvx",
      "args": [
        "video-jungle-mcp"
      ]
    }
  }
  ```
</details>

## Development

### Building and Publishing

To prepare the package for distribution:

1. Sync dependencies and update lockfile:
```bash
uv sync
```

2. Build package distributions:
```bash
uv build
```

This will create source and wheel distributions in the `dist/` directory.

3. Publish to PyPI:
```bash
uv publish
```

Note: You'll need to set PyPI credentials via environment variables or command flags:
- Token: `--token` or `UV_PUBLISH_TOKEN`
- Or username/password: `--username`/`UV_PUBLISH_USERNAME` and `--password`/`UV_PUBLISH_PASSWORD`

### Debugging

Since MCP servers run over stdio, debugging can be challenging. For the best debugging
experience, we strongly recommend using the [MCP Inspector](https://github.com/modelcontextprotocol/inspector).


You can launch the MCP Inspector via [`npm`](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) with this command:

```bash
npx @modelcontextprotocol/inspector uv --directory /Users/stankley/Development/video-jungle-mcp run video-jungle-mcp
```


Upon launching, the Inspector will display a URL that you can access in your browser to begin debugging.