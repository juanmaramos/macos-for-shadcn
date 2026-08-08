# Build Brief: macOS for shadcn

> This document is the complete handoff for a new coding task. Treat it as the only project context. Execute it end to end in a new repository. Do not modify the repository in which this file was supplied.

## 1. Outcome

Create **macOS for shadcn**, a desktop-first, shadcn-compatible style registry that makes current official shadcn components closely resemble the latest public macOS design direction while preserving the components' existing React APIs and Base UI behavior.

The first release is deliberately a **style layer, not a replacement component library**:

- Consumers continue to install and import ordinary official shadcn components.
- The project installs one comprehensive CSS layer and semantic tokens through the shadcn registry.
- Existing shadcn props, variants, composition, keyboard behavior, focus management, selection models, menus, dialogs, and portals remain owned by shadcn and Base UI.
- The CSS layer covers the current official shadcn catalogue and its visible states.
- Components that have no official shadcn equivalent are documented for later registry items; they are not a reason to delay the style release.
- The same React components and CSS must run in a browser, Electron, and Tauri. No platform adapter packages are needed for v0.1.

The internal visual bar is: **within the supported in-window component surface and controlled test conditions, a normal screenshot should be difficult to distinguish from a current macOS app**. The public promise must be more precise because a WebView cannot reproduce every native behavior or optical effect.

## 2. Name and positioning decision

Use these working names:

| Purpose | Name |
|---|---|
| Public project title | **macOS for shadcn** |
| Repository slug | `macos-for-shadcn` |
| Canonical repository | [`juanmaramos/macos-for-shadcn`](https://github.com/juanmaramos/macos-for-shadcn) |
| Local folder | a new sibling folder named `macos-for-shadcn` |
| Stable registry item | `macos` |
| Versioned registry item | `macos-27` |
| Consumer CSS file | `macos.css` |

Do **not** use `shadcn-apple-hig`. It is harder to say, uses two third-party marks as though the project were official, and implies Apple has certified the result. `macos-for-shadcn` is descriptive, searchable, and makes the relationship clearer.

The user reserved the public GitHub repository [`juanmaramos/macos-for-shadcn`](https://github.com/juanmaramos/macos-for-shadcn). It was verified on 2026-08-08 as public and empty, with no default branch yet. A point-in-time npm check found no exact package named `macos-for-shadcn`. These checks are not trademark clearance or legal advice. Recheck relevant trademark databases before public launch. The project does not need an npm package for v0.1.

Use this public description:

> A desktop-first macOS style for shadcn components, measured against current macOS reference controls and designed for React apps on the web, Electron, and Tauri.

Place this notice prominently in the README and showcase footer:

> macOS for shadcn is an independent open-source project. It is not affiliated with, endorsed by, or sponsored by Apple Inc. or the shadcn project. It includes no Apple fonts, symbols, artwork, templates, or application screenshots.

Do not use these phrases in public copy: “Apple UI,” “native components,” “pixel-perfect,” “indistinguishable,” “HIG compliant,” or “Apple certified.” It is acceptable to say “macOS-inspired,” “based on current macOS design conventions,” and to publish measured fidelity results with documented deviations.

## 3. Fixed product decisions

Do not reopen these choices unless implementation evidence proves one impossible:

1. **Start from current official shadcn, not a fork of its Git repository.** Install shadcn-owned component source into fixtures using the current CLI, just as consumers do.
2. **Base UI is the v0.1 primitive target.** It is the current shadcn default and matches the intended app stack. Radix and React Aria support can follow after the Base UI selector contract is stable.
3. **Use one CSS implementation on web, Electron, and Tauri.** Host-specific documentation may enable transparent/vibrant windows, but the component stylesheet must not branch by user agent or require runtime adapters.
4. **Use official shadcn behavior unchanged.** Do not rebuild menus, selection, keyboard navigation, table behavior, focus traps, or dialog behavior in v0.1.
5. **Style every current official component before adding missing macOS-specific components.** A source-discovered coverage manifest defines “every”; do not rely on a stale handwritten list.
6. **Use the canonical GitHub repository as the primary shadcn registry.** A user installs with `pnpm dlx shadcn@latest add juanmaramos/macos-for-shadcn/macos#<tag-or-sha>`.
7. **No runtime React package for the core style.** The installed code belongs to the consumer, consistent with shadcn.
8. **No separate documentation repository and no Storybook.** Keep the registry, showcase, reference harness, docs, and tests together. Build a small Vite showcase with an all-components route.
9. **Target the latest macOS design generation only.** At the date of this brief that is macOS 27. Keep the stable `macos` item on the latest generation and offer `macos-27` plus Git tags for reproducibility.
10. **Zero Apple-owned bytes in the repository.** See the legal rules below.

## 4. What “style-only” does and does not mean

The implementation should be predominantly CSS because official shadcn already supplies the behavior the first release needs. Style these existing contracts:

- semantic shadcn variables;
- `data-slot` elements;
- Base UI state attributes;
- ARIA states;
- shadcn `data-variant` and `data-size` attributes where present;
- normal pseudo-classes such as hover, active, focus-visible, disabled, and placeholder;
- documented context selectors such as a control inside a toolbar, sidebar, menu, or dialog.

CSS is expected to change typography, density, control heights, radii, borders, fills, shadows, translucency, selected/pressed/hover states, focus rings, separators, and motion.

CSS must **not** pretend to turn a DOM dialog into a real window-attached sheet, make a popup escape the host window, expose AppKit accessibility roles, sample the desktop behind a browser window, or reproduce synchronous AppKit live resizing. Those are host/native capabilities, not component styling. Document them as fidelity ceilings; do not build bridges in v0.1.

If a current shadcn component cannot reach the intended appearance without changing its TSX:

1. Prove the limitation in the showcase.
2. Record it in `docs/deviations.md` and `coverage/components.json`.
3. Prefer a narrowly scoped CSS selector or a consumer annotation.
4. Do not silently fork or overwrite the official component in the stable `macos` registry item.
5. Propose a separate optional registry item only after the core style is complete.

## 5. Sources of truth

Use this order of authority:

1. **Running macOS 27 standard controls** created in the local AppKit/SwiftUI reference harness. This is the visual oracle for measurable geometry and states.
2. **Official Apple Human Interface Guidelines**, especially macOS, materials, color, typography, layout, controls, menus, sidebars, toolbars, windows, and accessibility.
3. **Official Apple Design Resources for macOS 27**, consulted locally under their license only. Never commit or redistribute them.
4. **Official Apple developer documentation and WWDC sessions**, especially AppKit control APIs and current Liquid Glass guidance.
5. **Official current shadcn source, CLI output, component docs, registry schemas, Luma, and Rhea.** This is the source of truth for component props and DOM contracts.
6. Third-party libraries and agent skills only as inspiration or checklists. Never treat them as authoritative measurements.

Required starting links, last checked 2026-08-08:

- [Apple Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/)
- [Apple HIG: Materials](https://developer.apple.com/design/human-interface-guidelines/materials)
- [Apple Design Resources: macOS 27](https://developer.apple.com/design/resources/)
- [Apple macOS resources](https://developer.apple.com/macos/resources/)
- [WWDC26: Modernize your AppKit app](https://developer.apple.com/videos/play/wwdc2026/289/)
- [Apple Design Resources license](https://developer.apple.com/support/downloads/terms/apple-design-resources/Apple-Design-Resources-License-20230621-English.pdf)
- [shadcn CLI](https://ui.shadcn.com/docs/cli)
- [shadcn registry](https://ui.shadcn.com/docs/registry)
- [shadcn GitHub registries](https://ui.shadcn.com/docs/registry/github)
- [shadcn registry examples](https://ui.shadcn.com/docs/registry/examples)
- [shadcn Luma](https://ui.shadcn.com/docs/changelog/2026-03-luma)
- [shadcn Rhea](https://ui.shadcn.com/docs/changelog/2026-05-rhea)
- [shadcn Base UI default announcement](https://ui.shadcn.com/docs/changelog/2026-07-base-ui-default)
- [Third-party Apple design skills](https://github.com/rshankras/claude-code-apple-skills/tree/main/skills/design), supplementary only

Do not scrape the HIG into the repository. The HIG provides principles and semantic usage, not a complete public CSS specification. Read and paraphrase it, then derive measurable tokens from standard controls rendered by the reference harness. Record provenance without reproducing Apple text.

If Apple or shadcn has advanced beyond the versions named here when implementation begins, use the latest public release, record the new target in `docs/upstream.md`, and keep the architecture and acceptance tests unchanged.

## 6. Legal and asset rules

These rules are release blockers:

- Do not commit, package, embed, base64-encode, trace, or export SF Pro.
- Use `system-ui`, `-apple-system`, `BlinkMacSystemFont`, and normal platform fallbacks. macOS will supply its system font at runtime.
- Do not commit, package, export, or trace SF Symbols. Use the current shadcn-selected icon library, preferably Lucide unless the fixture already uses another supported library.
- Do not commit Apple Design Resource files, extracted assets, screenshots, measurements copied wholesale from templates, or mirrored HIG content.
- Do not use screenshots of Finder, System Settings, Xcode, or other Apple apps in the public README or showcase.
- Reference screenshots generated by our own AppKit/SwiftUI harness must remain local and gitignored. The repository may commit our web implementation screenshots and non-Apple diff reports that do not embed the native images.
- Add `docs/provenance.md` describing whether each token family is based on public semantic guidance, observation of running standard controls, or an explicit approximation.
- Add the non-affiliation notice and have a human perform legal review before public launch.

## 7. Repository isolation and bootstrap

The task begins in an unrelated existing repository. Keep it untouched.

1. Resolve the current repository’s absolute parent directory.
2. The canonical remote already exists at `https://github.com/juanmaramos/macos-for-shadcn.git` and is the only authorized destination for this work.
3. If the sibling target `<parent>/macos-for-shadcn` does not exist, clone the canonical remote into it.
4. If the target exists, verify that it is a Git repository whose `origin` resolves to the canonical remote. If it contains unrelated changes, points elsewhere, or is not a Git repository, stop and ask before changing it. Do not delete or overwrite anything.
5. Recheck remote metadata before starting. It was public and empty with no default branch on 2026-08-08; do not assume it stayed empty.
6. Perform every subsequent command inside that sibling checkout. Do not modify the repository from which this brief was supplied.
7. Use `pnpm` only. Do not use npm or yarn.
8. Execution of this brief authorizes pushing the verified initial implementation to this specific canonical repository. Because it starts empty, use `main` for the initial history unless the remote has gained a different default branch. Do not push to any other remote.
9. Do not create a GitHub release, deploy a site, publish a package, reserve a domain, or transfer/change repository settings without separate authorization.
10. Do not copy application code from the original repository.

At bootstrap, record exact versions rather than trusting this brief:

```sh
pnpm dlx shadcn@latest --version
pnpm dlx shadcn@latest init --help
pnpm dlx shadcn@latest add --help
pnpm dlx shadcn@latest docs --help
pnpm dlx shadcn@latest registry --help
```

Create the Vite/Base UI fixture using supported current CLI flags, then capture:

```sh
pnpm dlx shadcn@latest info --json
pnpm dlx shadcn@latest preset resolve --json
pnpm dlx shadcn@latest add --all --yes
```

If any command has changed, use `--help` and official docs, then write the actual commands and resolved versions to `docs/upstream.md`. Pin dependencies in `pnpm-lock.yaml`; do not pin the prose command `@latest` as though it were reproducible.

## 8. Target repository shape

Keep the workspace small and legible:

```text
macos-for-shadcn/
├── .github/workflows/ci.yml
├── .gitignore
├── AGENTS.md
├── LICENSE
├── README.md
├── package.json
├── pnpm-lock.yaml
├── pnpm-workspace.yaml
├── registry.json
├── registry/
│   └── styles/
│       └── macos.css
├── apps/
│   └── showcase/                 # Vite + React + TypeScript + Tailwind v4
│       ├── components.json       # Base UI; provisional Rhea baseline
│       └── src/
├── coverage/
│   ├── components.json           # upstream component/slot/state coverage
│   └── waivers.json              # reviewed deviations only
├── docs/
│   ├── architecture.md
│   ├── customization.md
│   ├── deviations.md
│   ├── electron.md
│   ├── provenance.md
│   ├── tauri.md
│   ├── updating.md
│   └── upstream.md
├── evals/
│   ├── README.md
│   ├── matrix.json
│   └── results/                  # reports; native reference images ignored
├── examples/
│   ├── electron-smoke/
│   └── tauri-smoke/
├── reference/
│   └── macos-controls/           # minimal Swift/AppKit reference harness
├── scripts/
│   ├── check-coverage.ts
│   ├── check-registry-install.ts
│   ├── collect-upstream.ts
│   └── generate-eval-report.ts
└── tests/
    ├── accessibility/
    ├── contract/
    ├── install/
    └── visual/
```

Avoid Turborepo unless the workspace demonstrably needs it. pnpm workspaces are enough. Avoid a custom documentation framework; the showcase and Markdown files are the docs.

## 9. Distribution and consumer experience

Implement a valid root `registry.json` using the current official schema. It must expose:

- `macos`: the latest supported macOS design generation;
- `macos-27`: the same v0.1 source under an explicit generation name.

Both are `registry:style` items that extend current shadcn rather than `extends: none`. They install `registry/styles/macos.css` at a predictable project-relative target and add the required import to the consumer’s configured global CSS using supported registry fields. Validate the exact schema with the current CLI; do not invent fields.

The desired published flow is:

```sh
# Existing shadcn project
pnpm dlx shadcn@latest add juanmaramos/macos-for-shadcn/macos#<release-tag-or-sha>

# Continue using official shadcn normally
pnpm dlx shadcn@latest add button dialog table sidebar
```

Then the consumer opts in at the application root:

```tsx
<html data-macos-style="27">
```

The README must show `--dry-run`, `--diff`, and pinned tag/SHA installation before the unpinned convenience command.

Do not overwrite `components/ui/*.tsx` in the core style item. Prove in an install test that applying the registry item to an existing project does not change official shadcn component source.

Third-party shadcn-style components, such as a community Dock, may inherit the semantic palette automatically. They are not part of the v0.1 coverage promise. Add a short compatibility guide explaining that third-party components should expose stable `data-slot` attributes and use shadcn semantic variables; component-specific selectors can be added later after license review.

## 10. CSS engineering contract

`registry/styles/macos.css` is the product. Keep it human-readable and divided by comments into tokens, base rules, materials, states, component families, motion, accessibility preferences, and opt-outs.

### Scope and cascade

- Scope product selectors under `html[data-macos-style="27"]`.
- Use shadcn `data-slot` and public state attributes; never target minified/generated class names or deep internal DOM positions when a slot exists.
- Use `:where()` when helpful to control specificity.
- Load the style after the consumer’s shadcn/Tailwind base so it can change the generated component baseline.
- Preserve consumer layout classes and ordinary composition. Add visual overrides only where necessary.
- Consumer CSS loaded after `macos.css` must win without requiring `!important`.
- Do not use `!important` except for a documented, tested browser accessibility workaround.
- Support an opt-out on any component subtree with `data-macos-unstyled`; ensure both the marked element and descendant slots are excluded.
- Test the cascade against components installed before and after the style.

### Token layers

Expose documented semantic custom properties, at minimum:

- system and fallback font stacks;
- font sizes, line heights, and weights by control/text role;
- application, content, sidebar, toolbar, popover, menu, and overlay surfaces;
- primary, secondary, tertiary, disabled, placeholder, and inverse labels;
- accent, selected content, destructive, warning, success, focus, separator, and border colors;
- control sizes, horizontal padding, icon sizes, radii, and concentric inset relationships;
- elevation and border-highlight recipes;
- material blur, saturation, tint, opacity, specular highlight, and darkened-edge values;
- motion duration, spring/easing approximations, and pressed-state scale/translation;
- active and inactive window state values.

Use `oklch()` where it improves interpolation and theme consistency, with tested fallbacks only if current supported browsers require them.

Provide two customization tiers:

1. **Brand-safe variables**: accent, canvas/content color, optional sidebar tint, and glass opacity. These keep the default geometry and state grammar.
2. **Advanced variables**: control size, radii, shadows, material strength, and motion. Document that changing them intentionally departs from the measured macOS reference.

The browser cannot read the user’s system accent or macOS 27 Liquid Glass opacity setting. Use a documented default and let the app set variables. Do not claim automatic system matching.

### Materials

Do not put glass on everything. Follow Apple’s semantic hierarchy:

- normal content surfaces remain primarily opaque or standard-material-like;
- Liquid Glass-like effects belong mainly to navigation and control layers where context warrants them;
- sidebar, toolbar, menu/popover, selected item, and overlay materials have separate tokens;
- controls inside toolbars may differ from the same controls inside content;
- thicker/tinted fallbacks protect contrast over difficult backgrounds.

For web, use in-page `backdrop-filter` with an opaque fallback. This cannot sample wallpaper or other windows behind the browser.

For Electron and Tauri, the same CSS remains unchanged. `docs/electron.md` and `docs/tauri.md` may show optional, version-verified host configuration for transparent/vibrant window backgrounds and real traffic lights. The smoke examples verify those recipes compile. Do not add a host adapter abstraction in v0.1.

### Required state coverage

Where a component supports them, style and demonstrate:

- light and dark appearance;
- default, hover, pressed/active, focus-visible, and disabled;
- valid and invalid;
- open and closed;
- checked, unchecked, selected, and indeterminate;
- destructive, primary/default, secondary, outline, ghost, and link variants;
- every official size;
- active and inactive window appearance through a deterministic harness attribute;
- reduced motion;
- reduced transparency, using the media query where supported plus a documented attribute fallback;
- increased contrast and forced colors without destroying usability;
- long content and truncation;
- RTL wherever the current official shadcn component claims RTL support.

## 11. Discover and lock the current shadcn contract

Do not hardcode an old component list from this brief.

1. Create a clean Base UI fixture using the current official CLI.
2. Install all current official components with `add --all`.
3. Save the exact shadcn CLI version, resolved preset, framework, Tailwind version, Base UI version, icon library, and generation date to `docs/upstream.md` and machine-readable coverage metadata.
4. Inspect installed TSX and official `docs --json` output to collect:
   - component/module name;
   - exported parts;
   - `data-slot` values;
   - variants and sizes;
   - Base UI state attributes and ARIA states;
   - whether the component is visual, structural, behavior-only, or a documentation recipe.
5. Create `coverage/components.json`. Every entry must have one status:
   - `token-covered`;
   - `selector-covered`;
   - `not-visual`;
   - `documented-deviation`.
6. Generate or validate this inventory with `scripts/collect-upstream.ts` and fail CI when installed slots disappear, new slots are unclassified, selectors reference removed slots, or a current official component lacks a showcase story.

Do not assert that every raw `data-state` value needs unique CSS. The coverage record should explain when a shared state token intentionally handles several components.

## 12. Baseline comparison: Luma versus Rhea

Current official shadcn already provides two useful baselines:

- Luma: rounded, softly elevated, macOS Tahoe-inspired geometry without glass;
- Rhea: a denser, more compact Luma intended for focused product interfaces.

Use **Rhea/Base UI provisionally** because macOS desktop applications are information-dense. Before writing broad overrides, render the golden controls below in both Luma and Rhea with otherwise identical settings. Compare control height, padding, radius, typography, and density to the native reference harness. Record the result in `docs/upstream.md`. Keep Rhea unless Luma is measurably closer across the majority of golden controls.

This comparison is a starting-point optimization, not a user-facing dependency. The final CSS must still restyle a normal current Base UI shadcn project when imported.

## 13. Showcase and documentation experience

Build `apps/showcase` as a production-quality Vite app using the actual installed shadcn source and the registry CSS. Do not mock the component DOM.

Required routes:

- `/` — concise product page, install command, current target/version, screenshots, compatibility, and legal notice;
- `/all` — every official visual shadcn component on one scrollable page, comparable to the shadcn/create overview;
- `/components/:slug` — focused component and state matrix;
- `/tokens` — live brand-safe customization controls and copyable CSS variables;
- `/conformance` — generated coverage, visual results, accessibility results, and known deviations;
- `/hosts` — web, Electron, and Tauri expectations and setup links.

The all-components page must include a searchable component index, light/dark switch, active/inactive window switch, transparency controls, reduced-motion toggle, and the default-vs-macOS style comparison. Keep the design restrained and let the components be the subject.

The README must contain:

1. one-sentence value proposition;
2. non-affiliation and zero-Apple-assets notice;
3. 60-second install for an existing shadcn app;
4. reproducible pinned install plus `--dry-run` and `--diff`;
5. before/after images generated from our own showcase only;
6. supported shadcn base and exact tested versions;
7. component coverage table linked to the generated report;
8. brand-safe customization examples;
9. web/Electron/Tauri compatibility matrix;
10. honest known deviations;
11. update policy and how annual macOS updates are handled;
12. development, testing, and contribution instructions;
13. license.

## 14. Native reference harness

Create a minimal local macOS reference app under `reference/macos-controls` using the latest installed stable or beta Xcode SDK that corresponds to the target design generation.

Prefer AppKit standard controls for a desktop target. Use SwiftUI only where it is the current canonical API or materially easier to reproduce the same standard control. Do not custom-draw Apple controls.

The golden reference set is:

| shadcn surface | Native reference concept |
|---|---|
| Button and Button Group | `NSButton` styles and grouped controls |
| Input and Textarea | `NSTextField` and `NSTextView` |
| Checkbox and Radio Group | standard checkbox/radio `NSButton` |
| Switch | `NSSwitch` |
| Slider | `NSSlider` |
| Select and Combobox | `NSPopUpButton` / combo box |
| Tabs and Toggle Group | `NSSegmentedControl` / tab view |
| Progress and Spinner | `NSProgressIndicator` |
| Menu and Context Menu | `NSMenu` |
| Popover and Tooltip | `NSPopover` / help-tag-like presentation |
| Dialog and Alert Dialog | `NSAlert` / sheet presentation |
| Sidebar and Resizable | split view with a source-list-like sidebar |
| Table | `NSTableView` |

Render deterministic content and states at a fixed window size, scale, accent configured for the harness, light/dark appearance, and active/inactive state where possible. Capture local reference images for evaluation, but gitignore them and never publish them.

The native harness is an oracle, not a dependency of the consumer library. If Xcode or the target macOS SDK is unavailable, complete all other work, mark native visual conformance `Incomplete`, and provide the exact command and environment needed to finish it. Do not fabricate native baselines.

## 15. Tests and evals

“Looks good” is not a test. Implement the following layers and make `pnpm verify` run every non-interactive gate that the current host can support.

### A. Static quality

- TypeScript strict mode with no `any` and no unjustified type assertions.
- ESLint or the current scaffold’s equivalent.
- CSS linting for invalid declarations, duplicate selectors, forbidden Apple asset/font names, unexpected URLs/data URIs, and `!important`.
- `pnpm build` for the showcase.
- Registry schema validation and registry build using the current shadcn CLI.

### B. Contract and coverage tests

- Verify every installed official component is classified in `coverage/components.json`.
- Verify every discovered `data-slot` is classified.
- Verify every selector-owned slot exists upstream.
- Verify every visual component has at least one showcase story.
- Verify all waivers contain a reason, evidence link, owner, and review date.
- Verify no core registry file writes to or overwrites `components/ui/*.tsx`.
- Snapshot exact upstream metadata so scheduled drift checks produce a reviewable diff.

### C. Consumer installation tests

In disposable temporary directories:

1. Create a fresh current Vite + Base UI shadcn app.
2. Create a second existing shadcn app with several components already installed.
3. Build the registry locally and serve its generated JSON/files from a local HTTP server, or use the current CLI-supported local registry path.
4. Run `shadcn add` with `--dry-run` first, then install the local `macos` item.
5. Confirm the CSS lands at the documented target and the global import is correct.
6. Confirm checksums of pre-existing official component TSX files are unchanged.
7. Add another official component after installing the style and confirm it inherits the style without another migration.
8. Build and run both fixtures.

After local verification passes, push the commit to the already-authorized canonical remote and repeat the install test against `juanmaramos/macos-for-shadcn/macos#<full-commit-sha>`. Do not create a release tag merely to run this test.

### D. Browser interaction and accessibility tests

Use Playwright and axe (or current maintained equivalents):

- Chromium and WebKit are required; Firefox is useful but not a release blocker for the desktop-first v0.1.
- Exercise keyboard navigation supplied by Base UI for dialogs, menus, popovers, tabs, selects, comboboxes, checkboxes, radio groups, sliders, and navigation components.
- Test focus visibility, Escape behavior, open/close behavior, disabled controls, invalid fields, and portal surfaces.
- Run automated accessibility scans for every component route in light and dark modes.
- Test forced colors, reduced motion, reduced transparency fallback, zoom at 200%, and keyboard-only operation.
- Treat WCAG-correct web accessibility as the goal. Do not claim VoiceOver output matches AppKit.

### E. Visual regression tests

Use Playwright screenshots at fixed viewport, device scale factor, fonts, locale, animations, dates, random seed, and reduced-motion settings.

Required matrix:

- Chromium and WebKit;
- light and dark;
- styled and default-shadcn comparison;
- component default plus interaction snapshots for hover, pressed, focus, open, selected/checked, invalid, and disabled where relevant;
- active and inactive window simulation;
- clear, default, and strongly tinted glass opacity values;
- normal and reduced transparency;
- all official sizes/variants;
- long content and RTL for supported components.

Commit implementation baselines from the showcase. Do not commit Apple/native baselines.

For native comparison, generate a local HTML report containing paired views and numeric results without embedding native images in a committed artifact. Mask text regions for strict pixel-diff because Electron/Chromium and AppKit use different text rasterizers. Evaluate geometry and non-text rendering separately from typography.

Do not choose arbitrary pass thresholds and then declare victory. During the golden-control calibration:

1. measure the inherent run-to-run noise of identical captures;
2. record browser-versus-browser and native-versus-web text rasterization deltas;
3. set thresholds slightly above measured noise;
4. store thresholds and rationale in `evals/matrix.json`;
5. require human review for the golden-control reference comparison.

Track at least:

- non-text differing-pixel percentage;
- SSIM or an equivalent perceptual score;
- bounding-box deltas for height, width, radius, padding, and alignment;
- contrast ratios;
- motion duration/curve deltas from frame capture where practical;
- pass, fail, skipped, and blocked counts by component and host.

### F. Electron and Tauri smoke tests

Create the smallest examples that render the built showcase or a golden control page.

- Electron: compile/package smoke test on macOS and launch smoke where CI permits.
- Tauri: `cargo check`/build smoke on macOS and launch smoke where CI permits.
- Both examples import the exact same `macos.css`; there is no forked host stylesheet.
- Verify optional transparent/vibrant host settings with current official documentation, and keep them optional.
- Capture one local screenshot from each host for the uncommitted eval report.
- Record that web uses only in-page backdrop filtering, Electron may have Skia text differences, and Tauri’s WKWebView is generally closer to Safari/Core Text.

### G. Evals report

`pnpm eval` must produce `evals/results/<run-id>/report.html` and `summary.json` containing:

- exact OS, Xcode/SDK, Node, pnpm, shadcn, Base UI, Tailwind, React, browser, Electron, and Tauri versions;
- commit SHA or `dirty` status;
- target design generation;
- coverage totals;
- commands run and exit status;
- visual and accessibility results;
- registry install evidence;
- known deviations and blocked gates;
- links to local screenshots/reports where safe;
- final verdict: `Passed`, `Incomplete`, or `Failed`.

Use `Passed` only when every required acceptance criterion below is met. Missing Xcode, unavailable SDKs, or an untested desktop host means `Incomplete`, not `Passed`.

## 16. Suggested scripts

Provide stable workspace commands with these meanings; exact tooling may differ:

```json
{
  "scripts": {
    "dev": "run the showcase",
    "build": "build the showcase and registry",
    "lint": "lint TypeScript and CSS",
    "typecheck": "typecheck all TypeScript",
    "test": "run unit and contract tests",
    "test:coverage": "verify upstream component/slot/story coverage",
    "test:install": "exercise registry installation in disposable apps",
    "test:a11y": "run browser accessibility suites",
    "test:visual": "run implementation screenshot regression",
    "test:hosts": "compile/smoke Electron and Tauri examples",
    "reference:macos": "build and capture the local native oracle",
    "eval": "generate the complete conformance report",
    "verify": "run all required release gates"
  }
}
```

Use maintained tools already present in the chosen scaffold when possible. Do not add abstractions or dependencies for a single trivial script.

## 17. Implementation order

Work in this order and keep the repository runnable after each stage:

1. **Isolate and clone** the canonical repository into the new sibling checkout.
2. **Research and pin** current Apple/shadcn versions and write `docs/upstream.md`.
3. **Scaffold** the pnpm workspace, Vite showcase, registry, tests, and CI.
4. **Install all official shadcn Base UI components** into the showcase fixture.
5. **Generate the contract inventory** and baseline all-components gallery.
6. **Create the native golden-control harness** and capture local references if the SDK is available.
7. **Compare Rhea and Luma**, record the decision, and choose the nearer starting geometry.
8. **Implement tokens first**: typography, semantic colors, geometry, materials, elevation, motion, accessibility preferences.
9. **Style golden controls** and iterate against the reference harness until the calibrated thresholds and human review pass.
10. **Expand CSS across the full official catalogue**, component family by component family, adding every supported state to the gallery.
11. **Implement registry install flow**, customization controls, opt-out, and third-party compatibility guidance.
12. **Add Electron/Tauri smoke examples** using the same CSS.
13. **Run all tests and visual evals**, repair failures, and generate the final report.
14. **Finish README and screenshots** from our implementation.
15. **Commit and push** the verified initial implementation to the default branch selected during bootstrap (`main` while the remote remains empty), then run the pinned-SHA GitHub registry install test. Do not create a release, deploy, or publish an npm package.

Do not stop after scaffolding or a sample Button. Continue until the full v0.1 acceptance criteria are satisfied or a real external blocker prevents them.

## 18. v0.1 acceptance criteria

All of the following are required for `Passed`:

- [ ] Work exists only in a sibling clone of `https://github.com/juanmaramos/macos-for-shadcn.git`; the original repository is untouched.
- [ ] Project uses pnpm, React, TypeScript strict mode, Tailwind v4, current official shadcn, and Base UI.
- [ ] Exact upstream versions and current macOS target are recorded.
- [ ] Root `registry.json` validates and exposes `macos` and `macos-27` as current-schema style items.
- [ ] The registry installs through a local end-to-end CLI test into both fresh and existing shadcn apps.
- [ ] After push, the registry installs from `juanmaramos/macos-for-shadcn/macos#<full-commit-sha>` into a disposable fixture.
- [ ] Installing the style does not rewrite official component TSX source.
- [ ] A component added after the style inherits it.
- [ ] One maintained `registry/styles/macos.css` supplies the core style for web, Electron, and Tauri.
- [ ] CSS is opt-in with `data-macos-style="27"`, supports `data-macos-unstyled`, and exposes documented brand-safe variables.
- [ ] No Apple font, icon, artwork, template, HIG mirror, or Apple-app screenshot exists in tracked files or generated public assets.
- [ ] Every current official visual shadcn component is installed, inventoried, styled or explicitly waived, and represented in the showcase.
- [ ] `/all` displays all official visual components and the required state controls.
- [ ] The golden reference controls are measured against a real local AppKit/SwiftUI harness, or the result is honestly `Incomplete` with exact unblock steps.
- [ ] Light/dark, core interaction states, all official variants/sizes, active/inactive, reduced motion/transparency, contrast, long content, and supported RTL are tested.
- [ ] Chromium and WebKit interaction, accessibility, and screenshot suites pass.
- [ ] Electron and Tauri examples compile against the same CSS; launch checks run where the host permits.
- [ ] `pnpm verify` passes every available release gate.
- [ ] `pnpm eval` generates the versioned HTML and JSON report with an honest verdict.
- [ ] README contains install, customization, compatibility, screenshots, coverage, deviations, update policy, legal notice, and development commands.
- [ ] The verified initial commit is pushed to the canonical repository’s default branch; no release, deployment, npm publication, or unrelated remote change occurs.

## 19. Known fidelity ceilings to document, not hide

These do not invalidate the style product, but they invalidate an absolute native-equivalence claim:

- Web accessibility semantics and VoiceOver announcements differ from AppKit controls.
- DOM menus, tooltips, selects, and popovers cannot render beyond the WebView/window boundary.
- CSS `backdrop-filter` samples in-page content, not arbitrary desktop content behind a window.
- Electron/Chromium text rasterization can differ from AppKit/Core Text.
- WebViews can show asynchronous repaint differences during aggressive live resizing.
- Browsers cannot read Full Keyboard Access, the system accent in a portable way, or the macOS 27 Liquid Glass transparency slider.
- Browser chrome, application menus, Dock behavior, native sheets, file dialogs, and Quick Look are host capabilities.

The first release promises high-fidelity **visual styling of official shadcn’s in-window components**, not replacement of the operating system.

## 20. Future work after v0.1

Do not implement these until the style release passes unless spare time remains and no core criterion is at risk:

- optional Radix and React Aria selector contracts;
- Finder-style `ColumnView`;
- multicolumn hierarchical `OutlineView`;
- functional `PathControl` with middle truncation and file drag/drop;
- toolbar overflow/customization behavior;
- native Electron/Tauri menus, attached sheets, file dialogs, Quick Look, Dock, and menu-bar integrations;
- audited compatibility selectors for community components such as Docks;
- a branded npm package or hosted registry/docs domain.

These belong in separate registry items so the core style remains simple. Before adapting community code, verify its license and copy only when the license permits; otherwise reimplement from public behavior and APIs.

## 21. Annual update process

The project cannot be kept current by scraping CSS because Apple does not publish the system as web CSS. Each WWDC cycle:

1. Open a `next` branch for the new macOS generation.
2. Review official HIG changes, design-resource release notes, framework docs, and relevant WWDC sessions.
3. Render the same native golden-control harness on the new SDK and at representative material/transparency settings.
4. Regenerate the shadcn upstream contract against the current CLI/Base UI.
5. Diff tokens, selectors, component slots, and screenshots.
6. Update the stable `macos` item, add a new versioned item if useful, and retain old behavior through Git tags rather than maintaining many live CSS profiles.
7. Publish a visual migration report, known deviations, and any consumer action required.
8. Run legal/asset checks again before release.

Budget an annual human design/engineering review. Agent skills can accelerate discovery and checklist work, but official Apple docs and running standard controls remain the source of truth.

## 22. Required final handoff from the implementing task

The final response must be concise but evidence-based. Include:

- absolute path to the new repository;
- canonical remote URL;
- current branch and commit SHA;
- what was built;
- exact local-registry and pinned-SHA GitHub install commands that were tested;
- exact commands run and pass/fail results;
- component/slot/story coverage totals;
- links to the README, `macos.css`, showcase, coverage manifest, deviations, and eval report;
- screenshot links from our showcase plus Electron/Tauri if generated;
- honest verdict: `Passed`, `Incomplete`, or `Failed`;
- any external publication step that still requires user authorization.

Do not summarize aspirations as completed work. Completion means the acceptance checklist and evidence exist in the new repository.
