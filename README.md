# Kiro Essentials

A curated collection of development skills, workflows, and personas adapted for [Kiro CLI](https://kiro.dev), ported from [claude-essentials](https://github.com/rileyhilliard/claude-essentials).

## What's Included

### Skills (20)

Reusable development methodologies and best practices. Point Kiro at this repo and reference these when working on projects.

**Testing & Quality:**

| Skill | Description |
|-------|-------------|
| [writing-tests](skills/writing-tests.md) | Testing Trophy methodology, behavior-focused tests |
| [verification-before-completion](skills/verification-before-completion.md) | Verify before claiming success |
| [fixing-flaky-tests](skills/fixing-flaky-tests.md) | Diagnose and fix tests that fail concurrently |
| [condition-based-waiting](skills/condition-based-waiting.md) | Replace race conditions with polling |

**Debugging & Problem Solving:**

| Skill | Description |
|-------|-------------|
| [systematic-debugging](skills/systematic-debugging.md) | Four-phase debugging framework |
| [reading-logs](skills/reading-logs.md) | Efficient log analysis using targeted search |

**Code Quality:**

| Skill | Description |
|-------|-------------|
| [refactoring-code](skills/refactoring-code.md) | Behavior-preserving code improvements |
| [optimizing-performance](skills/optimizing-performance.md) | Measurement-driven optimization |
| [handling-errors](skills/handling-errors.md) | Error handling best practices |
| [migrating-code](skills/migrating-code.md) | Safe migration patterns |

**Planning & Execution:**

| Skill | Description |
|-------|-------------|
| [writing-plans](skills/writing-plans.md) | Create detailed implementation plans |
| [executing-plans](skills/executing-plans.md) | Execute plans in controlled batches |
| [architecting-systems](skills/architecting-systems.md) | Clean, scalable system architecture |
| [design](skills/design.md) | Frontend design principles |

**Documentation & Writing:**

| Skill | Description |
|-------|-------------|
| [writer](skills/writer.md) | Writing style guide with 7 personas |
| [strategy-writer](skills/strategy-writer.md) | Executive-quality strategic documents |
| [documenting-systems](skills/documenting-systems.md) | Markdown documentation best practices |
| [documenting-code-comments](skills/documenting-code-comments.md) | Self-documenting code standards |

**Data & Infrastructure:**

| Skill | Description |
|-------|-------------|
| [managing-databases](skills/managing-databases.md) | PostgreSQL, DuckDB, Parquet, PGVector |

**Meta:**

| Skill | Description |
|-------|-------------|
| [visualizing-with-mermaid](skills/visualizing-with-mermaid.md) | Professional technical diagrams |

### Workflows (14)

Step-by-step prompt templates for common development tasks.

| Workflow | Description |
|----------|-------------|
| [test](workflows/test.md) | Run tests and analyze failures |
| [explain](workflows/explain.md) | Break down code or concepts |
| [debug](workflows/debug.md) | Launch systematic debugging |
| [optimize](workflows/optimize.md) | Find performance bottlenecks |
| [refactor](workflows/refactor.md) | Improve code quality |
| [review](workflows/review.md) | Comprehensive code review |
| [commit](workflows/commit.md) | Generate semantic commit messages |
| [deps](workflows/deps.md) | Audit and upgrade dependencies |
| [fix-issue](workflows/fix-issue.md) | Fix a GitHub issue by number |
| [pr](workflows/pr.md) | Create a PR with auto-generated description |
| [document](workflows/document.md) | Create or improve documentation |
| [plan](workflows/plan.md) | Create implementation plans |
| [execute](workflows/execute.md) | Execute an implementation plan |
| [init](workflows/init.md) | Bootstrap repo configuration |

### Personas (4)

Behavioral prompts that shape how Kiro approaches a task.

| Persona | Description |
|---------|-------------|
| [code-reviewer](personas/code-reviewer.md) | Comprehensive PR/MR reviews |
| [devils-advocate](personas/devils-advocate.md) | Rigorous critique of plans and designs |
| [log-reader](personas/log-reader.md) | Efficient log file analysis |
| [task-executor](personas/task-executor.md) | Lightweight task execution |

### Scripts (6)

Shell scripts for log analysis, usable directly via bash.

| Script | Description |
|--------|-------------|
| [aggregate-errors.sh](scripts/aggregate-errors.sh) | Aggregate errors by frequency |
| [extract-stack-traces.sh](scripts/extract-stack-traces.sh) | Extract and group stack traces |
| [parse-json-logs.sh](scripts/parse-json-logs.sh) | Parse JSON logs with jq |
| [slow-requests.sh](scripts/slow-requests.sh) | Find slow operations by duration |
| [timeline.sh](scripts/timeline.sh) | Error distribution over time |
| [trace-request.sh](scripts/trace-request.sh) | Trace request ID across log files |

## How to Use with Kiro

### Option 1: Index as a Knowledge Base (Recommended)

This is the most powerful approach. Once indexed, Kiro can automatically search and apply the right skill for any task.

**Step 1:** In a Kiro CLI chat session, point Kiro at this repo:

```
Can you use /path/to/kiro-essentials?
```

**Step 2:** Ask Kiro to index it:

```
Index /path/to/kiro-essentials as a knowledge base
```

**Step 3:** Use it naturally. Kiro will search the knowledge base and apply relevant skills:

```
Help me debug this error: TypeError: Cannot read property 'id' of undefined
```
```
Review my PR against main
```
```
Write tests for src/auth/login.ts
```
```
Create an implementation plan for adding real-time notifications
```

You don't need to name specific skills. Kiro searches the indexed content and pulls in the relevant methodology. But you can be explicit if you want:

```
Use the systematic-debugging skill to investigate this bug
```
```
Apply the code-reviewer persona to review my changes
```

### Option 2: Reference Files Directly

Point Kiro at specific files when you want a particular methodology:

```
Read kiro-essentials/skills/writing-tests.md and apply that approach to my test suite
```
```
Read kiro-essentials/personas/devils-advocate.md and poke holes in my design
```
```
Read kiro-essentials/workflows/commit.md and commit my changes
```

### Option 3: Copy into Your Project

Copy relevant skills into your project for persistent context:

```bash
# Copy skills you use most into your project
mkdir -p docs/dev-guides
cp kiro-essentials/skills/writing-tests.md docs/dev-guides/
cp kiro-essentials/skills/systematic-debugging.md docs/dev-guides/
cp kiro-essentials/skills/handling-errors.md docs/dev-guides/
```

Then when working in that project, Kiro can reference them directly.

### Option 4: Run the Shell Scripts Directly

The log analysis scripts work standalone:

```bash
# Aggregate errors by frequency
bash /path/to/kiro-essentials/scripts/aggregate-errors.sh app.log "ERROR" 20

# Trace a request across log files
bash /path/to/kiro-essentials/scripts/trace-request.sh req-abc123 logs/

# Find slow requests
bash /path/to/kiro-essentials/scripts/slow-requests.sh app.log 1000 20
```

Or ask Kiro to run them for you:

```
Use the scripts in kiro-essentials/scripts to analyze the errors in /var/log/app.log
```

### Example Prompts by Category

**Testing:**
- "Write tests for this module following the testing trophy model"
- "Fix the flaky test in tests/integration/auth.test.ts"
- "Why is this test timing out? Use condition-based waiting patterns"

**Debugging:**
- "Debug why the API returns 500 on POST /users"
- "Analyze the logs in /var/log/app/ for the last hour"

**Code Quality:**
- "Refactor src/legacy/payment.ts"
- "Optimize the DataTable component"
- "Review error handling in src/api/"

**Planning:**
- "Plan the implementation of OAuth2 authentication"
- "Execute the plan in plans/2025-01-15-auth.md"

**Writing:**
- "Write a README for this project (use the Engineer persona)"
- "Write a strategy memo for migrating to microservices"
- "Review my commit messages and suggest improvements"

**Architecture:**
- "Help me design the module boundaries for this feature"
- "Play devil's advocate on my caching strategy"

## What's Different from claude-essentials

This is a content port, not a plugin port. Claude Code has a plugin system with slash commands, agent delegation, hooks, and auto-skill-loading. Kiro doesn't have those mechanics, so:

| claude-essentials | kiro-essentials |
|---|---|
| `/ce:test` slash command | `workflows/test.md` prompt template |
| `Skill()` tool auto-loading | Knowledge base search or direct file reference |
| `@ce:code-reviewer` agent | `personas/code-reviewer.md` behavioral prompt |
| Session hooks | Not applicable (no hook system) |
| Sub-agent delegation | Single-agent workflows |

The development methodologies, patterns, and best practices are identical. The left column shows Claude Code-specific features that don't exist in Kiro.

## Credits

All skill content, workflows, and personas are adapted from [claude-essentials](https://github.com/rileyhilliard/claude-essentials) by Riley Hilliard, licensed under MIT.

## License

MIT
