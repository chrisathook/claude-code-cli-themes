# Monokai CVD Aggressive

A Claude Code theme derived from the classic Monokai palette by Wimer Hazenberg, modified for aggressive color vision deficiency (CVD) safety and elevated contrast. The goal is to preserve the recognizable Monokai aesthetic — the charcoal background, the warm pinks and limes — while fixing the specific spots where the original palette is hostile to CVD users or has poor luminance contrast.

## Installation

Copy `monokai-cvd-aggressive.json` into `~/.claude/themes/`, then run `/theme` in a Claude Code session and select **Monokai CVD Aggressive**.

## What this fixes vs. classic Monokai

Monokai is already one of the more CVD-friendly popular palettes — its iconic pink/magenta and yellow-green pairing is genuinely distinguishable for deuteranopia and protanopia, which is better than most themes. The issues addressed by this variant are smaller but high-impact.

### Selection highlights had no dedicated hue

In original Monokai, both `suggestion` (the arrow-key selection highlight in command pickers) and `promptBorder` (the input box border) are cyan. When everything important is cyan, nothing reads as "this is what's selected right now."

The fix sets `suggestion`, `permission`, `permissionShimmer`, and `remember` all to bright yellow `rgb(255,214,10)` (`#FFD60A`) — a hue used nowhere else in the theme. Yellow has the highest luminance of any saturated color and is unambiguously distinguishable for all common CVD types. `inverseText` is set to pure black so text on the yellow highlight stays legible.

### Diffs used green vs. pink — the highest-risk CVD task

Diff review is where users compare colors most carefully and where weak hue discrimination causes the most friction. While Monokai's lime green `rgb(166,226,46)` and pink `rgb(249,38,114)` are technically distinguishable for red-green CVD, both still carry a green-or-not-green cognitive load that the Okabe-Ito palette avoids entirely.

Diff colors are remapped to a blue (added) / orange (removed) pairing:

| Token | Color | Value |
|---|---|---|
| `diffAdded` | deep blue | `rgb(30,64,175)` |
| `diffAddedDimmed` | darker blue | `rgb(30,58,138)` |
| `diffAddedWord` | vivid blue | `rgb(37,99,235)` |
| `diffRemoved` | burnt orange | `rgb(154,52,18)` |
| `diffRemovedDimmed` | darker orange | `rgb(124,45,18)` |
| `diffRemovedWord` | vivid orange | `rgb(234,88,12)` |

Blue vs. orange is distinguishable purely on hue for all CVD types and reinforced by a strong luminance gap. This is the single most aggressive change in the theme and the one with the largest practical impact on daily use.

### Warning and selection were both yellow

Monokai's `warning` is soft yellow `rgb(230,219,116)` (`#E6DB74`), which sits too close to the new selection yellow to read as a distinct signal. `warning` shifts to Monokai's own orange `rgb(253,151,31)` (`#FD971F`) — already in the palette, semantically reads as "caution," and doesn't compete with the selection cue.

### Secondary text was unreadable

Monokai's `subtle` (`rgb(117,113,94)`) sits at roughly 3:1 contrast against the dark background — below WCAG AA. The problem is worse for `inactive` and `inactiveShimmer`, which are even darker. The practical effect is that metadata under the welcome banner (model name, project path) and the footer shortcuts hint are genuinely hard to read.

All three secondary-text tokens were brightened while preserving Monokai's warm olive-gray hue. Each RGB channel was scaled proportionally toward white, so the relative warmth is maintained but luminance jumps into AAA territory.

| Token | Before | After | Contrast vs bg |
|---|---|---|---|
| `subtle` | `rgb(117,113,94)` | `rgb(217,213,196)` | ~3:1 → ~10:1 |
| `inactive` | `rgb(73,72,62)` | `rgb(182,178,166)` | ~1.4:1 → ~7:1 |
| `inactiveShimmer` | `rgb(95,92,78)` | `rgb(196,192,178)` | ~2:1 → ~8:1 |

## What this preserves from classic Monokai

The background stays at the iconic `rgb(39,40,34)` charcoal, and primary text stays at the near-white `rgb(248,248,242)` — both untouched.

`error` keeps Monokai's pink `rgb(249,38,114)`. Magenta is the safest "alarm" color for CVD because it retains its blue channel even when red sensitivity is absent, so it still reads as a high-alarm signal for deutan, protan, and tritan vision alike.

`success` keeps Monokai's lime green `rgb(166,226,46)`. Pure red/green pairings are CVD-risky, but green *alone* at high luminance still reads as "OK." Paired against magenta error rather than red error, the discrimination is hue plus luminance plus context — multiple redundant signals.

Branding tokens (`claude`, `claudeShimmer`, `claudeBlue_FOR_SYSTEM_SPINNER`, etc.), accent colors for plan mode and auto-accept, the IDE indicator, the eight-slot subagent palette, and the rainbow gradient are all kept at their original Monokai values. These rarely carry critical decision-making information and benefit from retaining the recognizable Monokai feel.

## CVD types this is designed for

The aggressive choices in this theme target the four most common categories of color vision deficiency, in roughly decreasing order of prevalence:

**Deuteranopia and deuteranomaly** (red-green, the most common form): diff blue/orange, selection yellow, and magenta errors all survive deutan vision intact.

**Protanopia and protanomaly** (red-green, less common but similar): the same choices that work for deutan also work here. Both forms confuse red and green; the theme avoids that pairing entirely for high-stakes UI roles.

**Tritanopia and tritanomaly** (blue-yellow, rare): selection yellow still reads as the brightest hue available, and the diff blue and orange remain distinguishable by luminance even if the hue distinction muddies.

**Monochromacy** (full color blindness, very rare): every semantic distinction in this theme is also encoded in luminance, so it degrades gracefully to grayscale rather than collapsing into a single mid-tone smear.

## Customization

The JSON hot-reloads — edit hex or RGB values, save, and the running Claude Code session reflects the change without a `/theme` cycle. Common per-user tweaks:

- If the diff blue feels too dark on your terminal, brighten `diffAdded` toward `rgb(59,130,246)` while keeping the orange-removed contrast.
- If pure black `inverseText` is too harsh on the yellow highlights, try `rgb(20,20,20)` for a slight softening without losing legibility.
- If you have tritan vision specifically and the selection yellow feels muddy, try a pure white `rgb(255,255,255)` instead — luminance contrast carries the signal even when hue distinction is weak.

## Credits

- Original Monokai palette: [Wimer Hazenberg](https://monokai.nl/)
- Theme structure and Claude Code token mapping reference: [matcra587/claude-themes](https://github.com/matcra587/claude-themes)
- CVD-safe diff palette: Okabe & Ito (2008), [Color Universal Design](https://jfly.uni-koeln.de/color/)
