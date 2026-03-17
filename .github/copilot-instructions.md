---
applyTo: "**"
---

# Dutch A2 Vocabulary – Copilot Instructions

## Project Overview

**Dutch A2 Vocabulary** is a Blazor WebAssembly (client-side, no server) flashcard app for studying Dutch vocabulary at the A2/inburgering lezen level. It runs entirely in the browser using .NET 8 WASM.

## Architecture

| Layer | File(s) | Purpose |
|---|---|---|
| Model | `Models/WordEntry.cs` | `record WordEntry(string Dutch, string English, string Category)` |
| Data | `Data/WordData.cs` | Static list of ~812 `WordEntry` objects, grouped by category |
| UI | `Pages/Home.razor` | Single-page flashcard UI with flip, navigation, shuffle, keyboard support |
| Layout | `Layout/MainLayout.razor` | Minimal shell — no nav sidebar |
| Styles | `wwwroot/css/app.css` | Custom `.fc-*` CSS classes for the flashcard component |

## Data Conventions (`WordData.cs`)

- All entries use `new("dutch", "english translation", "Category Name")`.
- 13 categories (in order): `Function Words`, `Common Verbs`, `Numbers & Time`, `People & Family`, `Body & Health`, `Food & Drink`, `Home & Furniture`, `Transport & Directions`, `Work & Education`, `Shopping & Money`, `Weather & Nature`, `Emotions & Adjectives`, `Society & Civic`.
- **No true duplicates** — if a word appears in two categories it must have a meaningfully different translation or context label (e.g. `zijn` = "his" vs "to be"). Avoid adding the same Dutch string with the same English meaning twice.
- Parenthetical disambiguation suffixes (e.g. `water (nutsvoorziening)`) are acceptable only when the bare word already exists with a different meaning.
- Target vocabulary: ~800 highest-frequency words that appear in A2 inburgering *lezen* (reading) exams. Prioritise practical civic, admin, health, and daily-life vocabulary over rare or literary words.

## UI / Interaction

- **Flip card**: click the card, `Enter`, `ArrowUp`, or `ArrowDown`.
- **Next card**: `→` arrow key or *Next* button.
- **Previous card**: `←` arrow key or *Prev* button.
- **Shuffle**: `Space` or *Shuffle* button. Resets to index 0.
- The card front shows the Dutch word and its category; the back shows the English translation with the Dutch word in smaller text.
- A progress bar at the bottom reflects position in the deck.
- The container receives focus automatically on load and after button clicks so keyboard shortcuts work immediately.

## Development

```powershell
# Run locally (hot reload)
dotnet watch run

# Build for production
dotnet publish -c Release
```

- Framework: **Blazor WebAssembly** — no server-side code, no `@inject` services needed for the flashcard logic.
- When adding new features, keep all state in `Home.razor` `@code` block unless the feature is complex enough to warrant a dedicated service.
- Do not introduce JavaScript interop unless strictly necessary — prefer Blazor/C# solutions.
- Do not add a navigation menu or extra pages unless explicitly requested.

## Adding / Editing Words

- Edit `Data/WordData.cs` only.
- Keep entries sorted within their category section.
- Do not change `WordEntry` record fields without updating every call site.
- After any bulk edit, verify there are no duplicate Dutch strings with the same meaning.
