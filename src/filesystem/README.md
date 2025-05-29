# Filesystem MCP Server (Custom Version)

This is a customized version of the Filesystem MCP server that modifies tool descriptions to de-emphasize the `edit` and `write` functions in favor of other tools that provide better visibility of changes.

## Security

The server is designed with security in mind:

- Only directories explicitly specified as command-line arguments are accessible
- Path traversal attacks are prevented by validating all paths
- Symlinks are checked to ensure they don't point outside allowed directories
- Parent directories are validated for new file creation

## Usage

```bash
npx @modelcontextprotocol/filesystem-server ~/allowed/directory1 /another/allowed/directory
```

You can specify multiple directories to allow access to.

## Available Tools

- `read_file`: Read the contents of a file
- `read_multiple_files`: Read the contents of multiple files at once
- `write_file`: (LOW PRIORITY) Create a new file or overwrite an existing file - consider using other tools instead
- `edit_file`: (LOW PRIORITY) Make line-based edits to a text file - consider using other tools instead
- `create_directory`: Create a new directory
- `list_directory`: List the contents of a directory
- `directory_tree`: Get a recursive tree view of files and directories
- `move_file`: Move or rename a file or directory
- `search_files`: Search for files matching a pattern
- `get_file_info`: Get metadata about a file or directory
- `list_allowed_directories`: List the directories that the server is allowed to access

## Tool Priority

This custom version modifies the descriptions of `write_file` and `edit_file` to indicate they should be used with caution and as a lower priority compared to other tools that provide better visibility of changes.

## Examples

### Reading a file

```json
{
  "name": "read_file",
  "arguments": {
    "path": "~/Documents/notes.txt"
  }
}
```

### Writing a file (use with caution)

```json
{
  "name": "write_file",
  "arguments": {
    "path": "~/Documents/new-file.txt",
    "content": "Hello, world!"
  }
}
```

### Editing a file (use with caution)

```json
{
  "name": "edit_file",
  "arguments": {
    "path": "~/Documents/config.json",
    "edits": [
      {
        "oldText": "  \"debug\": false,",
        "newText": "  \"debug\": true,"
      }
    ]
  }
}
```

### Creating a directory

```json
{
  "name": "create_directory",
  "arguments": {
    "path": "~/Documents/new-project/src"
  }
}
```

### Listing a directory

```json
{
  "name": "list_directory",
  "arguments": {
    "path": "~/Documents"
  }
}
```

### Getting a directory tree

```json
{
  "name": "directory_tree",
  "arguments": {
    "path": "~/Documents/project"
  }
}
```

### Moving a file

```json
{
  "name": "move_file",
  "arguments": {
    "source": "~/Documents/old-name.txt",
    "destination": "~/Documents/new-name.txt"
  }
}
```

### Searching for files

```json
{
  "name": "search_files",
  "arguments": {
    "path": "~/Documents",
    "pattern": "report",
    "excludePatterns": ["node_modules", ".git"]
  }
}
```

### Getting file info

```json
{
  "name": "get_file_info",
  "arguments": {
    "path": "~/Documents/report.pdf"
  }
}
```

### Listing allowed directories

```json
{
  "name": "list_allowed_directories",
  "arguments": {}
}
```
