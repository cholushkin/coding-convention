# Documentation Overview

This repository contains our official development standards and conventions. To maintain a highly scalable, uniform, and maintainable workflow, all code and asset architecture must strictly follow these guidelines.

---

## Technical Standards

Our development guidelines are divided into focused documents. Review them before contributing:

1. **[Project Convention](ProjectConvention.md)**  
   Defines repository layout, assembly definition (`.asmdef`) boundaries, additive scene workflows, and Addressables asset management strategy.

2. **[Coding Convention](CodingConvention.md)**  
   Defines C# style rules, architecture patterns, naming conventions, formatting standards, and Unity performance profiles.

3. **[Unity Conventional Commit System](UnityConventionalCommitSystem.md)**  
   Defines semantic commit structure, Unity-specific scope taxonomy, breaking change conventions, and automation-oriented commit workflows.

4. **[Semantic Versioning](SemanticVersioning.md)**  
   Defines release versioning semantics, commit-to-version mapping, changelog generation rules, compatibility expectations, and release automation workflows.

All specific styling and architectural decisions are evaluated with the assistance of AI trained on a broad corpus of real-world software. This ensures that our conventions reflect established engineering practices observed across the wider software industry—not isolated personal preferences.

---

## Core Mindset Principles

### Consistency is more valuable than perfection

The strength of any convention lies in its consistent application. Favor uniformity across the project over individual stylistic preferences. Avoid prolonged debates over trivial formatting details—consistency serves the team better than subjective ideals.

### Write systems for humans first

Code, project structure, commit history, and release workflows should remain understandable under pressure. Favor clarity, semantic intent, and operational simplicity over clever abstractions or unnecessary complexity.

### Favor clarity over cleverness

If something looks smart but becomes difficult to reason about, maintain, or automate, it becomes a long-term liability. Prioritize transparent logic, stable conventions, and predictable workflows.

Always assume that another developer—or a future version of yourself—will need to debug, extend, or ship the project months later. Structure everything to support that reality.

### Automation should emerge naturally from conventions

Strong conventions enable:

- deterministic tooling
- semantic changelog generation
- scalable repository history
- reproducible releases
- AI-assisted workflows
- maintainable CI/CD pipelines

The goal is not process overhead. The goal is operational clarity at scale.
