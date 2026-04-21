# SocOps Agent Instructions

## 🚀 Quick Start Checklist

Before starting development, complete these steps:

- [ ] **Initialize**: `dotnet restore` (dependencies)
- [ ] **Build**: `dotnet build SocOps/SocOps.csproj`
- [ ] **Test**: `dotnet run --project SocOps/SocOps.csproj` and verify http://localhost:5166 loads
- [ ] **Verify**: Play the game, click a square, check Bingo detection works

---

## Project Overview

**SocOps** is a Social Bingo game for in-person mixers. Players find people matching questions and get 5 in a row to win. Built with **.NET 10 + Blazor WebAssembly** (C#, runs in browser).

**Live Demo**: https://dotnet-presentations.github.io/vscode-github-copilot-agent-lab/

---

## Architecture

### Game Flow
- **Start** → Player sees StartScreen
- **Playing** → Player marks squares on BingoBoard
- **Bingo** → 5 in a row detected, modal shows victory

### Core Services
- **BingoGameService** — Game state, board generation, event lifecycle
- **BingoLogicService** — Win detection (horizontal, vertical, diagonal), square marking

### Component Tree
```
Home.razor → StartScreen | GameScreen → BingoBoard → BingoSquare (5x5)
                                      → BingoModal (overlay)
```

---

## Key Files

| File | Purpose |
|------|---------|
| `SocOps/Pages/Home.razor` | Main game page, state logic |
| `SocOps/Services/BingoGameService.cs` | Game state management |
| `SocOps/Services/BingoLogicService.cs` | Win detection |
| `SocOps/Data/Questions.cs` | Bingo card questions |
| `SocOps/Components/*.razor` | UI components |
| `SocOps/Models/GameState.cs` | State enum (Start, Playing, Bingo) |

---

## Common Development Tasks

**Add questions:**
1. Edit `SocOps/Data/Questions.cs`
2. Add strings to questions list
3. Rebuild and test

**Create component:**
1. Create `SocOps/Components/MyComponent.razor`
2. Add `@code` block with logic
3. Add scoped CSS in `MyComponent.razor.css`
4. Import in parent: `<MyComponent />`

**Modify game state:**
1. Update `SocOps/Models/GameState.cs`
2. Update `BingoGameService.cs` handlers
3. Update `Home.razor` conditional logic

**Style elements:**
- Use Bootstrap classes from `wwwroot/lib/bootstrap/`
- Create scoped `.razor.css` files
- Reference `wwwroot/css/app.css` variables

---

## Copilot Agents

Use slash commands to activate specialized workflows:

- `/pixel-jam` — UI design with visual iteration
- `/quiz-master` — Quiz/question logic
- `/tdd` — Test-driven development
- `/ui-review` — UI/UX critique
- `/frontend-design` — Creative component design

Reference `.github/instructions/` for CSS and design guidance.

---

## Code Patterns

**Inject service:**
```csharp
@inject BingoGameService GameService
@GameService.StartGame()
```

**Blazor event:**
```csharp
<button @onclick="@(() => GameService.MarkSquare(id))">Mark</button>
```

**Component parameter:**
```csharp
[Parameter]
public string Title { get; set; }

[Parameter]
public EventCallback<int> OnClick { get; set; }
```

---

## Useful Links

- [Blazor Docs](https://learn.microsoft.com/en-us/aspnet/core/blazor/)
- [.NET 10](https://learn.microsoft.com/en-us/dotnet/core/whats-new/dotnet-10)
- [Repo](https://github.com/SaintResh/my-soc-ops-csharp)

Happy coding! 🎮
