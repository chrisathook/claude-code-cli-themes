# Deutan Themes for VS Code / Cursor

A VS Code extension that contributes two themes — **Deutan Dark** and **Deutan Light** — designed for severe deuteranopia. The same extension installs in Cursor (Cursor is a VS Code fork and shares the theme format).

## Themes

| Theme | UI base | Pairs with |
|---|---|---|
| Deutan Dark | `vs-dark` | [Claude Code Deutan Dark](../themes/deutan-dark.md), [iTerm2 Deutan Dark](../iterm2/) |
| Deutan Light | `vs` | [Claude Code Deutan Light](../themes/deutan-light.md), [iTerm2 Deutan Light](../iterm2/) |

The selection cue, diff palette, and status colors mirror the Claude Code themes — so when you switch between Claude Code, an iTerm2 window, and VS Code/Cursor, the visual language stays consistent.

## Installation

### Option 1: Local extension (fastest for personal use)

VS Code and Cursor expect extension directories to be named `<publisher>.<name>-<version>`. The bundled `package.json` declares publisher `chrisw` and name `deutan-themes`, so the install directory must be `chrisw.deutan-themes-1.0.0` — not just `deutan-themes-1.0.0`. If you forked and changed the publisher, substitute your value.

For Cursor:
```bash
mkdir -p ~/.cursor/extensions/chrisw.deutan-themes-1.0.0
cp -r vscode/* ~/.cursor/extensions/chrisw.deutan-themes-1.0.0/
```

For VS Code:
```bash
mkdir -p ~/.vscode/extensions/chrisw.deutan-themes-1.0.0
cp -r vscode/* ~/.vscode/extensions/chrisw.deutan-themes-1.0.0/
```

Restart the editor (or `Cmd+Shift+P` → **Developer: Reload Window**), then open the theme picker with `Cmd+K Cmd+T` and select **Deutan Dark** or **Deutan Light**.

### Option 2: Build a `.vsix` package

If you want a clean install/uninstall path or plan to share it with others on your team:

```bash
cd vscode/
npm install -g @vscode/vsce
vsce package
# produces deutan-themes-1.0.0.vsix

code --install-extension deutan-themes-1.0.0.vsix
# for Cursor:
cursor --install-extension deutan-themes-1.0.0.vsix
```

Installing via `.vsix` takes care of the directory naming automatically — no manual prefix needed.

### Option 3: Publish to the Marketplace

For wider distribution, follow [VS Code's publishing guide](https://code.visualstudio.com/api/working-with-extensions/publishing-extension). You'll need a Microsoft Partner Center account with a registered `chrisw` publisher and a personal access token. Cursor users can install marketplace extensions via the [Open VSX Registry](https://open-vsx.org/) or by manually downloading `.vsix` files.

## Switching themes

`Cmd+K Cmd+T` opens the **Color Theme** picker. Arrow up/down (you'll see live previews as you move through the list — handy for verifying contrast feels right). Press Enter to commit.

For automatic dark/light switching tied to macOS appearance:

1. **Settings** (`Cmd+,`) → search for `Auto Detect Color Scheme`
2. Enable **Window: Auto Detect Color Scheme**
3. Set **Workbench: Preferred Dark Color Theme** to `Deutan Dark`
4. Set **Workbench: Preferred Light Color Theme** to `Deutan Light`

Now the editor follows your macOS appearance setting automatically. Same setting works in Cursor.

## Design notes

### Selection cue switches color between themes

This is the same trade-off described in the [Claude Code Deutan Light README](../themes/deutan-light.md):

- **Dark theme**: bright yellow `#FFD60A` for `list.activeSelectionBackground`, `tab.activeBorderTop`, `editorCursor.foreground`, and find-match highlights
- **Light theme**: deep blue `#1E40AF` for the same tokens — yellow has too little contrast on white

Once you adjust to "yellow in dark, blue in light = focus indicator," it's consistent within each theme.

### Diff colors use Okabe-Ito blue/orange

`diffEditor.insertedTextBackground` and `diffEditor.insertedLineBackground` use blue tints; `removed` versions use orange tints. This avoids the green-vs-red discrimination problem entirely. Git decorations in the sidebar follow the same logic — added files are blue, deleted files are orange, modified files are amber.

### Bracket pair colorization uses six CVD-safe hues

`editorBracketHighlight.foreground1` through `foreground6` are: blue, orange, purple, magenta, teal, amber. No greens. All six hues are distinguishable for severe deutan vision, so nested bracket pairs read clearly even at deep nesting levels.

### Syntax highlighting avoids yellow conflict

The selection cue uses pure bright yellow `#FFD60A`. Syntax strings use amber `#FBBF24` (more orange-leaning) so they're visually distinct from the selection highlight even though both are in the warm range. Functions use teal instead of yellow, which most themes default to.

### Terminal palette inside the editor matches iTerm2

The integrated terminal's ANSI palette (`terminal.ansiRed`, `terminal.ansiGreen`, etc.) uses the same substitutions as the standalone iTerm2 preset — ANSI "red" is magenta, ANSI "green" is teal, etc. So apps that print colored output behave consistently whether you're in the integrated terminal or a separate iTerm2 window.

## Customization

Theme JSON files are in `themes/`. The structure is standard VS Code theme format:

- `colors` — workbench/UI color tokens (sidebar, tabs, status bar, etc.)
- `tokenColors` — syntax highlighting via TextMate scopes

Edit either file, reload the window (`Cmd+Shift+P` → **Developer: Reload Window**), and the changes apply. For live editing of an active theme, install the [Theme Editor](https://marketplace.visualstudio.com/items?itemName=Tyriar.theme-editor) extension or use **Developer: Generate Color Theme from Current Settings** to scaffold from your current state.

## Credits

- Cone response profile measured via [EnChroma Color Vision Test](https://enchroma.com/pages/test)
- Theme JSON schema: VS Code's [color theme documentation](https://code.visualstudio.com/api/extension-guides/color-theme)
- Okabe-Ito blue/orange diff palette: Okabe & Ito (2008), [Color Universal Design](https://jfly.uni-koeln.de/color/)
