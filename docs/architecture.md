# Architecture

The v0.1 product is one opt-in stylesheet distributed as a shadcn `registry:style` item. Official shadcn Base UI source owns behavior; `macos.css` owns tokens and visual state styling through public `data-slot`, ARIA, Base UI state, variant, and size attributes.

The showcase is a real Vite consumer fixture. It imports the same source stylesheet that the registry distributes and uses the official generated components without alternate DOM mocks. Browser, Electron, and Tauri hosts share that CSS; host-specific material configuration remains optional.
