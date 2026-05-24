# Deutan Dark

A Claude Code dark theme designed specifically for strong deuteranopia — high luminance contrast, no reliance on green signal, and a palette tuned to which cones are actually firing.

## Designed for

This theme is built around a specific cone response profile measured via EnChroma's cone-isolation test:

| Cone | Response |
|---|---|
| Blue (S) | 100% |
| Red (L) | 75% |
| Green (M) | 0% |

That's a strong deutan presentation — the M-cone is effectively non-functional, the L-cone is reduced, and the S-cone is fully intact. The design choices follow directly from those numbers.

For a light-mode counterpart with the same design principles, see [Deutan Light](deutan-light.md).

## Installation

Copy `deutan-dark.json` into `~/.claude/themes/`, then run `/theme` in a Claude Code session and select **Deutan Dark**.

## Design principles

**Blue is the workhorse color.** With S-cone at 100%, blue carries the strongest and most reliable signal of any hue. The theme leans on blue for the input box border, the IDE indicator, the brief-label-Claude marker, and most importantly the added-diff highlight. When in doubt, blue is the safe choice.

**Green is gone — replaced with cyan-teal.** Pure green (anything in the lime / forest / emerald range) is decoded purely by luminance with M=0, so it carries no useful hue information. `success`, `fastMode`, and the green subagent slot all shift to cyan-teal `rgb(20,184,166)` — that hue blends blue and green, but since green is missing, it reads as a saturated dark cyan that's distinguishable from pure blue by the slight green-derived shift in apparent luminance.

**Yellow stays as the selection cue.** Yellow stimulates the L-cone (75% functional) and M-cone (0%), so it appears slightly dimmer than to normal vision, but it remains high-luminance and unambiguously distinct against the near-black background. `suggestion`, `permission`, and `remember` all use `rgb(255,214,10)` — and no other role uses yellow, so when something pops yellow it's unambiguously a focus indicator.

**Errors use magenta, not red.** Magenta is red plus blue, and the S-cone carries the signal through even with reduced L-cone. `rgb(236,72,153)` reads as a high-alarm color across the entire deutan spectrum.

**Diffs use blue (added) and orange (removed).** With M=0, red-vs-green discrimination is impossible — green looks like dim yellow-brown, regardless of luminance. Blue vs orange exploits the two strongest remaining cone signals (S at 100%, L at 75%) and reinforces with a strong luminance gap.

**Background pushed darker than standard.** `rgb(10,10,10)` (vs. typical dark themes at `rgb(30,30,35)` or so) increases the contrast ratio for every foreground color, which helps when reduced L-cone response makes warmer colors appear dimmer than they would to normal vision.

## Key token decisions

| Token | Value | Reasoning |
|---|---|---|
| `background` | `rgb(10,10,10)` | Near-black for maximum contrast against every other color |
| `text` | `rgb(255,255,255)` | Pure white, ~20:1 contrast |
| `subtle` | `rgb(210,210,210)` | ~14:1 contrast — readable metadata text |
| `inactive` | `rgb(160,160,160)` | ~8:1 contrast — visible but clearly secondary |
| `suggestion` | `rgb(255,214,10)` | Yellow, exclusive focus indicator |
| `permission` | `rgb(255,214,10)` | Same yellow — selection-family role |
| `success` | `rgb(20,184,166)` | Cyan-teal, replaces invisible green |
| `error` | `rgb(236,72,153)` | Magenta, exploits S-cone |
| `warning` | `rgb(251,146,60)` | Saturated orange, distinct from selection yellow |
| `diffAdded` | `rgb(30,58,138)` | Deep blue background |
| `diffRemoved` | `rgb(154,52,18)` | Burnt orange background |
| `promptBorder` | `rgb(59,130,246)` | Bright blue — high-confidence signal at the input box |

## Customization tips

The JSON hot-reloads — edit values and the running Claude Code session reflects them without a `/theme` cycle.

- If success cyan-teal feels too close to pure blue, push it greener with `rgb(45,212,191)` — adds more apparent luminance without re-introducing the green-discrimination problem.
- If the magenta error feels too pink for "alarm," try `rgb(219,39,119)` for a deeper, more saturated tone.
- If pure white text is too bright, try `rgb(240,240,240)` — still ~17:1 contrast on the near-black background.

## Credits

- Cone response profile measured via [EnChroma Color Vision Test](https://enchroma.com/pages/test)
- Theme structure and Claude Code token mapping reference: [matcra587/claude-themes](https://github.com/matcra587/claude-themes)
- Okabe-Ito blue/orange diff palette: Okabe & Ito (2008), [Color Universal Design](https://jfly.uni-koeln.de/color/)
