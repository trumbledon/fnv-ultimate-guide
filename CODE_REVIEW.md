# Code Review

## Summary
The single-page Fallout: New Vegas guide is visually rich and content-heavy. A few structural and accessibility changes would make it more maintainable and performant without altering the authored content.

## Recommendations

1. **Extract CSS and JavaScript into external assets for caching and maintainability.**
   The page inlines several hundred lines of CSS and the entire interaction script inside the HTML. Moving the style block and script into separate files would let browsers cache them, shrink the initial HTML, and make future edits safer (e.g., avoid accidental changes to content).【F:index.html†L8-L956】【F:index.html†L2546-L2643】

2. **Reduce scroll-handler work for the table of contents.**
   The current scroll listener walks every section on each scroll event and recalculates bounding boxes, which can be costly on long documents. Precomputing section offsets once (and updating on resize) or switching to `IntersectionObserver` for the active-link highlight would reduce layout thrash and improve scroll performance on lower-power devices.【F:index.html†L2548-L2593】

3. **Expose the theme toggle state to assistive tech.**
   The theme toggle button lacks an explicit pressed state, so screen readers cannot announce whether dark mode is active. Consider adding `aria-pressed` and updating it when the theme changes to advertise the current mode and improve keyboard accessibility cues.【F:index.html†L1016-L1019】【F:index.html†L2611-L2640】
