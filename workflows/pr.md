# Workflow: PR

Create a pull request with auto-generated description.

## Usage

> "Create a PR"
> "Create a PR against develop"

## Process

1. **Check prerequisites:**
   ```bash
   git status                    # uncommitted changes?
   git remote -v                 # remote exists?
   git rev-parse --abbrev-ref --symbolic-full-name @{u} 2>/dev/null  # pushed?
   ```
   - If uncommitted changes: "Please commit first"
   - If not pushed: `git push -u origin $(git branch --show-current)`

2. **Determine base branch:**
   ```bash
   git rev-parse --verify origin/main 2>/dev/null && echo main || echo master
   ```

3. **Gather context:**
   ```bash
   MERGE_BASE=$(git merge-base HEAD origin/$BASE)
   git log $MERGE_BASE..HEAD --oneline
   git diff $MERGE_BASE..HEAD --stat
   git diff $MERGE_BASE..HEAD
   ```

4. **Generate PR content** (following [writer](../skills/writer.md), Contributor persona):

   **Title:** Conventional format, 50 chars max, imperative mood
   ```
   feat: add user authentication flow
   fix: resolve race condition in data sync
   ```

   **Body:**
   ```markdown
   ## Summary
   [2-3 sentences: what and why]

   ## Changes
   - [Key change 1]
   - [Key change 2]

   ## Testing
   - [ ] Tests added/updated

   ## Notes
   [Context for reviewers, or "None"]
   ```

5. **Create the PR:**
   ```bash
   gh pr create --title "<title>" --base <base> --body "<body>"
   ```

6. **Report:** Print the PR URL.
