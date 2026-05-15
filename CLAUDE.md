# Reaction Time

Single-file web app (`index.html`) — no build step, no dependencies beyond Google Fonts.

## Project context

A reaction-time game built by students **Anna Bergese, Verena Mantero, Simone Operto** (class 2C LSSA, IIS Vallauri, Fossano). Deployed as a static page.

## Structure

Everything lives in `index.html`:
- **CSS** (`:root` vars, all components) — lines ~10–530
- **HTML** (layout, arena, sidebar) — lines ~530–640
- **JS** (all logic, no frameworks) — lines ~640–end

## UI layout

Two-column grid (`.layout`):
- **Left — `.arena`**: headline, animated button system (`.btn-system` with orbiting rings), result display, gauge bar, "meanwhile" fun-facts cards
- **Right — `.sidebar`**: language/mode toggles, stats grid, scrollable history, clear button

Fixed overlays: starfield canvas, nebula, confetti canvas, flash overlay, toasts, info button.

## Key JS globals

| Variable | Purpose |
|---|---|
| `lang` | `'it'` or `'en'`, persisted in localStorage |
| `flashMode` | `'flash'` or `'audio'`, persisted in localStorage |
| `scores` | Array of `{ ms, name, mode }`, persisted in localStorage key `rtScores` |
| `state` | Game FSM: `'idle' → 'wait' → 'go'` (or `'early'`) |

## Game FSM

`toIdle()` → `toWait()` → `toGo()` → `recordHit()` → back to idle  
Early press during `wait` → `toEarly()` → back to idle after 1.3 s

## i18n

All user-facing strings are in the `STRINGS` object (`{ it: {…}, en: {…} }`). Helper `s(key)` reads from current `lang`. `applyLang()` pushes all strings to the DOM and re-renders history/stats.

## Colors (CSS vars)

`--bg` `--border` `--text` `--muted` `--accent` (indigo) `--cyan` `--green` `--red` `--amber` `--purple`

## Info button

Fixed bottom-left `.info-wrap` with hover+click tooltip crediting the student authors. Tooltip has CSS hover (desktop) + JS click toggle (mobile).
