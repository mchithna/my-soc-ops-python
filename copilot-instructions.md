# Soc Ops - Workspace Instructions

## ✅ Development Checklist (Before Commits)

1. **Lint**: `ruff check .` — Fix style and import issues
2. **Build**: `uvicorn app.main:app --port 8000 --reload` — Verify app starts
3. **Test**: `pytest tests/ -v` — All 25 tests pass

---

## 🎮 Project Overview

**Soc Ops** is a FastAPI-based social bingo game for in-person mixers. Players mark squares on a 5x5 bingo board by answering questions about each other.

### Tech Stack
- **Backend**: FastAPI 0.115+, Uvicorn, Jinja2
- **Frontend**: HTML/CSS/JS with HTMX for interactivity
- **Testing**: pytest 8.0+, httpx for API testing
- **Code Quality**: ruff linting

### Project Structure
```
app/
  ├── main.py           # FastAPI app & route handlers
  ├── game_logic.py     # Core bingo logic (board generation, validation)
  ├── game_service.py   # Session management & game state
  ├── models.py         # Data classes
  ├── data.py           # Question pool
  └── templates/        # Jinja2 templates (base, home, game screens)
tests/
  ├── test_api.py       # API endpoint tests
  └── test_game_logic.py # Game logic unit tests
```

---

## 🔧 Development Workflow

### Running the App
```bash
# Development server (auto-reload on changes)
uvicorn app.main:app --port 8000 --reload

# Or use the configured VS Code task
# Ctrl+Shift+B → "Run FastAPI Server (Port 8000)"
```

### Testing
```bash
# Run all tests with verbose output
pytest tests/ -v

# Run specific test file
pytest tests/test_game_logic.py -v

# Run single test class
pytest tests/test_api.py::TestHomePage -v
```

### Linting & Formatting
```bash
# Check code style (E=errors, F=flakes, I=imports, N=naming, W=warnings)
ruff check .

# Auto-fix fixable issues
ruff check . --fix
```

---

## 📋 Key Guidelines

### API Design
- All game state is session-based (HTTP-only cookie)
- **GET /**: Home page with start button
- **POST /start**: Generate new board, return game screen
- **POST /toggle/{square_id}**: Mark/unmark square
- **POST /reset**: Clear board, return to start screen
- **POST /dismiss**: Close bingo modal

### Game Logic
- **Board**: 5×5 grid (25 squares), center is free space
- **Generation**: Shuffle 24 random questions + free space, assign IDs 1-25
- **Bingo Check**: Validate rows, columns, diagonals
- **Session Format**: Bingo state tracked in encrypted cookie

### Frontend Instructions
- Use **HTMX** for dynamic interactions (no page reloads)
- Component templates in `app/templates/components/`
- CSS utilities documented in `.github/instructions/css-utilities.instructions.md`
- No purple gradients (see `.github/instructions/frontend-design.instructions.md`)

### Testing Standards
- Unit tests for pure game logic (`test_game_logic.py`)
- Integration tests for API endpoints with test client (`test_api.py`)
- All tests should be deterministic and isolated
- Minimum: 25 passing tests

---

## 🚀 Common Tasks

### Add a New API Endpoint
1. Define route in `app/main.py`
2. Write test case in `tests/test_api.py`
3. Run `pytest tests/test_api.py -v` to verify
4. Lint with `ruff check .`

### Modify Game Logic
1. Update logic in `app/game_logic.py`
2. Write/update unit tests in `tests/test_game_logic.py`
3. Run `pytest tests/test_game_logic.py -v`
4. Test integration with `pytest tests/test_api.py -v`

### Update Questions
1. Edit `app/data.py` — questions list
2. Run tests to ensure board generation still works
3. Test in browser to verify randomization

---

## 📖 Context Engineering References

- **CSS Utilities**: `.github/instructions/css-utilities.instructions.md`
- **Frontend Design**: `.github/instructions/frontend-design.instructions.md`
- **Lab Guide**: [Copilot Dev Days Agent Lab](https://copilot-dev-days.github.io/agent-lab-python/)

---

## 🎨 Design System: Cyberpunk Neon

### Color Palette

The UI uses a dark cyberpunk aesthetic with electric neon accents:

| Color | Hex | Usage | Effect |
|-------|-----|-------|--------|
| **Cyan** | `#00d9ff` | Borders, focus states, default glows | Primary interactive glow |
| **Magenta** | `#ff0080` | Winners, emphasis, modals | High-contrast highlights |
| **Lime Green** | `#39ff14` | Marked squares, success states | Success/completion indicator |
| **Dark BG** | `#0a0e27` | Main background | Deep space aesthetic |
| **Text** | `#e0e0e0` | Primary text | High contrast on dark |

### Typography

- **Font Stack**: System font (sans-serif)
- **Letter Spacing**: `0.05em` for cyberpunk feel
- **Transform**: Uppercase on headings, buttons, and emphasis text
- **Glows**: Text-shadow applied to all interactive elements

### Component Styling

**Board Container**
- Cyan double border (`3px double`)
- Glow shadow: `0 0 20px #00d9ff`
- Dark navy background with subtle glow inset

**Marked Squares**
- Lime green background (`rgba(57, 255, 20, 0.4)`)
- Lime border with glow shadow
- Text glow effect for emphasis

**Winning Squares**
- Magenta background with pulse animation
- Continuous glow animation: `glow-pulse 1.5s infinite`
- Winner emoji highlighted with glow

**Free Space (Center)**
- Cyan highlight with glow
- Non-interactive, identifies center bingo square

**Modal**
- Magenta double border with multi-layer glow
- Glitch animation on entrance (`0.5s ease-out`)
- High-opacity dark overlay (`0.9`)

### Animations

**Glitch Effect** (Modal entrance)
- Random horizontal skew: `-3px` to `3px`
- Duration: `0.5s`
- Timing: `ease-out`

**Glow Pulse** (Winning squares)
- Text-shadow expansion
- Box-shadow brightness increase
- Duration: `1.5s` continuous

**Hover States**
- Cyan glow expansion on buttons
- Box-shadow intensifies
- Subtle background color shift

### CSS Utilities

For consistent styling, use these utility classes:

```css
.glow-cyan      /* Cyan text-shadow glow */
.glow-magenta   /* Magenta text-shadow glow */
.glow-lime      /* Lime green text-shadow glow */
```

### Responsive Design

- Mobile-first approach maintained
- Dark theme works across all viewport sizes
- Glow effects scale with container size
- Touch targets remain 60px minimum height

---

## ⚠️ Important Notes

- **Do not use Simple Browser** — Start the app and confirm it's running
- **Port 8000** — Always use for consistency with task configuration
- **Session Security** — Bingo state is encrypted with `itsdangerous` before storing in cookie
- **Python 3.13+** — Project requires Python 3.13 (or adjust `pyproject.toml`)
- **Cyberpunk Theme** — All neon colors and glows are CSS-only, no HTML changes needed
