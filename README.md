# Ship

A Claude Code skill that automatically generates conventional commit messages and handles the full git workflow from staging to push.

## Installation

### Recommended (clone directly into Claude Code skills directory)

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/missuo/ship.git ~/.claude/skills/ship
```

### Manual install/update (only the skill file)

If you already have this repo cloned, copy the skill file into Claude Code's skills directory:

```bash
mkdir -p ~/.claude/skills/ship
cp SKILL.md ~/.claude/skills/ship/
```

## Usage

In Claude Code, invoke the skill:

```
/ship
```

Or ask Claude directly:

```
Please commit and push my changes
```

## Overview

This skill analyzes your git changes to automatically determine the appropriate commit type (feat, fix, docs, style, refactor, perf, test, build, ci, chore) following the [Conventional Commits](https://www.conventionalcommits.org/) specification.

### Key Features

- **Automatic type inference** - Detects commit type from file changes
- **Smart scope detection** - Extracts scope from file paths
- **Descriptive messages** - Generates clear, concise commit summaries
- **Full workflow** - Stages, commits, and pushes in one command
- **Safety checks** - Warns about sensitive files and large changes

## Commit Type Detection

The skill automatically determines commit types based on file patterns:

| Type         | Detected From                             | Examples                          |
| ------------ | ----------------------------------------- | --------------------------------- |
| **feat**     | New functionality, new files with exports | New API endpoints, new components |
| **fix**      | Corrections to logic, error handling      | Bug fixes, crash fixes            |
| **docs**     | Documentation files                       | README, markdown, comments        |
| **style**    | Formatting, no logic changes              | Indentation, semicolons           |
| **refactor** | Code restructuring                        | Renaming, moving code             |
| **perf**     | Optimization changes                      | Caching, algorithm improvements   |
| **test**     | Test files                                | _.test.ts, _.spec.ts              |
| **build**    | Build system files                        | package.json, dependencies        |
| **ci**       | CI/CD configuration                       | GitHub Actions, workflows         |
| **chore**    | Maintenance tasks                         | .gitignore, config files          |

## Commit Message Format

Generated messages follow this structure:

```
<type>(<scope>): <short summary>

<body>

<footer>
```

### Examples

**Simple feature:**

```
feat(api): add user login endpoint
```

**Bug fix with body:**

```
fix(ui): correct button alignment on mobile

The previous implementation used incorrect flexbox properties,
causing buttons to overflow on screens smaller than 375px.
```

**Breaking change:**

```
refactor(db): change user table schema

BREAKING CHANGE: removed username column in favor of email
```

## Scope Detection

Common scopes are auto-detected from file paths:

| Path Pattern       | Scope  |
| ------------------ | ------ |
| `src/api/*`        | `api`  |
| `src/components/*` | `ui`   |
| `src/auth/*`       | `auth` |
| `tests/*`          | `test` |
| `docs/*`           | `docs` |
| `src/db/*`         | `db`   |

## Safety Features

The skill includes safety checks to prevent:

- **Sensitive file commits** - Warns about .env, credentials, private keys
- **Oversized commits** - Suggests splitting very large changes
- **Mixed commits** - Detects when features and fixes are combined
- **Uncertain changes** - Asks for clarification when type is unclear

## Full Examples

### Example 1: New Feature

**Your changes:**

```
src/auth/login.ts (new file)
src/auth/logout.ts (new file)
```

**Command:**

```
/ship
```

**Result:**

```bash
git add src/auth/login.ts src/auth/logout.ts
git commit -m "feat(auth): add login and logout endpoints"
git push
```

### Example 2: Bug Fix

**Your changes:**

```
src/utils/formatter.ts (modified)
```

**Command:**

```
Please commit my fix
```

**Result:**

```bash
git add src/utils/formatter.ts
git commit -m "fix(utils): handle null values in formatter"
git push
```

### Example 3: Documentation Update

**Your changes:**

```
README.md (modified)
```

**Command:**

```
/ship
```

**Result:**

```bash
git add README.md
git commit -m "docs(readme): update installation instructions"
git push
```

### Example 4: Breaking Change

**Your changes:**

```
src/api/users.ts (modified - API changed)
```

**Command:**

```
Commit my changes with breaking change note
```

**Result:**

```bash
git add src/api/users.ts
git commit -m "refactor(api): change user response schema

BREAKING CHANGE: user_id field renamed to id"
git push
```

## Tips

- Commit **small**, logical units of change for best results
- The skill works best when changes are focused on a single purpose
- For complex multi-purpose changes, consider committing separately
- Always review the generated message before confirming

## Version History

- **1.0.0** - Initial release with automatic commit type detection

## License

MIT
