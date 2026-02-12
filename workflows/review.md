# Workflow: Review

Comprehensive code review.

## Usage

> "Review my code changes"
> "Review the current branch against main"

## Process

Follow the [code-reviewer](../personas/code-reviewer.md) persona:

1. Check git status for uncommitted changes
2. Check current branch name
3. Determine what to review:
   - Uncommitted changes → review those
   - On feature branch → review all changes against main
   - Otherwise → ask what to review
4. Get the diff: `git diff --name-only main...HEAD`
5. Perform comprehensive review covering:
   - Correctness, security, performance
   - Maintainability, conventions, testing
   - Product/UX impact, developer experience
   - Documentation updates needed
6. Output structured review with severity levels
