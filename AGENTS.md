# Repository guidance

## Mission

Build a style-only shadcn registry that makes current official Base UI components
feel at home in macOS 27 while preserving their React APIs and behavior. The
implementation brief in `docs/MACOS_FOR_SHADCN_ONE_SHOT.md` is authoritative.

`registry/styles/macos.css` is the product. The Vite app in `apps/showcase` is
the product preview, documentation site, and component fixture.

## Current checkpoint

- Bootstrapped on 2026-08-08 with shadcn CLI 4.16.2, the `base-rhea` preset,
  Base UI, React 19, Tailwind CSS v4, Vite, and pnpm 10.28.2.
- The generated fixture contains all 61 current official component modules.
- The registry exposes `macos` and the generation-pinned `macos-27` style item.
- The CSS file contains only the safe system-font and root-token foundation.
  Component styling is intentionally pending visual reference extraction.
- This host has macOS 26.5.2, Xcode 26.6, and the macOS 26.5 SDK. Apple has
  published Xcode 27 betas with the macOS 27 SDK, but one is not installed here.

Do not describe this checkpoint as a complete theme or verified native match.

## Figma handoff

Primary supplementary reference:

`https://www.figma.com/design/ICPoIaFDbiAq3IET4WWZ7t/macOS-27--Community-?node-id=207-14472`

The public Community page is visible in a browser, but the current Figma MCP
connector reported that it requires edit access before it can read the file.
The project owner plans to duplicate the file into their drafts/team and then
provide that duplicate URL. Verify MCP access before continuing extraction.

Once accessible, inspect rather than export. Capture only derived values needed
for original CSS, in this order:

1. semantic colors and material hierarchy;
2. text roles, weights, sizes, and line heights;
3. control heights, radii, padding, icon sizes, and concentric relationships;
4. light, dark, active, inactive, hover, pressed, selected, disabled, and focus states;
5. menu, popover, dialog, toolbar, sidebar, table, and form-control recipes;
6. motion timings and accessibility variants where the source documents them.

Record derived decisions and uncertainty in `docs/provenance.md`; do not copy
raw Figma assets into the repository. The project owner states that they use the
published resource under their Apple Developer Program access. This is project
context, not a substitute for the required human legal review before release.

## Engineering rules

- Use pnpm only.
- Keep behavior in official shadcn/Base UI components.
- Do not hand-edit generated files in `apps/showcase/src/components/ui` unless
  an upstream compatibility fix is documented.
- Do not add Apple fonts, symbols, artwork, templates, design-resource exports,
  native reference screenshots, or application screenshots.
- Recreate appearance with original CSS against public `data-slot`, ARIA, and
  Base UI state attributes. Do not trace or package source assets.
- Scope product CSS under `html[data-macos-style="27"]` and preserve
  `data-macos-unstyled` subtree opt-outs.
- Consumer CSS loaded after `macos.css` must win without `!important`.
- Keep the same CSS for browser, Electron, and Tauri; host integrations are docs
  and smoke fixtures, not alternate component implementations.
- Make surgical changes. Do not refactor generated upstream source incidentally.

## Next implementation slice

1. Extract and document the Figma reference values after MCP access is verified.
2. Implement token layers and component-family selectors in `macos.css`.
3. Replace the starter Vite page with lazy React Router routes for `/`, `/all`,
   `/components/:slug`, `/tokens`, `/conformance`, and `/hosts`.
4. Put the concise install flow and one-click agent prompt on the landing page.
5. Generate coverage from the fixture, then add registry, install, build,
   accessibility, and host checks.
6. Run `pnpm verify` before claiming the implementation is complete.

The partial checkpoint may be checked with `pnpm registry:validate`,
`pnpm --filter showcase typecheck`, and `pnpm --filter showcase build`.
