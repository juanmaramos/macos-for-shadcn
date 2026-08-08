# Updating upstream

1. Update the CLI in a review branch and regenerate `pnpm-lock.yaml`.
2. Run `pnpm dlx shadcn@latest info --json` and `preset resolve --json`.
3. Preview every official component change with `add --dry-run` and `--diff`; never overwrite customized source without review.
4. Run `pnpm test:coverage` to detect new, removed, or unclassified slots.
5. Re-run browser tests and the local native reference harness before moving the stable `macos` item.
