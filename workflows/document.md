# Workflow: Document

Create or improve documentation.

## Usage

> "Document src/utils/auth.ts" (code comments)
> "Document the README" (system docs)
> "Document the API for /users endpoint" (API docs)

## Routing

| Input | Approach |
|-------|----------|
| Source code file (`.ts`, `.py`, `.go`) | Code comment audit using [documenting-code-comments](../skills/documenting-code-comments.md) |
| Markdown file or README | System documentation using [documenting-systems](../skills/documenting-systems.md) |
| API docs request | API documentation using system docs skill |
| Architecture overview | Architecture docs with [visualizing-with-mermaid](../skills/visualizing-with-mermaid.md) |

## Code Comment Workflow

1. Read target file completely
2. Audit comments: categorize each one
3. Apply fixes: remove unnecessary, rewrite unclear
4. Report: summarize removals, rewrites, suggested refactors

## Documentation Workflow

1. Read source files, types, route definitions
2. Plan structure using progressive disclosure
3. Write documentation following [writer](../skills/writer.md) Engineer persona
4. Cross-reference related docs

## Location Standards

| Doc Type | Location | Pattern |
|----------|----------|---------|
| Project overview | Root | README.md |
| API reference | /docs/api/ | {resource-name}.md |
| Architecture | /docs/architecture/ | {topic}.md |
| Guides | /docs/guides/ | {topic}.md |
