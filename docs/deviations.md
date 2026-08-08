# Known deviations

- The macOS 27 native reference comparison is incomplete because Xcode 27 is not installed on the current host.
- Browser overlays cannot render beyond their WebView or window boundary.
- Web backdrop filters sample in-page content, not arbitrary windows or wallpaper behind the host.
- Electron/Chromium and AppKit/Core Text rasterize text differently.
- Web accessibility semantics are tested for WCAG behavior, not identical AppKit VoiceOver announcements.
- Browsers cannot portably read the system accent, Full Keyboard Access, or Liquid Glass transparency setting.
- The current registry import uses the fixture's `@/` alias and the install prompt tells agents to correct only that import when a consumer uses a different alias. A portable global-CSS target placeholder is not available in shadcn 4.16.2.
