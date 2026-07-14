# Changelog

All notable changes to puretui are documented here. The format follows
[Keep a Changelog](https://keepachangelog.com/); versions follow semver.
The public API is the set of names in each module's `__all__`; exact
emitted ANSI bytes are NOT covered by semver (first-frame goldens still
never change silently — see docs/stability at 1.0).

## [Unreleased]

## [0.6.0] - 2026-07-14
### Changed
- **Renamed: the import and dist name is now `puretui`** (was repo-local
  `tui` / dist `tui-core`, never published).
- Public API frozen: every module declares `__all__`; a permanent test
  pins `__all__` <-> package exports <-> pyproject consistency.
### Added
- Bracketed paste (always on; `PasteEvent`), focus events
  (`RawTerminal(focus=True)`, `FocusEvent`), OSC 52 clipboard
  (`osc52_copy`), terminal title push/pop (`RawTerminal(title=...)`),
  cursor shapes (`set_cursor_shape`).
- `read_key(fd=...)` injectable input seam; fuzzed decoder.
- `Canvas.clear()` in-place frame reset; `App.run` reuses the frame canvas.
- Property tests; publishable `benchmarks/bench.py`.
### Performance
- Renderer raw-line memo (unchanged lines cost ~nothing; steady-state
  frame ~0.015ms), width caches, color-string interning: full-frame
  renders ~14% faster than 0.5.0, ~25% faster than 0.2.0.

## [0.5.0] - 2026-07-08
### Added
- App kit: `App` (view stack, keymaps, capture modality, mouse dispatch),
  kit-side `Toast`/`Toasts`; `puretui.commands` (`CommandSet`, `Palette`,
  palette drawing).
### Fixed
- Wheel events no longer bypass an active capture; toast prune races.

## [0.4.0] - 2026-07-05
### Added
- Widgets on Region: `select_list` (run-fit windowing, integrated click
  handling), `text_pane`, `popup`/`modal`, `LineEdit` + `input`,
  `col_layout`, `meter_rows`.

## [0.3.0] - 2026-07-04
### Added
- `Region`: clipped local-coordinate drawing surfaces (alignment verbs,
  cursor flow, splits, HitMap integration, windowed blit, widget sugar);
  Canvas clip plumbing; `theme.presets()`.

## [0.2.0] - 2026-07-01
### Added
- Layout engine (`Rect`, `Fixed`/`Flex`, splits), `run()` loop,
  `ListState`/`ScrollState`/`HitMap`, `Style` objects, testing helpers,
  ANSI-aware `wrap()`, SGR mouse decoding, synchronized output.
### Changed
- Color depth `"16"` now emits real 16-color SGR codes; the no-color
  tier is `"mono"` (`NO_COLOR`/`TERM=dumb`).

## [0.1.0] - 2026-07-01
- Initial extraction: `term` (colors/input/renderer), `Canvas`, themes,
  procedural widgets incl. the single-elimination bracket renderer.
