## File and Folder Structure

- Repository root level Prj:
	- `Prg/ArtSources` : Art assets source 
	- `Prg/ScriptUtils` : Script utilities submodule
	- `Prj/Unity/UnityProjectName` : Unity project root level location
	- `Prj/Builds` : Builds for different platforms
- **Unity project root level:**
    - `Assets/`: Standard Unity assets.
    - `ProjectSettings/`: Unity project settings.
    - `Packages/`: Package Manager assets.
    - `UserSettings/`: Local user settings.
- **Within `Assets/`:**
    - `Scripts/`: Your primary C# scripts. Organize further by feature or system (e.g., `Scripts/Player`, `Scripts/AI`, `Scripts/UI`).
    - `Scenes/`: Your game scenes.
    - `Prefabs/`: Reusable game objects.
    - `Materials/`: Material assets.
    - `Textures/`: Texture assets.
    - `Audio/`: Audio clips and mixers.
    - `Animations/`: Animation controllers and clips.
    - `Editor/`: Custom editor scripts. Place these in a folder named `Editor` to prevent them from being included in builds.
    - `Plugins/`: Third-party plugins.
    - `Data/`: Data assets like JSON, XML, or ScriptableObjects.


## C# Script Structure and Naming

- **File And Folder Names:** PascalCase (e.g., `PlayerController.cs`, `UIManager.cs`). Match the primary class name.
- **Class Names:** PascalCase (e.g., `PlayerController`, `UIManager`). Use descriptive names that clearly indicate the class's purpose.    
- **Namespaces (Optional but Recommended for Larger Projects):** Use PascalCase and reflect the project or feature (e.g., `MyGame.Gameplay`, `MyGame.UI`). Place namespaces at the top of your script.

*Prj/Unity/GameName/Assets/Scripts/Game/Player/Player.cs* :

```
namespace MyGame.Player
{
	public class PlayerController : MonoBehaviour
	{
		// ... your code ...
	}
}
```

- **Class Members**
	- **Public Fields:** PascalCase (e.g., `MoveSpeed`, `Health`). Make them easily inspectable in the Inspector. Consider using `[SerializeField]` for private fields you want to expose in the Inspector.
	- **Private Fields:** camelCase with a leading underscore `_` (e.g., `_currentHealth`, `_rigidbody`). This clearly distinguishes them from public fields and properties.    
	- **Properties:** PascalCase (e.g., `CurrentHealth`, `IsGrounded`). Use properties to control access to fields and potentially add logic.
	- Methods: PascalCase (e.g., `Move`, `Jump`, `Initialize`). Use descriptive verbs.
	- **Constants:** SCREAMING_SNAKE_CASE (e.g., `MAX_HEALTH`, `DEFAULT_SPEED`). Use `const` or `static readonly` appropriately.
- **Enums:** PascalCase (e.g., `GameState`, `EnemyType`).
- **Interfaces:** PascalCase with a leading `I` (e.g., `IInteractable`, `IDamageable`).
- **Generic Type Parameters:** Single uppercase letters (e.g., `T`, `U`).
- **Local Variables:** camelCase (e.g., `direction`, `velocity`). Keep them concise and meaningful within their scope.

*Prj/Unity/GameName/Assets/Scripts/Game/Player/PlayerController.cs* :

``` 
public class PlayerController : MonoBehaviour
{
	public float MoveSpeed = 5f;
	[SerializeField] private float _jumpForce = 10f;
	private Rigidbody _rigidbody;
	public float CurrentHealth { get; private set; } = 100f;
	public bool IsGrounded { get; private set; }

	// ...
}
```

- Class names:
  - `Manager`: Used for classes that manage multiple similar entities.
  - `Controller`: Used for classes that control parts of a single complex entity.
  - `Processor`: Used for classes that continuously process data and provide results.
  - `Service`: Provides utility functions, external system access, or cross-cutting concerns (e.g., logging, saving, analytics)
- Events naming: 
  - Event name starts from `Event`: `EventRetrieveSimpleGUIInstance`
  - Handler of the event has name `Handle`:         
  ```private void Handle(EventRetrieveSimpleGUIInstance eventRetrieveSimpleGUIInstance, PublishContext context)```

## Code Style and Formatting

- **Indentation:** Use 4 spaces for indentation. Avoid tabs. Configure your IDE accordingly.   
- **Braces:** Use Allman style (each brace on a new line).
- **Line Length:** Aim for a maximum of 120 characters per line for readability.
- **Spacing:**
    - Add a blank line between methods.
    - Add a blank line between logical blocks of code within a method.
    - Use a single space around operators (`=`, `+`, `-`, `*`, `/`, `==`, `!=`, etc.).
    - Use a single space after commas in parameter lists and array/collection initializers.
    - No space between a method name and the opening parenthesis `(`.
    - No space inside parentheses.
    - No space inside square brackets for array/indexer access.
- **Comments:**
	- Use `//` for single-line comments to explain logic or clarify complex sections.
    - Use `///` for XML documentation comments for classes, methods, properties, and fields to generate API documentation.
    - **Regions (Use Sparingly):** While Unity often generates `#region` directives, use them judiciously for logically grouping larger sections of code (e.g., Inspector variables, Unity lifecycle methods). Overuse can clutter the code.

*Prj/Unity/GameName/Assets/Scripts/Game/Player/PlayerController.cs* :

```
/// Handles the movement of the player character.
public class PlayerController : MonoBehaviour
{
	public float MoveSpeed = 5f; // The speed at which the player moves.
	
	/// Moves the player in the specified direction.
	public void Move(Vector3 direction)
	{
		if (direction != Vector3.zero)
		{
			// Calculate the movement vector based on speed and direction.
			Vector3 movement = direction * MoveSpeed * Time.deltaTime;
			// ... apply movement to the Rigidbody ...
		}
	}
}
```

## General Best Practices

- **Early Returns:** Reduce nesting and improve readability by using early returns for error handling or simple checks.    
- **Defensive Programming:** Anticipate potential issues (e.g., null references, out-of-bounds errors) and add checks to prevent them. Use asserts. 
- Carefully consider the selection of external packages and libraries.