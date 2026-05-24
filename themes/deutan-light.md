# Deutan Light

A Claude Code light theme designed specifically for strong deuteranopia — high luminance contrast against a white background, no reliance on green signal, and the selection cue rebuilt around the 100% blue cone.

## Designed for

This theme is built around the same cone response profile as its dark counterpart:

| Cone | Response |
|---|---|
| Blue (S) | 100% |
| Red (L) | 75% |
| Green (M) | 0% |

Strong deutan: M-cone effectively non-functional, L-cone reduced, S-cone fully intact. See [Deutan Dark](deutan-dark.md) for the dark-mode counterpart.

## Installation

Copy `deutan-light.json` into `~/.claude/themes/`, then run `/theme` in a Claude Code session and select **Deutan Light**.

## Why light mode needs different choices

Naively inverting a dark theme into a light theme breaks for deutan vision in two specific ways, both addressed here.

**Yellow doesn't work as a selection cue on white.** Yellow has high luminance, which is what made it the dominant focus indicator in Deutan Dark — but on a white background, that same high luminance means it has *low contrast* against the background. Yellow on white is unreadable for anyone, CVD or not.

The fix: selection cues in this theme use **deep saturated blue** `rgb(30,64,175)` instead. This exploits your 100% S-cone (the strongest signal you have) and provides ~10:1 contrast against the white background. The semantic ("this is what's active") is preserved; the specific hue changes because the contrast math demands it.

**Status colors need to be darker, not brighter.** On a dark background, light/saturated status colors pop. On a white background, those same colors wash out. Every status color in this theme is the darker, more saturated variant of its dark-mode equivalent — magenta becomes deep rose, orange becomes burnt umber, cyan-teal becomes a darker teal.

## Design principles

**Blue as the primary accent everywhere.** Selection cues, prompt border, IDE indicator, brief-label-Claude marker, added-diff highlight all use blue at varying saturations. This is the strongest signal available to S=100% vision, and using it consistently makes the whole UI feel more legible.

**Green replaced with darker teal.** `success` is `rgb(13,148,136)` — a darker, more saturated teal than the dark-mode version, chosen for contrast against white. Same reasoning as Deutan Dark: pure green carries no useful information at M=0, so cyan-teal is the closest "go" semantic that actually transmits a signal.

**Errors use deep magenta-rose.** `rgb(190,24,93)` — same hue family as the dark-mode magenta, but darker for white-background contrast. Still exploits the S-cone for alarm signal.

**Diffs use light blue and light orange backgrounds.** Subtle tinted backgrounds (rather than the deep saturated colors used in dark mode) so the diff text on top remains readable. Word-level highlights are more saturated to draw the eye to specific changes.

**Pure white background.** `rgb(255,255,255)`. Some light themes lean toward off-white or cream to reduce eye strain, but for accessibility purposes pure white maximizes contrast against every other color — and that contrast matters more than the slight aesthetic difference.

## Key token decisions

| Token | Value | Reasoning |
|---|---|---|
| `background` | `rgb(255,255,255)` | Pure white for maximum contrast |
| `text` | `rgb(15,15,15)` | Near-black, ~19:1 contrast |
| `subtle` | `rgb(60,60,60)` | ~12:1 contrast — readable metadata |
| `inactive` | `rgb(95,95,95)` | ~7:1 contrast — secondary text, still AAA |
| `suggestion` | `rgb(30,64,175)` | Deep blue — replaces dark mode's yellow, exploits S-cone |
| `permission` | `rgb(30,64,175)` | Same deep blue |
| `selectionBg` | `rgb(219,234,254)` | Pale blue tint for selected-line backgrounds |
| `success` | `rgb(13,148,136)` | Dark teal, replaces invisible green |
| `error` | `rgb(190,24,93)` | Deep magenta-rose, exploits S-cone |
| `warning` | `rgb(194,65,12)` | Burnt umber, distinct from error magenta |
| `diffAdded` | `rgb(191,219,254)` | Pale blue background tint |
| `diffRemoved` | `rgb(254,215,170)` | Pale orange background tint |
| `promptBorder` | `rgb(37,99,235)` | Saturated blue, visible against white |

## Customization tips

The JSON hot-reloads — edit values and the running session reflects them immediately.

- If the deep blue selection cue feels too dark, lift to `rgb(37,99,235)`. Still high contrast on white but slightly brighter.
- If pure white background causes eye strain in low light, try `rgb(250,250,250)` or `rgb(248,248,248)` — barely-visible warmth that reduces strain without significantly compromising contrast.
- If diff backgrounds (`diffAdded` / `diffRemoved`) feel too washed out, push them toward `rgb(147,197,253)` / `rgb(253,186,116)` for stronger tints.

## Credits

- Cone response profile measured via [EnChroma Color Vision Test](https://enchroma.com/pages/test)
- Theme structure and Claude Code token mapping reference: [matcra587/claude-themes](https://github.com/matcra587/claude-themes)
- Okabe-Ito blue/orange diff palette: Okabe & Ito (2008), [Color Universal Design](https://jfly.uni-koeln.de/color/)
