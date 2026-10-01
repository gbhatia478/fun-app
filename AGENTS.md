# App development preferences

## Prioritize iPhone viewing

The user primarily views this app on an iPhone. Optimize all app design and implementation decisions for the iPhone experience first.

- Build mobile-first layouts that fit narrow iPhone screens without horizontal scrolling or clipped content.
- Keep text readable without zooming and make buttons and other controls easy to tap, with touch targets of at least 44 × 44 CSS pixels.
- Support Safari on iOS, portrait and landscape orientations, safe-area insets, and the changing viewport height caused by browser controls.
- Ensure core interactions work with touch and do not depend on hover.
- When changing the UI, verify representative iPhone viewport widths, including 375, 390, and 430 CSS pixels. Check layout, text wrapping, and touch controls. State when verification uses browser emulation rather than a physical iPhone.
- Preserve a usable desktop layout while treating iPhone usability as the primary design priority.
