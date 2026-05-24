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
| [Monokai CVD Aggressive](themes/monokai-cvd-aggressive.md) | `dark` | Monokai-derived with aggressive CVD safety — Okabe-Ito blue/orange diffs, bright yellow selection cue, brightened metadata text. |

Each theme's README documents what was changed from its source palette and the rationale behind the choices.

## Contributing

Pull requests welcome. Open an issue first if you want to propose a new theme so we can discuss the palette before you do the work. Each contribution should include both a JSON file in `themes/` and a paired markdown README explaining the color choices — the rationale is what makes a theme worth keeping around, not just the hex values.

## Credits

Source palettes and external references are credited per-theme in each theme's README.

## License

MIT — see [LICENSE](LICENSE).

## Disclaimer

Not affiliated with, endorsed by, or sponsored by Anthropic. "Claude" and "Claude Code" are trademarks of Anthropic. Original palette names are trademarks of their respective creators; this repo uses them descriptively to indicate derivation.
