# iTerm2 Themes

iTerm2 color presets that pair with the Claude Code themes in this repo. Same design principles, adapted to fit iTerm2's ANSI 16-color palette and special-color slots.

## Themes

| File | Pairs with | Base |
|---|---|---|
| `deutan-dark.itermcolors` | [Deutan Dark](../themes/deutan-dark.md) | dark |
| `deutan-light.itermcolors` | [Deutan Light](../themes/deutan-light.md) | light |

## Installation

1. Open iTerm2 → **Settings** → **Profiles** → **Colors**
2. Click **Color Presets…** (bottom right) → **Import…**
3. Select the `.itermcolors` file you want to import
4. Click **Color Presets…** again and select the now-imported preset

The preset applies to whichever profile you have selected on the left. If you want both dark and light themes available, import both and switch between them via the Color Presets dropdown.

For automatic dark/light switching tied to macOS appearance, see [iTerm2's dynamic profiles](https://iterm2.com/documentation-dynamic-profiles.html) — you can define a profile that swaps presets based on system appearance, though it requires JSON profile config rather than the GUI.

## ANSI palette mapping

The trick for CVD-friendly terminal themes is preserving the *semantic slots* (ANSI 1 is still "red," ANSI 2 is still "green") while shifting the actual rendered colors to hues the user can decode. Applications that say "print this in red" still get an alarm-colored output — the alarm color just happens to be magenta instead of pure red.

### Key substitutions (both themes)

| ANSI slot | Standard | Deutan Dark | Deutan Light | Why |
|---|---|---|---|---|
| 1 (red) | pure red | magenta | deep rose | Red is decoded poorly at M=0; magenta uses the S-cone (100%) for alarm signal |
| 2 (green) | pure green | cyan-teal | dark teal | Pure green is functionally invisible at M=0; cyan-teal carries via the S-cone |
| 4 (blue) | blue | bright blue | saturated blue | Blue is the strongest signal — kept as the workhorse color |
| 5 (magenta) | magenta | purple | deep purple | Slot 1 took magenta, so slot 5 shifts to purple — visually distinct |
| 6 (cyan) | cyan | brighter cyan | dark cyan | Distinguished from slot 2 by saturation and luminance |

### Special slots

`Selection Color` and `Cursor Color` mirror the corresponding Claude Code theme's `suggestion` value — yellow in dark mode, deep blue in light mode. This keeps the "active item" cue consistent whether you're in Claude Code's UI or running other terminal apps.

`Link Color` uses saturated blue (slot 4) since blue is the most legible color for clickable elements and the S-cone is fully intact. `Badge Color` uses magenta (slot 1) so iTerm2 badges read as high-priority signals.

## Known limitations

Several pairs of ANSI colors will look similar for severe deutan vision and there's no clean way to fix this without breaking semantic expectations:

- **Slot 2 (cyan-teal) and slot 6 (cyan)** — both lean blue-cyan with M=0. Differentiated by luminance and slight saturation differences, but apps that use both heavily (some syntax highlighters) may have low contrast between them.
- **Slot 1 (magenta) and slot 5 (purple)** — both have heavy blue content. Slot 5 is more violet, slot 1 more pink, but the discrimination is subtle.

If a specific app's color usage feels muddy, the right fix is usually configuring that app's own color settings (e.g., vim/neovim colorschemes, bat themes) rather than re-tuning the terminal palette globally.

## Companion Claude Code themes

For the full setup, also install the matching Claude Code theme from [`../themes/`](../themes/). The selection color and cursor color in these iTerm2 presets are intentionally aligned with the Claude Code theme's `suggestion` color so the visual signal for "this is what's active" is consistent across both UIs.
