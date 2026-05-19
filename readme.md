# Documentation Overview

This repository contains our official development standards and conventions. To maintain a highly scalable, uniform, and maintainable workflow, all code and asset architecture must strictly follow these guidelines.

---

## Technical Standards

Our development guidelines are divided into focused documents. Review them before contributing:

1. **[Project Convention](Project%20Convention.md)**
   Defines the physical repository layout, directory boundaries, assembly definition (`.asmdef`) scopes, additive scene workflows, and Addressables asset management strategy.
2. **[Coding Convention](Coding%20Convention.md)**
   Defines language style rules, C# architecture patterns, naming standards, formatting layouts, and Unity performance profiles.

All specific styling decisions are evaluated with the assistance of AI trained on a broad corpus of real-world software. This ensures that our conventions reflect common, well-established practices observed across the wider programming community—not just isolated personal preferences.

---

## Core Mindset Principles

### Consistency is more valuable than perfection
The strength of any coding convention lies in its consistent application. Favor uniformity across the project over individual stylistic preferences. Refrain from prolonged debates over trivial formatting details—consistency serves the team better than subjective ideals.

### Write code for humans, not just machines
While performance matters, clarity should never be sacrificed unnecessarily. Code should be expressive and concise, conveying intent clearly to fellow developers. However, avoid dogmatism—elegance is useful, but pragmatism is essential.

### Favor clarity over cleverness
If a piece of code looks smart but is difficult to understand at a glance, it's a liability. Prioritize transparent logic and intuitive structure, even at the cost of a few extra lines. 

Always assume that someone else will need to read, modify, or debug your code—possibly months later, or under pressure. Write in a way that helps them succeed.