# Workflow: Fix Issue

Fix a GitHub issue by number.

## Usage

> "Fix issue #123"
> "Fix GitHub issue 456"

## Process

1. **Fetch the issue:**
   ```bash
   gh issue view <number> --json title,body,labels,comments
   ```

2. **Analyze the issue:**
   - Understand what's requested or what bug is reported
   - Check labels for context
   - Review comments for additional context
   - Identify acceptance criteria

3. **Explore the codebase:**
   - Find relevant files mentioned in the issue
   - Understand current implementation
   - Identify where changes need to be made

4. **Plan the fix:**
   - Break down into steps
   - Consider edge cases
   - Think about testing requirements

5. **Implement the fix:**
   - Make necessary code changes
   - Follow existing patterns and style
   - Keep changes focused on the issue scope

6. **Verify:**
   - Run relevant tests
   - Check acceptance criteria are met
   - Ensure no regressions

7. **Summarize:**
   - List files changed
   - Explain approach taken
   - Note any follow-up items

Do not automatically commit or create a PR. Let the user review first.
