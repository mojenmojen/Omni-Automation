# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This repository contains Omni Automation plug-ins for OmniFocus (task management app) using the Omni Automation JavaScript API. Plug-ins are written in JavaScript and extend OmniFocus functionality.

## File Conventions

- **File extensions**: `.omnijs` or `.omnifocusjs` for OmniFocus plug-ins
- **Plug-in metadata**: Each plug-in starts with a JSON comment block defining `type`, `author`, `version`, and `description`
- **Author attribution**: Plug-ins include `// Twitter: @unlocked2412` comment

## Plug-in Architecture

All plug-ins follow this structure:

```javascript
/*{
    "type": "action",
    "author": "unlocked2412",
    "version": "0.1",
    "description": "Description here"
}*/
(() =>
    Object.assign(
        new PlugIn.Action(selection => {
            const omniJSContext = () => {
                const main = () => {
                    // Main logic here
                };
                // Helper functions...
                return main();
            };
            return omniJSContext();
        }), {
            validate: selection => /* validation logic */
        })
)();
```

Key patterns:
- **IIFE wrapper**: All plug-ins use immediately-invoked function expressions
- **`PlugIn.Action`**: Creates an action that operates on the current selection
- **`validate`**: Function determining when the action is available (e.g., `selection.tasks.length > 0`)
- **Functional style**: Code uses functional programming patterns with helper functions from [prelude-jxa](https://github.com/RobTrew/prelude-jxa)

## OmniFocus API Objects

Common objects used in plug-ins:
- `selection.tasks` / `selection.projects` - Currently selected items
- `document.windows[0]` - Main window
- `win.content` - Content tree for navigation
- `flattenedTasks` / `flattenedProjects` / `flattenedTags` - All items in database
- `task.deferDate` / `task.dueDate` - Date properties
- `settings.objectForKey('DefaultStartTime')` - App settings

## Plug-in Categories

- **Change Defer Date**: Modify defer dates by relative amounts (+1 day, +1 week, etc.)
- **Postpone Due Date**: Modify due dates by relative amounts
- **Organize**: Reorder tasks (Move To Top, Move To Bottom, Convert Tasks to Projects)
- **Sharing**: Share tasks filtered by tags
- **Statistics**: Display OmniFocus database statistics

## Installation

Users install plug-ins by double-clicking `.omnifocusjs` files and selecting the OmniFocus iCloud Drive location, or by linking a custom folder via `Automation > Configure... > Add Linked Folder...`
