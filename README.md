# macOS for shadcn

A desktop-first macOS style for current official shadcn components, designed for React apps on the web, Electron, and Tauri.

> macOS for shadcn is an independent open-source project. It is not affiliated with, endorsed by, or sponsored by Apple Inc. or the shadcn project. It includes no Apple fonts, symbols, artwork, templates, or application screenshots.

## Status

This repository is an early implementation. The GitHub registry contract, complete Base UI fixture, foundational style layer, and self-hosted showcase are under active verification. Native macOS 27 calibration is incomplete until the reference harness is run with Xcode 27.

## Preview locally

```sh
pnpm install
pnpm dev
```

The Vite showcase includes the product landing page, live controls, component catalogue, conformance status, host notes, and copyable agent instructions.

## Install in an existing shadcn app

Prefer a release tag or full commit SHA once a verified preview commit is available:

```sh
pnpm dlx shadcn@latest add juanmaramos/macos-for-shadcn/macos#<full-commit-sha> --dry-run
pnpm dlx shadcn@latest add juanmaramos/macos-for-shadcn/macos#<full-commit-sha> --diff
pnpm dlx shadcn@latest add juanmaramos/macos-for-shadcn/macos#<full-commit-sha>
```

Then opt in at the application root:

```tsx
<html data-macos-style="27">
```

The unpinned convenience form follows the repository default branch:

```sh
pnpm dlx shadcn@latest add juanmaramos/macos-for-shadcn/macos
```

Continue installing official components normally. The style does not replace their source or behavior.

```sh
pnpm dlx shadcn@latest add button dialog table sidebar
```

## Paste into an agent

Copy the maintained prompt from [`docs/agent-prompt.md`](docs/agent-prompt.md). It tells an agent to inspect the target app, preview the registry diff, preserve official component source, install the style, verify the CSS import, and enable the root attribute.

## Customization

Brand-safe variables keep the default geometry and interaction grammar:

```css
html[data-macos-style="27"] {
  --macos-accent: oklch(0.63 0.19 252);
  --macos-canvas: oklch(0.965 0.006 250);
  --macos-content: oklch(0.985 0.003 250);
  --macos-sidebar-tint: oklch(0.94 0.018 245);
  --macos-glass-opacity: 0.78;
}
```

See [`docs/customization.md`](docs/customization.md) for advanced variables and opt-outs.

## Compatibility

| Host | Core CSS | Host material integration | Current status |
| --- | --- | --- | --- |
| Browser | Same `macos.css` | In-page backdrop filtering only | Fixture builds |
| Electron | Same `macos.css` | Optional transparent/vibrant window | Smoke example pending |
| Tauri | Same `macos.css` | Optional transparent/vibrant window | Smoke example pending |

## Known ceilings

DOM controls cannot escape the host window, reproduce AppKit accessibility roles, sample arbitrary desktop content, or match AppKit/Core Text rasterization exactly. See [`docs/deviations.md`](docs/deviations.md).

## Development

```sh
pnpm registry:validate
pnpm test:coverage
pnpm build
pnpm verify
```

Upstream versions and the current calibration status are recorded in [`docs/upstream.md`](docs/upstream.md). Generated component coverage lives in [`coverage/components.json`](coverage/components.json).

## License

[MIT](LICENSE)
