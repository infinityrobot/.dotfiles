# CLAUDE

- When creating a PR in GitHub, add me as the assignee.

## Obsidian CLI

Use the `obsidian` CLI for all Obsidian vault interactions. The CLI connects to the **Notes** vault via a local Obsidian plugin. Obsidian must be open for commands to work.

### Core Concepts

- `file=<name>` resolves by name (like wikilinks); `path=<path>` is an exact folder/file path.
- Most commands default to the active file when `file`/`path` is omitted.
- Quote values with spaces: `name="My Note"`.
- Use `\n` for newline, `\t` for tab in content values.
- Use `--format=json` (or `format=json`) for parseable output wherever supported.

### Searching

```bash
obsidian search query="search text"                    # Full-text search
obsidian search query="text" path="folder" limit=10    # Scoped search
obsidian search:context query="text"                   # Search with matching line context
obsidian search:context query="text" format=json       # Parseable JSON output
```

### Reading Notes

```bash
obsidian read file="Note Name"          # Read by wikilink name
obsidian read path="folder/note.md"     # Read by exact path
obsidian file file="Note Name"          # Show file info (path, size, dates)
obsidian outline file="Note Name"       # Show heading structure
```

### Creating Notes

```bash
obsidian create name="New Note"                              # Create empty note
obsidian create name="New Note" content="# Title\nBody"      # Create with content
obsidian create path="folder/note.md" content="text"         # Create at specific path
obsidian create name="New Note" template="Template Name"     # Create from template
```

### Appending / Prepending

```bash
obsidian append file="Note" content="New content"      # Append to end
obsidian prepend file="Note" content="New content"     # Prepend to start
obsidian append file="Note" content="inline" inline    # Append without newline
```

### Properties (Frontmatter)

```bash
obsidian properties file="Note"                         # List properties for a file
obsidian properties format=json                         # All vault properties as JSON
obsidian property:read name="status" file="Note"        # Read a specific property
obsidian property:set name="status" value="done" file="Note"   # Set a property
obsidian property:set name="tags" value="tag1,tag2" type=list file="Note"  # Set list property
obsidian property:remove name="status" file="Note"      # Remove a property
```

### Daily Notes

```bash
obsidian daily                                          # Open today's daily note
obsidian daily:read                                     # Read today's daily note
obsidian daily:path                                     # Get daily note file path
obsidian daily:append content="- Task or log entry"     # Append to daily note
obsidian daily:prepend content="# Morning\nNotes"       # Prepend to daily note
```

### Tags

```bash
obsidian tags                              # List all tags
obsidian tags counts sort=count            # Tags sorted by frequency
obsidian tags file="Note"                  # Tags for a specific file
obsidian tags format=json                  # Parseable JSON output
obsidian tag name="tagname" verbose        # Tag details with file list
```

### Backlinks & Links

```bash
obsidian backlinks file="Note"             # List files linking to this note
obsidian backlinks file="Note" format=json # Parseable JSON output
obsidian links file="Note"                 # List outgoing links from a note
obsidian orphans                           # Files with no incoming links
obsidian deadends                          # Files with no outgoing links
obsidian unresolved                        # Broken/unresolved links
```

### File Management

```bash
obsidian files                             # List all files
obsidian files folder="subfolder"          # List files in a folder
obsidian folders                           # List all folders
obsidian move file="Note" to="new/path"    # Move or rename
obsidian rename file="Note" name="New"     # Rename
obsidian delete file="Note"                # Delete (to trash)
```

### Tasks

```bash
obsidian tasks                             # List all tasks
obsidian tasks todo                        # Incomplete tasks only
obsidian tasks done                        # Completed tasks only
obsidian tasks daily                       # Tasks from daily note
obsidian tasks file="Note" format=json     # Tasks in a file as JSON
obsidian task file="Note" line=5 toggle    # Toggle task status
```

### Vault Info

```bash
obsidian vault                             # Vault name, path, file/folder counts, size
obsidian vaults                            # List all known vaults
```
