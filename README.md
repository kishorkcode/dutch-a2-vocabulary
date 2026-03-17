# Dutch A2 Vocabulary Flashcards

A browser-based flashcard app for studying Dutch vocabulary at the A2 / *inburgering lezen* (civic integration reading) level. Built with **Blazor WebAssembly** — no server required, runs entirely in the browser.

**Live App:** https://kishorkcode.github.io/dutch-a2-vocabulary/

## Features

- ~800 high-frequency Dutch words across 13 categories
- Flip cards to reveal English translations
- Filter by category using pill buttons
- Shuffle the deck at any time
- Keyboard-first navigation
- Progress bar showing position in the deck

### Keyboard Shortcuts

| Key | Action |
|-----|--------|
| `→` | Next card |
| `←` | Previous card |
| `Enter` / `↑` / `↓` | Flip card |
| `Space` | Shuffle deck |

## Categories

Function Words · Common Verbs · Numbers & Time · People & Family · Body & Health · Food & Drink · Home & Furniture · Transport & Directions · Work & Education · Shopping & Money · Weather & Nature · Emotions & Adjectives · Society & Civic

## Getting Started

**Prerequisites:** [.NET 8 SDK](https://dotnet.microsoft.com/download/dotnet/8.0)

```powershell
# Clone the repo
git clone https://github.com/kishorkcode/dutch-a2-vocabulary.git
cd dutch-a2-vocabulary

# Run with hot reload
dotnet watch run --project DutchA2Vocabulary

# Build for production
dotnet publish -c Release
```

Then open `http://localhost:5000` in your browser.

## Project Structure

```
DutchA2Vocabulary/
├── Data/WordData.cs          # ~800 vocabulary entries grouped by category
├── Models/WordEntry.cs       # WordEntry record (Dutch, English, Category)
├── Pages/Home.razor          # Flashcard UI — all interaction logic lives here
├── Layout/MainLayout.razor   # Minimal shell layout
└── wwwroot/css/app.css       # Flashcard styles (.fc-* classes)
```

## Adding / Editing Words

Edit `Data/WordData.cs` only. Keep entries sorted within their category section and avoid duplicate Dutch strings with the same English meaning.

## License

[MIT](LICENSE)
