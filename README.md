# puretui

**A zero-dependency, pure-stdlib terminal UI toolkit for Python (POSIX).**

A styled cell-grid canvas with clipped regions, truecolor ANSI with
256/16/mono fallback, flexbox-style layout, raw keyboard + mouse input
(bracketed paste, focus events), a flicker-free diff renderer, procedural
widgets, an app kit (views, keymaps, command palette), and snapshot
testing — in about 3,000 lines you can read in an afternoon.

```python
from puretui import Canvas, Fixed, Flex, Theme, run
from puretui import widgets

def render(cols, rows, frame):
    cv = Canvas(cols, rows, widgets.base_style())
    root = cv.region()
    head, body = root.split_v(Fixed(2), Flex(1))
    head.left("hello, puretui", r=0)
    head.rule(r=1)
    body.center("q to quit", r=body.h // 2)
    return cv.to_lines()

run(render, on_key=lambda k: k not in ("q", "Q"))
```

- **Zero dependencies.** Python 3.8+ standard library only. POSIX (macOS/Linux).
- **Explicit.** Procedural drawing, plain data, no reactivity, no magic.
- **Tested.** 600+ unit tests, property tests, a fuzzed input decoder,
  and byte-exact golden snapshots.
- **Fast.** ~2ms full frames at 120x40; steady-state frames ~0.015ms
  (`python3 benchmarks/bench.py` for numbers on your machine).

## Install

```sh
pip install puretui
```

## Examples

```sh
python3 examples/dashboard.py    # layout, tables, sparklines, mouse
python3 examples/logtail.py      # app kit: views, filter capture, palette
```

## Status

Pre-1.0: the API is stabilizing (`__all__` defines the public surface;
see CHANGELOG.md). Built as the engine of a
[World Cup terminal dashboard](https://github.com/0JamesAB/worldcup26) —
the flagship consumer that keeps every release honest with byte-identical
rendering oracles.

## License

MIT
