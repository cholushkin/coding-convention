- Reference project: [unity-game-template](https://github.com/cholushkin/unity-game-template?utm_source=chatgpt.com)
- Clone Reference project and use as a starting point for new projects 

---
## Project Structure
- Keep runtime and editor code strictly separated via assembly definitions (asmdefs)
- Keep third-party code isolated from project code
- Prefer package-style organization (the entire game treated as a big local package)

### Root Structure

```text
ProjectRoot/
├── ArtSources/      # Raw source assets (Blender, Photoshop, etc.)
├── Builds/
│   ├── Windows/  
│   └── Android/
├── Documentation/
├── References/      # Game design documents, references, inspiration
├── Tools/           # External CLI tools, scripts, automation
└── Unity/
    └── Game/        # Unity project root (consistent naming)
````

### Unity Project Structure

```
Assets/
├── Game/            # Project-specific code and assets
│   ├── Runtime/
│   └── Editor/
└── Libs/            # Shared internal modules and external plugins
    ├── FrameworkA/
    └── SharedModule/
```

---
## Script & Assembly Organization
- **Feature-First Structure:** Group by feature/domain for gameplay; group by type only for global infrastructure.
- **Strict Layer Separation:** Keep gameplay code separated from framework/infrastructure and UI code.
- **No Dumping Grounds:** Avoid generic folders like `Managers`, `Helpers`, `Utils`, or `Misc`.
- **Shallow Hierarchy:** Prefer a flat, wide folder structure over excessive nesting.

### Assemblies & Boundaries
- `Game.Runtime.asmdef` (Must never reference `UnityEditor`)
- `Game.Editor.asmdef` (For editor-only tooling; may reference Runtime)
- `Game.Tests.asmdef`

### Runtime Structure

```
Runtime/
├── Core/            # Shared framework, bootstrapper, and infrastructure
├── Gameplay/        # Isolated feature folders (e.g., Grid, Pieces, Mechanics)
├── UI/              # UI screens, views, and UI-specific logic
├── Audio/           # Sound managers, mixers, and audio configurations
└── Debug/           # Runtime developer tools, cheats, and debug views
```

---
## Asset & Scene Management

### Asset Loading & Addressables
- **No Resources Folder:** Do not use `Resources/` for general asset loading. Use it exclusively for the minimal bootstrap configuration.
- **Addressables:** Prefer Addressables for all runtime-loaded content.
- **Grouping:** Addressable groups must mirror the `Gameplay/` feature folder structure to ensure clean asset bundling and memory unloading.

### Scenes
- **Additive Loading:** Keep scenes focused and small. Use additive scene loading for large systems.
- **Single Entry Point:** Execution must always start from the `Bootstrap` scene. Direct loading of gameplay scenes is forbidden outside of `DevScenes/`.

```
Scenes/
├── Bootstrap/       # Initial setup, DI container initialization, global systems
├── Gameplay/        # Core gameplay loops and levels
├── UI/              # Persistent UI overlays (HUD, Loading Screens)
└── DevScenes/       # Isolated test/debug scenes (excluded from production builds)
```

### Prefabs & Assets
- **Nesting & Variants:** Keep prefab nesting shallow. Use variants only for controlled, meaningful differences—avoid deep variant inheritance chains.
- **Isolation:** Keep authored assets and generated/procedural content separated.
- **Debug Cleanup:** Keep debug/testing assets isolated within the `Debug/` or `DevScenes/` context.