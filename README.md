# Nomicon CLI

![Status: Work in Progress](https://img.shields.io/badge/Status-Work_in_Progress-warning)
![License: MIT](https://img.shields.io/badge/License-MIT-blue)

> A lightweight Personal Knowledge Management CLI tool built in Go.

**Nomicon** is a command-line interface focused on agile `.md` file management. Designed to function as a "second brain" or personal grimoire directly from the terminal, it brings the power of tools like Obsidian (Zettelkasten, bidirectional links, frontmatter) without breaking your workflow in the shell.

## 🚀 The Concept

The goal of Nomicon is not to replace text editors, but to orchestrate them. It allows for quick note creation, idea logging via quick-capture, and the visualization of complex relationships between your files, all isolated within different Workspaces (Vaults). 

## ✨ Planned Features

- **Workspace Management:** Isolate your projects (code, novels, studies) into different directories.
- **Native Zettelkasten:** Support for Obsidian-style `[[links]]` and backlink listings.
- **Quick Capture:** Append or prepend text to existing files without opening an editor.
- **Terminal Rendering:** Read your Markdown files with color and style formatting directly in the shell output.
- **Global Search & Stats:** Find what you need with full-text search and track your writing volume.

---

## 🛠️ Command Reference (Draft)

### 🗂️ Workspace Management (Vaults)
- `nomicon register <name> <path>`: Saves a specific directory linked to an alias (e.g., maps `/home/project/` to `project`).
- `nomicon connect <name>`: Changes the CLI context. All subsequent commands will only apply within this directory.
- `nomicon status`: Shows the currently active workspace/directory.
- `nomicon workspaces`: Lists all registered directories and highlights the active one.

### 📝 Creation, Editing & Organization
- `nomicon new <title>`: Creates a new note. Automatically generates a YAML Frontmatter at the top.
  - `--alias`: Sets a shortcut alias for quick access.
  - `--category` or `--cat`: Adds a category (organizing into subfolders).
  - `--template`: Creates the file using a pre-defined structure.
- `nomicon log <alias or title> "text"`: Inserts text quickly into a note.
  - `--append` or `--prepend`: Chooses whether the text goes to the top or bottom of the file (bottom by default).
- `nomicon log default prepend` / `append`: Changes the default logging behavior.
- `nomicon tag add <alias> <#tag>`: Adds tags to the YAML Frontmatter.
- `nomicon tag list <#tag>`: Filters and searches notes by their tags.
- `nomicon edit <alias>`: Opens the file directly in the system's default editor (via the `$EDITOR` environment variable).

### 🔍 Reading, Search & Statistics
- `nomicon read <alias or title>`: Renders formatted/colored markdown in the terminal.
- `nomicon dump --cat <name>`: Reads and displays all content from a category, separated by file.
  - `--date`: Sorts the reading output by date instead of alphabetically.
- `nomicon ls`: Lists the file tree grouped by category. Accepts a `--recent` flag.
- `nomicon find <text>`: Performs a full-text search inside all notes in the current workspace.
- `nomicon stats` or `count <category/alias>`: Returns quick statistics (e.g., word count, characters, estimated reading time) for a specific file or the entire workspace (e.g., tracking the word count on the rules for a game).

### 🕸️ Connections & Graphs (Zettelkasten)
- `nomicon link <alias1> <alias2>`: Injects a `[[alias2]]` wikilink into file 1.
  - `--type "relationship"`: Registers the relationship type in the YAML.
- `nomicon backlinks <alias>`: Scans the workspace and lists all files mentioning or linking to the alias (e.g., `nomicon backlinks ismiral`).
- `nomicon graph`: Generates an ASCII representation of the file's connections in the terminal or exports the map.
