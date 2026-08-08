# Upstream snapshot

Generated on 2026-08-08.

| Dependency or tool | Resolved value |
| --- | --- |
| shadcn CLI | 4.16.2 |
| shadcn style | `base-rhea` |
| shadcn preset | `b27GcrRo` |
| Base UI | 1.7.0 range; exact lockfile version is authoritative |
| React | 19.2.6 range; exact lockfile version is authoritative |
| Tailwind CSS | v4 |
| Icon library | Lucide |
| Node | 25.6.0 |
| pnpm | 10.28.2 |
| Host macOS | 26.5.2 (25F84) |
| Xcode | 26.6 (17F113) |
| Installed macOS SDK | 26.5 |
| Target design generation | macOS 27 |

Apple's public developer releases list macOS 27 and Xcode 27 betas. The local
native oracle is unavailable only because this host has not installed Xcode 27;
it does not mean the target generation is unpublished. Installing beta tooling
is intentionally outside this checkpoint.

The current official CLI installed 61 UI source modules plus the seeded Button, for 61 distinct component files total. Rhea/Base UI remains the provisional baseline because it is the denser current official style. A measured Rhea-versus-Luma decision is blocked until the macOS 27 reference harness runs with Xcode 27.

Commands captured during bootstrap:

```sh
pnpm dlx shadcn@latest --version
pnpm dlx shadcn@latest init --help
pnpm dlx shadcn@latest add --help
pnpm dlx shadcn@latest docs --help
pnpm dlx shadcn@latest registry --help
pnpm dlx shadcn@latest init --name showcase --template vite --base base --preset rhea --no-monorepo --yes
pnpm dlx shadcn@latest info --json
pnpm dlx shadcn@latest preset resolve --json
pnpm dlx shadcn@latest add --all --yes
```

## Generated-source normalization

The 4.16.2 `scroll-area` output included an unused `React` namespace import.
The fixture removes that import so its strict TypeScript production build
passes. No component behavior, markup, styling, or public API was changed.

The showcase ESLint config also scopes two exceptions to generated fixture
files: mixed component/variant exports are allowed under
`react-refresh/only-export-components`, and the upstream carousel/mobile-query
subscription effects are exempt from `react-hooks/set-state-in-effect`. Authored
showcase routes and product code keep the full ruleset.
