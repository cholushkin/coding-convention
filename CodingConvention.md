### C# Naming Conventions

#### Member Accessibility Styles
- **Private/Protected Fields:** camelCase with a leading underscore `_` (e.g., `_currentHealth`, `_rigidbody`).
- **Properties & Public Members:** PascalCase (e.g., `CurrentHealth`, `IsGrounded`).
- **Local Variables & Parameters:** camelCase (e.g., `direction`, `targetVelocity`).
- **Constants & Statics:** SCREAMING_SNAKE_CASE for pure constants (`MAX_HEALTH`). PascalCase for static readonly configuration types.

#### Architectural Suffixes
- `Controller`: Controls execution, input, or state transitions for a single complex actor/system.
- `Processor`: Pure, side-effect-free data transformation pipelines.
- `Service`: Cross-cutting infrastructure or domain-agnostic helpers (e.g., `SaveService`, `LogService`).
- **Avoid `Manager` / `Util`:** Do not name classes `Manager` or `Utility`. Be specific. If a class handles data collection, call it a `Repository` or `Registry`.

#### Event Design
- **Declaration:** Use past-tense verbs or the `On` prefix. Do not prefix with the word `Event`.
- **Handlers:** Match subscription methods with the `On` prefix or context action.

```csharp
public event Action<HealthChangedEventArgs> OnHealthChanged;
private void OnHealthChanged(HealthChangedEventArgs args) { ... }
````

### Serialization & Properties
- **No Public Fields:** Never expose raw, mutable public fields (`public float Speed`). Use properties instead.
- **Inspector Exposure:** For fields that need Unity Designer configuration, use auto-properties with target serialization attributes, or keep them private backing fields.
- **File-Scoped Namespaces:** Always use file-scoped namespaces to reduce useless indentation levels.

```csharp
namespace MyGame.Gameplay.Player;

public class PlayerController : MonoBehaviour
{
    [field: SerializeField] public float MoveSpeed { get; private set; } = 5f;
    [SerializeField] private float _jumpForce = 10f;
}
```

### Code Style & Formatting
- **Indentation:** Controlled via the project `.editorconfig`. Let your IDE format on save.
- **Braces:** Allman style (each brace on a new line) for logic blocks. For single-line statements inside `if` or loops, omit the braces entirely and use a 2-line format.
- **Line Length:** Soft limit at 120 characters. Wrap long method arguments or complex LINQ operations.
- **Keep it Clean:**
    - Single space around operators.
    - No spaces inside parentheses `()` or brackets `[]`.
    - **Self-Documenting Code over Comments:** Write descriptive class, method, and variable names so the code explains itself. Avoid `/// <summary>` blocks on obvious code. Reserve XML comments strictly for shared core tools/libraries (`Libs/`) or exceptionally complex algorithms where intent isn't immediately clear from the signature.
- **Regions:** Use `#region` strictly to group distinct structural blocks (e.g., Properties, Events, Unity Lifecycle, Implementation) to keep long files highly navigably structured. Do not use them inside methods.

### Clean Code & Performance Principles
- **Early Returns & Guard Clauses:** Eliminate nesting depth immediately. Check for invalid states or null parameters at the absolute top of the method.
- **Defensive, Lean Logic:** Use `Debug.Assert` for critical invariant testing in development.
- **Allocation Awareness:** Avoid structural allocations (`LINQ`, `String boxing`, instantiation) within high-frequency loops like `Update()`, `FixedUpdate()`, or inside rendering logic. Use cached collections or native arrays where appropriate.
## Comprehensive Code Example

```csharp
namespace MyGame.Gameplay.Grid;

using System;
using System.Collections.Generic;
using UnityEngine;

[SelectionBase]
[DisallowMultipleComponent]
public sealed class GridController : MonoBehaviour
{
    // --- Serialization & Properties ---
    [field: SerializeField] public int Width { get; private set; } = 8;
    [field: SerializeField] public int Height { get; private set; } = 8;
    [field: SerializeField] public float CellSize { get; private set; } = 1f;

    // --- Event Design ---
    public event Action<TileStateChangedEventArgs> OnTileChanged;
    public event Action OnGridGenerationCompleted;

    // --- Private/Protected Fields ---
    [SerializeField] private GameObject _tilePrefab;
    [SerializeField] private Transform _gridGridRoot;

    private readonly Dictionary<Vector2Int, GameObject> _activeTiles = new();
    private bool _isInitialized;

    private const int MAX_GRID_DIMENSION = 64;
    #endregion

    #region --- Unity Lifecycle ---
    private void Awake()
    {
        InitializeGrid();
    }

    private void OnDestroy()
    {
        ClearGrid();
    }
    #endregion

    #region --- Public API ---
    public void GenerateLayout(int newWidth, int newHeight)
    {
        if (newWidth <= 0 || newWidth > MAX_GRID_DIMENSION) 
            return;
        if (newHeight <= 0 || newHeight > MAX_GRID_DIMENSION) 
            return;

        ClearGrid();

        Width = newWidth;
        Height = newHeight;

        InitializeGrid();
    }

    public bool TryGetTileAt(Vector2Int coordinates, out GameObject tile)
    {
        if (!IsValidCoordinate(coordinates))
        {
            tile = null;
            return false;
        }

        return _activeTiles.TryGetValue(coordinates, out tile);
    }
    #endregion

    #region --- Implementation ---    
    private void InitializeGrid()
    {
        Debug.Assert(_tilePrefab != null, "GridController is missing its Tile Prefab reference.");
        if (_isInitialized) 
            return;

        _activeTiles.EnsureCapacity(Width * Height);

        for (int x = 0; x < Width; x++)
        {
            for (int y = 0; y < Height; y++)
            {
                Vector2Int coordinates = new Vector2Int(x, y);
                SpawnTileAt(coordinates);
            }
        }

        _isInitialized = true;
        OnGridGenerationCompleted?.Invoke();
    }

    private void SpawnTileAt(Vector2Int coordinates)
    {
        Vector3 worldPosition = CalculateWorldPosition(coordinates);
        
        GameObject tileInstance = Instantiate(_tilePrefab, worldPosition, Quaternion.identity, _gridGridRoot);
        tileInstance.name = $"Tile_{coordinates.x}_{coordinates.y}";

        _activeTiles.Add(coordinates, tileInstance);

        OnTileChanged?.Invoke(new TileStateChangedEventArgs(coordinates, tileInstance));
    }

    private void ClearGrid()
    {
        if (_activeTiles.Count == 0) 
            return;

        foreach (KeyValuePair<Vector2Int, GameObject> pair in _activeTiles)
        {
            if (pair.Value) 
                Destroy(pair.Value);
        }

        _activeTiles.Clear();
        _isInitialized = false;
    }

    private Vector3 CalculateWorldPosition(Vector2Int coordinates)
    {
        return new Vector3(
            coordinates.x * CellSize, 
            0f, 
            coordinates.y * CellSize
        );
    }

    private bool IsValidCoordinate(Vector2Int coords)
    {
        return coords.x >= 0 && coords.x < Width && coords.y >= 0 && coords.y < Height;
    }
    #endregion
}

public readonly struct TileStateChangedEventArgs
{
    public readonly Vector2Int Coordinates;
    public readonly GameObject TileObject;

    public TileStateChangedEventArgs(Vector2Int coordinates, GameObject tileObject)
    {
        Coordinates = coordinates;
        TileObject = tileObject;
    }
}
```
