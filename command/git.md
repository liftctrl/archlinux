# Git Command Notes

This document collects useful Git commands for daily work.

---

## 1. Undo Last Commit

There are two common ways to undo the last commit, depending on whether it has been pushed or not.

### 1.1 Local Only (Commit Not Pushed)

If the commit has not been pushed to a remote, you can reset the branch to the previous commit:

```bash
git reset --soft HEAD~1   # Undo commit, keep changes staged
git reset --mixed HEAD~1  # Undo commit, keep changes unstaged
git reset --hard HEAD~1   # Undo commit, discard changes
```

### 1.2 Remote (Commit Already Pushed)

If the commit has been pushed, you should not reset history (to avoid breaking others’ clones).
Instead, create a new commit that reverts the changes:

```bash
git revert <commit-hash>
```

This will open an editor to confirm the revert message, then create a new commit that undoes the changes.

---

## 2. Commit Message Structure

A good commit message usually has three parts:

**a) Header (Required)**

Format:

```bash
<type>(<scope>): <short summary>
```

- **type** – Describes the purpose of the commit. Common types include:

| Type     | When to use                                                         |
| -------- | ------------------------------------------------------------------- |
| feat     | Adding a new feature                                                |
| fix      | Bug fixes                                                           |
| docs     | Documentation changes                                               |
| style    | Formatting, white-space, missing semi-colons, etc. (no code change) |
| refactor | Code restructuring without changing behavior                        |
| perf     | Performance improvements                                            |
| test     | Adding or fixing tests                                              |
| chore    | Maintenance tasks (build scripts, dependencies, etc.)               |


- **scope** (optional) – The part of the code affected. Examples: `auth`, `ui`, `api`, `database`.
- **short summary** – One-line description (50–72 characters). Use **imperative mood**, like `Add` instead of `Added` or `Fix` instead of `Fixed`.

**b) Body (Optional, but recommended for complex changes)**

- Explain **why** the change was made and **what it does**.
- Wrap lines at ~72 characters.
- Example:

```bash
Add JWT token refresh endpoint

This allows the client to refresh their authentication token
without requiring a full login, improving user experience.
```

**c) Footer (Optional)**

- Usually for:
  - Issue references (`Closes #123`)
  - Breaking changes (`BREAKING CHANGE: ...`)

Example:

```bash
BREAKING CHANGE: the login API now requires a `client_id` parameter
Closes #456
```

**Practical Examples**

| File / Change                      | Commit Message                                                |
| ---------------------------------- | ------------------------------------------------------------- |
| Added new login API                | `feat(auth): add login API with JWT support`                  |
| Fixed button alignment on mobile   | `fix(ui): resolve overlapping buttons on mobile view`         |
| Updated README setup instructions  | `docs(readme): clarify installation steps for Windows`        |
| Refactored validation logic in API | `refactor(api): simplify user validation logic`               |
| Added unit tests for auth module   | `test(auth): add unit tests for login and register endpoints` |


**Tips for Writing Good Commit Messages**

1. **One commit per logical change** – Avoid bundling unrelated changes.
2. **Use imperative mood** – “Fix bug” not “Fixed bug”.
3. **Be concise but descriptive** – Don’t just write Update file.
4. **Mention issue numbers if applicable** – helps traceability.
5. **Separate commits for docs, style, and refactors** – avoids confusion in code history.

---
