# Claude Code Themes

A personal collection of custom themes for Claude Code. Some are accessibility-focused, some are aesthetic variants of established palettes, some are project-specific. Each theme has its own README in `themes/` explaining what it is and why the colors were chosen.

## Installation

Drop any theme JSON into `~/.claude/themes/`, then in a running Claude Code session run `/theme` and pick it from the list. Claude Code watches the directory and hot-reloads, so edits to the JSON apply live to the active session without restarting.

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

The pre-selection step matters for ephemeral containers where you don't want to run `/theme` every session.

## Themes

| Theme | Base | Description |
|---|---|---|
| [Deutan Dark](themes/deutan-dark.md) | `dark` | Personal high-contrast dark theme tuned to a specific strong-deutan cone profile (S=100%, L=75%, M=0%). Blue-dominant palette, cyan-teal replaces green, yellow selection cue. |
| [Deutan Light](themes/deutan-light.md) | `light` | Light-mode counterpart to Deutan Dark. Selection cue switches to deep blue (yellow doesn't work on white), status colors darkened for white-background contrast. |
| [Monokai CVD Aggressive](themes/monokai-cvd-aggressive.md) | `dark` | Generic CVD-friendly variant of Monokai. Okabe-Ito blue/orange diffs, yellow selection cue, brightened metadata. Less personalized than the Deutan themes — use these if you want Monokai's aesthetic and have any common form of CVD. |

Each theme's README documents what was changed from its source palette and the rationale behind the choices.

## iTerm2 companion themes

Matching iTerm2 color presets are in [`iterm2/`](iterm2/) — they share the same selection cue, cursor color, and overall palette philosophy as the Claude Code themes, so running Claude Code inside iTerm2 feels cohesive. See [iterm2/README.md](iterm2/README.md) for installation.

## VS Code / Cursor companion themes

Matching themes for VS Code and Cursor are in [`vscode/`](vscode/) as a single installable extension contributing both **Deutan Dark** and **Deutan Light**. Mirrors the Claude Code themes for selection cue, diff palette, and integrated-terminal ANSI colors. See [vscode/README.md](vscode/README.md) for installation methods.

## Contributing

Pull requests welcome. Open an issue first if you want to propose a new theme so we can discuss the palette before you do the work. Each contribution should include both a JSON file in `themes/` and a paired markdown README explaining the color choices — the rationale is what makes a theme worth keeping around, not just the hex values.

## Credits

Source palettes and external references are credited per-theme in each theme's README.

## License

MIT — see [LICENSE](LICENSE).

## Disclaimer

Not affiliated with, endorsed by, or sponsored by Anthropic. "Claude" and "Claude Code" are trademarks of Anthropic. Original palette names are trademarks of their respective creators; this repo uses them descriptively to indicate derivation.
