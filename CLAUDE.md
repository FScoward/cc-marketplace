# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a Claude Code plugin marketplace repository (`cc-marketplace`). It serves as a collection of Claude Code plugins that extend the functionality of Claude Code CLI.

## Architecture

### Plugin Structure

Each plugin follows the standard Claude Code plugin structure:

```
<plugin-name>/
├── .claude-plugin/
│   └── plugin.json          # Plugin metadata (name, description, version, author)
├── agents/                   # Custom agents (optional)
└── commands/                 # Custom slash commands (optional)
```

### Plugin Metadata

The `plugin.json` file contains:
- `name`: Plugin identifier
- `description`: Brief description of plugin purpose
- `version`: Semantic version
- `author`: Object with author `name`

## Development Workflow

### Adding a New Plugin

1. Create a new directory at the root level with the plugin name
2. Add `.claude-plugin/plugin.json` with required metadata
3. Optionally add `agents/` and `commands/` directories
4. Commit the plugin to the repository

### Plugin Installation

Users can install plugins from this marketplace by referencing the plugin directory path or by following Claude Code plugin installation procedures.

## Current Plugins

- **dev-plugin**: Development plugin template with basic configuration
