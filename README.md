# Claude Code Accessibility Themes

Custom Claude Code themes built for people with color vision deficiency (CVD) and anyone who finds the built-in `dark-daltonized` and `light-daltonized` presets insufficiently contrasted. Every theme in this repo prioritizes aggressive luminance contrast (WCAG AA minimum, AAA where practical), CVD-safe hue selection that doesn't rely on red-vs-green discrimination, and semantic color separation so each UI role gets a dedicated hue rather than overlapping with branding or status colors.

## Background

Claude Code v2.1.118+ supports custom themes via JSON files in `~/.claude/themes/`. The built-in daltonized variants are a reasonable starting point, but they lean conservative: low-contrast selection highlights, muted diff backgrounds, and palette choices that still drift toward red/green for status colors. The themes here push further, and the trade-offs in each one are documented in its own README so you can decide whether the choices match your specific CVD type and contrast needs.

## Installation

Drop any theme JSON into `~/.claude/themes/`, then in a running Claude Code session run `/theme` and pick it from the list. Claude Code watches the directory and hot-reloads — edits to the JSON apply live to the active session without restarting.

### Dev containers and sandboxes

If you run Claude Code inside a devcontainer or Docker sandbox, either bind-mount the host themes directory:

```jsonc
// devcontainer.json
"mounts": [
  "source=${localEnv:HOME}/.claude/themes,target=/root/.claude/themes,type=bind,readonly"
]
```

Or COPY the JSON into your image and pre-select the active theme via `~/.claude/settings.json`:

```dockerfile
COPY themes/monokai-cvd-aggressive.json /root/.claude/themes/
RUN echo '{"theme":"custom:Monokai CVD Aggressive"}' > /root/.claude/settings.json
```

The pre-selection step matters for ephemeral containers where you don't want to `/theme` every session.

## Available themes

| Theme | Base | Description |
|---|---|---|
| [Monokai CVD Aggressive](themes/monokai-cvd-aggressive.md) | `dark` | Monokai-derived. Okabe-Ito blue/orange diff colors, bright yellow as the exclusive selection cue, brightened metadata text. |

Each theme has its own README in `themes/` explaining the specific color rationale and what was changed from its source palette.

## Design principles

Three principles apply across every theme in this repo.

**Yellow is reserved exclusively as the selection and focus cue.** Whatever color a theme uses for `suggestion`, `permission`, and `remember`, no other role is permitted to overlap. When something pops in the selection color, the eye should immediately know it means "this is what's active right now" — not status, not branding, not warning. Yellow is the chosen color because it has the highest luminance of any saturated hue and is unambiguously distinguishable across all common CVD types.

**Diffs use Okabe-Ito blue and orange instead of green and red.** Diff review is the single highest-friction UI element for users with deuteranopia or protanopia, because it's where the eye does the most fine-grained color comparison. Replacing the conventional green/red with blue (added) and orange (removed) — the canonical CVD-safe pairing from Okabe and Ito's 2008 Color Universal Design palette — eliminates the discrimination problem on hue alone, reinforced by luminance.

**Errors use magenta rather than red.** Pure red is the worst hue for CVD safety because it loses its primary channel for deutan and protan vision. Magenta (around `#EC4899` to `#F92672`) retains its blue component even when red sensitivity is absent, so it still reads as a high-alarm signal across CVD types. This is also why Monokai's original pink/magenta is preserved in the Monokai-derived theme.

## Contributing

Pull requests welcome for additional themes following these principles. Open an issue first if you want to propose a new theme family, so we can discuss the palette before you do the work. Each theme contribution should include both a JSON file in `themes/` and a paired markdown README explaining the color rationale, so future users can audit whether your choices match their needs.

## Credits

- Original color palettes credited per-theme (e.g. Monokai by Wimer Hazenberg)
- Theme structure and Claude Code token mapping reference: [matcra587/claude-themes](https://github.com/matcra587/claude-themes)
- Okabe & Ito (2008), [Color Universal Design](https://jfly.uni-koeln.de/color/) — the canonical CVD-safe palette

## License

MIT — see [LICENSE](LICENSE).

## Disclaimer

Not affiliated with, endorsed by, or sponsored by Anthropic. "Claude" and "Claude Code" are trademarks of Anthropic. Original palette names ("Monokai," etc.) are trademarks of their respective creators; this repo uses them descriptively to indicate derivation.
