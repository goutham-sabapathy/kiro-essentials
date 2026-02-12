# Documenting Systems

Creates task-oriented technical documentation with progressive disclosure. Use when writing READMEs, API docs, architecture docs, or markdown documentation.

## Core Principles

### 1. Progressive Disclosure

| Layer | Content | User Question |
|-------|---------|---------------|
| 1 | One-sentence description | What is it? |
| 2 | Quick start code block | How do I use it? |
| 3 | Full API reference | What are my options? |
| 4 | Architecture deep dive | How does it work? |

**Warnings, breaking changes, and prerequisites go at the TOP.**

### 2. Task-Oriented Writing

```markdown
<!-- Bad: Feature-oriented -->
## AuthService Class
The AuthService class provides authentication methods...

<!-- Good: Task-oriented -->
## Authenticating Users
To authenticate a user, call login() with credentials:
```

### 3. Show, Don't Tell

Every concept needs a concrete example.

## Formatting Standards

- **Sentence case headings**: "Getting started" not "Getting Started"
- **Max 3 heading levels**: Deeper means split the doc
- **Always specify language** in code blocks
- **Relative paths** for internal links
- **Tables** for structured data with 3+ attributes

## Quality Checklist

- [ ] Code examples tested and runnable
- [ ] No placeholder text or TODOs
- [ ] Matches actual code behavior
- [ ] Scannable without reading everything
- [ ] Reader knows what to do next

## Anti-Patterns

| Problem | Fix |
|---------|-----|
| Wall of text | Break up with headings, bullets, code, tables |
| Buried critical info | Warnings/breaking changes at TOP |
| Missing error docs | Always document what can go wrong |

## Templates

### README Template

```markdown
# Project Name

One-sentence description.

## Quick start

\`\`\`bash
npm install project-name
npm start
\`\`\`

## Prerequisites

- Node.js 18+
- PostgreSQL 15+

## Configuration

[Environment variables, config files]

## Usage

[Core workflows with examples]

## API Reference

[If applicable]

## Contributing

[How to contribute]
```

### API Endpoint Template

```markdown
## Create user

\`POST /api/users\`

Creates a new user account.

**Request:**
\`\`\`json
{ "email": "user@example.com", "name": "Test User" }
\`\`\`

**Response (201):**
\`\`\`json
{ "id": "usr_123", "email": "user@example.com" }
\`\`\`

**Errors:**
| Status | Code | Description |
|--------|------|-------------|
| 400 | VALIDATION_ERROR | Missing required fields |
| 409 | DUPLICATE_EMAIL | Email already registered |
```

## File Organization

| Doc Type | Location | Filename Pattern |
|----------|----------|------------------|
| Project overview | Root | README.md |
| API reference | /docs/api/ | {resource-name}.md |
| Architecture | /docs/architecture/ | {topic}.md |
| Guides/How-to | /docs/guides/ | {topic}.md |
