# Agent install prompt

Paste this into your coding agent from the root of an existing shadcn project:

```text
Add macOS for shadcn to this project without replacing or rewriting official shadcn component source.

1. Inspect the project with `pnpm dlx shadcn@latest info --json` and confirm it uses Base UI and Tailwind v4.
2. Preview the pinned registry item with `pnpm dlx shadcn@latest add juanmaramos/macos-for-shadcn/macos#<full-commit-sha> --dry-run` and review its diff.
3. Install that same pinned item.
4. Verify `macos.css` was installed next to the configured components directory under `styles/`, and verify the configured global Tailwind CSS file imports it after the existing shadcn imports. Correct only the import path if this project's alias differs from `@/`.
5. Add `data-macos-style="27"` to the application root `<html>` element.
6. Build the app and confirm a newly added official shadcn component inherits the style.
7. Report the files changed and any compatibility limitation. Do not use Apple fonts, symbols, artwork, templates, or screenshots.
```

Replace `<full-commit-sha>` with a verified commit from this repository. The showcase exposes the same prompt with a one-click copy control.
