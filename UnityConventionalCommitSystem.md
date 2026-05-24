# Modern Conventional Commit System for Unity Projects

Production-ready commit conventions for:

- Unity game development
- small engineering teams
- AI-assisted development workflows
- automated changelog generation
- semantic versioning
- CI/CD pipelines
- long-term repository maintainability

---

# Goals

This convention optimizes for:

- human readability
- machine readability
- semantic changelog generation
- AI-assisted workflows
- scalable repository history
- predictable release management
- low cognitive overhead

The system prioritizes:

- semantic clarity
- stable taxonomy
- automation compatibility
- production-ready workflows

---

# Commit Message Format

```text
<type>(optional-scope): short description

optional body

optional footer(s)
```

Breaking changes:

```text
<type>(scope)!: breaking change description
```

Example:

```text
feat(gameplay): add wall running
```

Breaking change example:

```text
feat(save)!: replace legacy save format
```

---

# Commit Types

| Type | Description |
|---|---|
| `feat` | Adds or removes functionality |
| `fix` | Fixes bugs or incorrect behavior |
| `refactor` | Restructures code without changing behavior |
| `perf` | Performance or memory optimizations |
| `build` | Build system, dependencies, CI/CD |
| `ops` | Infrastructure and deployment changes |
| `chore` | Maintenance and non-functional tasks |
| `docs` | Documentation only |
| `test` | Adds or improves tests |
| `style` | Formatting or stylistic changes only |
| `revert` | Reverts a previous commit |

---

# Unity Scope Taxonomy

Scopes improve:

- repository navigation
- changelog grouping
- semantic history
- AI understanding
- team communication

Recommended scopes:

| Scope | Description |
|---|---|
| `gameplay` | Gameplay systems and mechanics |
| `ui` | User interface and UX |
| `audio` | Music and sound systems |
| `art` | Assets, animations, materials |
| `physics` | Physics systems |
| `rendering` | Rendering, shaders, pipelines |
| `input` | Input systems and controls |
| `ai` | NPC logic and gameplay AI |
| `save` | Persistence and serialization |
| `netcode` | Multiplayer and networking |
| `editor` | Unity editor tooling |
| `tools` | Internal developer tools |
| `build` | Build pipeline |
| `ci` | Continuous integration |
| `platform` | Platform-specific logic |
| `addressables` | Unity Addressables |
| `ecs` | DOTS/ECS systems |
| `urp` | Universal Render Pipeline |
| `hdrp` | High Definition Render Pipeline |
| `localization` | Localization systems |
| `analytics` | Telemetry and analytics |
| `security` | Security-related changes |

---

# Commit Description Rules

Descriptions should:

- use imperative present tense
- describe intent, not implementation
- remain concise and readable
- avoid punctuation at the end
- avoid capitalization at the beginning

Good:

```text
fix(save): prevent corrupted inventory serialization
```

Bad:

```text
fix: Changed null check.
```

---

# Breaking Changes

Use `!` immediately after type or scope.

Examples:

```text
feat(core)!: remove legacy inventory api
```

```text
refactor(save)!: migrate serialization format
```

Optional footer:

```text
BREAKING CHANGE: save files from v1 are incompatible
```

---

# AI & Automation Rules

- commit messages must be deterministic and machine-readable
- AI-generated commits must follow the same rules as human commits
- avoid vague descriptions
- one commit should represent one logical change
- squash temporary AI-generated commits before merge
- prefer semantic clarity over technical noise
- use domain language instead of implementation details

---

# Commit Quality Rules

A production-quality commit should:

- compile successfully
- keep the project runnable
- represent one logical change
- avoid unrelated modifications
- remain understandable without opening the diff
- be reversible when possible

Prefer:

- small focused commits
- semantic history
- isolated refactors
- stable intermediate states

Avoid:

- mixed feature and refactor commits
- temporary debug commits
- vague wording
- large unrelated changes

---

# Footer Conventions

Examples:

```text
Closes: GH-142
Refs: GH-201
Reviewed-by: Jane Doe
Co-authored-by: AI Agent
BREAKING CHANGE: save files are incompatible with previous versions
```

---

# Examples

## Feature

```text
feat(gameplay): add wall running system
```

## Fix

```text
fix(ui): prevent tooltip flickering
```

## Refactor

```text
refactor(ai): split behavior tree evaluation stages
```

## Performance

```text
perf(rendering): reduce dynamic shadow allocations
```

## Build

```text
build(ci): cache package dependencies
```

## Breaking Change

```text
feat(save)!: replace binary save pipeline

BREAKING CHANGE: old save files are incompatible
```

## Documentation

```text
docs(readme): add local multiplayer setup guide
```

---

# Recommended Workflow

1. Create small focused commits
2. Keep commit messages semantic and deterministic
3. Use scopes consistently across the repository
4. Mark breaking changes explicitly
5. Generate changelogs automatically from commit history
6. Tag releases using Semantic Versioning

---

ver.2.0

#unity #conventional-commit #semver #release-management #gamedev #automation #ai-native-development
