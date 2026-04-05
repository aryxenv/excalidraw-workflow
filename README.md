# Excalidraw Workflow

A ready-to-use template for creating architecture diagrams with [Excalidraw MCP](https://github.com/patchli/excalidraw-mcp-server) and Copilot CLI.

Ask Copilot to "create an architecture diagram" and it will research your codebase, build the diagram in Excalidraw, and export a PNG.

## What's Included

```
.github/
├── agents/
│   └── diagrammer.agent.md    # Copilot agent that researches code & draws diagrams
├── skills/
│   └── excalidraw-diagrams/
│       └── SKILL.md            # Skill with export pipeline & design guidelines
└── copilot-instructions.md     # Project-level Copilot context
excalidraw/
├── diagrams/                   # .excalidraw source files
│   └── export/                 # Exported PNGs (+ intermediate SVGs)
├── scripts/
│   └── svg-to-png.js           # SVG → dark-mode PNG converter
└── package.json                # @resvg/resvg-js dependency
```

## Prerequisites

- [Copilot CLI](https://github.com/features/copilot/cli) (`copilot`)
- [Node.js](https://nodejs.org/) 18+
- The Excalidraw MCP server (runs automatically via `npx`)

## Getting Started

1. **Clone this repo** (or use it as a template).

2. **Install export dependencies:**

   ```bash
   cd excalidraw && npm install
   ```

3. **Ask Copilot to create a diagram:**

   ```bash
   copilot -p "create an architecture diagram for this project"
   ```

   The `@diagrammer` agent and `excalidraw-diagrams` skill activate on keywords like "diagram", "visualize", or "architecture".

4. **Review & export.** Copilot will:
   - Research your codebase to identify components and connections
   - Build the diagram using Excalidraw MCP tools
   - Export an SVG, convert it to a dark-mode PNG, and embed it in your docs

## Export Pipeline

The export script converts Excalidraw SVG exports into 1600px-wide dark-mode PNGs:

```bash
cd excalidraw
node scripts/svg-to-png.js diagrams/export/architecture.svg
```

Output lands next to the input file as `architecture.png`.

## Customizing for Your Project

1. **Update `.github/copilot-instructions.md`** with your project's architecture, tech stack, and conventions so the diagrammer agent has accurate context.
2. **Edit the skill** (`.github/skills/excalidraw-diagrams/SKILL.md`) to adjust colour palettes, layout rules, or export settings.
3. **Edit the agent** (`.github/agents/diagrammer.agent.md`) to change the research-then-draw workflow or add constraints.
