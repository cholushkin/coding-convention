# Semantic Versioning for Unity Engineering Workflows

Semantic versioning conventions for:

- Unity projects
- small engineering teams
- automated release pipelines
- AI-assisted workflows
- long-term maintainability

This specification extends standard Semantic Versioning with production-oriented release rules designed for Unity ecosystems.

---

# Goals

The system prioritizes:

- deterministic versioning
- automation compatibility
- semantic clarity
- predictable upgrades
- readable release history
- low operational overhead

---

# Version Format

```text
MAJOR.MINOR.PATCH
```

Examples:

```text
1.0.0
1.4.2
2.0.0
```

Pre-release versions:

```text
1.5.0-alpha.1
1.5.0-beta.2
1.5.0-rc.1
```

---

# Version Semantics

| Version | Meaning |
|---|---|
| `MAJOR` | Breaking or incompatible changes |
| `MINOR` | Backward-compatible features |
| `PATCH` | Backward-compatible fixes |

---

# Commit-to-Version Mapping

| Commit Pattern | Version Impact |
|---|---|
| `feat` | MINOR |
| `fix` | PATCH |
| `perf` | PATCH |
| `!` or `BREAKING CHANGE` | MAJOR |
| `docs` | none |
| `style` | none |
| `test` | none |
| `chore` | none |

Examples:

```text
feat(gameplay): add climbing system
→ MINOR
```

```text
fix(ui): prevent tooltip flickering
→ PATCH
```

```text
feat(save)!: replace serialization format
→ MAJOR
```

---

# Breaking Changes

Breaking changes must be explicit.

Use:

```text
!
```

or:

```text
BREAKING CHANGE:
```

Examples:

```text
feat(core)!: remove legacy inventory api
```

```text
BREAKING CHANGE: save files are incompatible with previous versions
```

---

# Unity-Specific Breaking Changes

Examples of breaking changes in Unity ecosystems:

- incompatible save formats
- prefab contract changes
- removed serialized fields
- Addressables migration
- rendering pipeline migration
- ECS architecture migration
- networking protocol changes
- public API removal
- namespace restructuring

---

# Pre-release Rules

| Tag | Meaning |
|---|---|
| `alpha` | unstable internal iteration |
| `beta` | feature complete, testing ongoing |
| `rc` | release candidate |

Examples:

```text
2.0.0-alpha.1
2.0.0-beta.3
2.0.0-rc.1
```

---

# Changelog Generation

Release notes should be generated automatically from semantic commits.

Recommended grouping:

| Commit Type | Changelog Section |
|---|---|
| `feat` | Features |
| `fix` | Fixes |
| `perf` | Performance |
| `refactor` | Internal |
| `build` | Build |
| `docs` | Documentation |

Recommended exclusions:

- `style`
- `test`
- temporary maintenance commits

---

# Compatibility Rules

Major versions may introduce:

- API incompatibility
- serialization incompatibility
- package dependency changes
- platform support changes

Minor and patch releases should remain backward compatible whenever possible.

---

# Release Workflow

```text
semantic commits
→ version calculation
→ changelog generation
→ tagged release
→ package distribution
```

The release process should remain deterministic and reproducible.

---

# Automation Rules

- versioning must be derivable from commit history
- releases should not require manual interpretation
- semantic meaning must remain machine-readable
- AI-generated commits must follow the same conventions
- release generation should remain reproducible

---

# Example

## Commit History

```text
feat(gameplay): add wall climbing
fix(ui): prevent inventory flickering
perf(rendering): reduce shadow allocations
```

## Generated Version

```text
1.4.0
```

## Generated Changelog

```text
## Features
- add wall climbing

## Fixes
- prevent inventory flickering

## Performance
- reduce shadow allocations
```

---

# Ecosystem Integration

Designed to work together with:

- semantic commit conventions
- automated changelog generation
- Unity package workflows
- CI/CD pipelines
- VersionHistory integration

---

# References

- https://semver.org/
- https://www.conventionalcommits.org/
- https://keepachangelog.com/
