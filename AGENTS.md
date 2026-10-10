# AGENTS.md — EMV Home Assistant Theme

## Project overview

EMV Theme is a lightweight, standalone Home Assistant theme,
distributed through HACS.

Repository:
https://github.com/emarvegt/ha-theme-emv

The theme originated from UI Lovelace Minimalist but is maintained
independently. It must remain a standalone theme rather than becoming
a custom Home Assistant integration.

The primary purpose is to provide a clean, compact, responsive
interface for a household Home Assistant installation.

## Project structure

- `themes/emv.yaml` — Main theme definition
- `hacs.json` — HACS repository metadata
- `README.md` — Documentation

Keep the repository structure minimal.

Do not introduce build systems, frameworks, package managers, or
additional runtime dependencies unless explicitly requested.

## Core principles

### 1. Performance first

The dashboard runs continuously on a dedicated Android touchscreen
with limited processing resources.

Prioritize:
- Minimal frontend resource consumption
- Low memory usage
- Fast initial rendering
- Smooth scrolling and interaction
- Minimal unnecessary updates and reflows

Avoid:
- Additional JavaScript
- Custom frontend components
- DOM manipulation
- Polling or timers
- Unnecessary animations
- Expensive CSS effects
- Excessive CSS selectors

Prefer static CSS variables and native Home Assistant functionality.

Do not introduce card-mod or other custom dependencies to solve
problems that can be addressed natively.

### 2. Native Home Assistant functionality

Prefer solutions in this order:

1. Native Home Assistant theme variables
2. Native Lovelace layout and configuration options
3. Existing Home Assistant functionality
4. External/custom solutions, only when explicitly approved

Avoid solutions that rely on undocumented internal CSS selectors,
Shadow DOM traversal, or fragile implementation details.

Never assume that a CSS variable exists or is supported.
Verify it against Home Assistant frontend source or documentation.

Clearly distinguish between:
- Officially supported configuration
- Undocumented but functional behavior
- Experimental workarounds

### 3. Responsive design

The primary dashboard, "Scherm", is used on:

- A dedicated portrait-oriented Full HD (1080×1920) touchscreen
- Mobile phones with varying viewport widths

The design must work well on both.

Desired behavior:

**Dedicated touchscreen**
- Three sections (Klimaat, Licht, Auto) side by side
- Compact spacing between sections
- Consistent card widths and alignment
- Efficient use of available screen space

**Mobile**
- Sections stack vertically
- Cards occupy the available width
- No unnecessarily narrow cards
- No horizontal scrolling
- Touch controls remain comfortable to use

Important:
Physical screen resolution is not necessarily the CSS viewport size.
Account for browser scaling, device pixel ratio, and viewport width.

Prefer responsive layouts that adapt automatically rather than
device-specific hardcoded configurations.

Avoid duplicating cards for different screen sizes.

### 4. Theme scope

This repository controls theme styling, not the dashboard's
Lovelace configuration.

The theme can influence:
- Colors
- Typography
- Spacing
- Borders
- Shadows
- Supported layout variables
- Light and dark appearances

It cannot arbitrarily change Home Assistant's layout algorithms
or individual card configurations.

Do not claim that theme variables can solve problems outside
their actual scope.

When a requested change requires modifying dashboard YAML,
explain the required change rather than implementing a fragile
theme workaround.

### 5. Maintainability

Keep changes small, targeted, and easy to understand.

- Preserve the existing `emv` theme identifier.
- Preserve existing colors and appearance unless requested.
- Maintain both light and dark themes.
- Avoid duplicate configuration.
- Group related variables logically.
- Add comments for non-obvious settings.
- Preserve compatibility with HACS.

When adjusting existing values, modify the original declaration
rather than introducing duplicate YAML keys.

Do not introduce configuration solely for speculative future use.

### 6. Dependencies

The intended theme has no additional runtime dependencies.

Some legacy `card-mod` configuration remains from the original
UI Lovelace Minimalist theme.

Treat this as legacy configuration, not a dependency to expand.

Do not add new card-mod functionality.

When removing legacy configuration:
- Verify that the functionality is genuinely obsolete.
- Identify any resulting visual changes.
- Preserve existing behavior where possible.

### 7. HACS compatibility

The repository is installed as a HACS Theme.

Maintain:
- The `themes/` directory
- Valid theme YAML
- The `hacs.json` manifest
- The `emv` theme identifier

Do not convert the repository into a HACS Integration.

Do not introduce release packaging or build steps unless required.

### 8. Validation

Before completing changes:

1. Check YAML syntax.
2. Ensure the root theme identifier remains `emv`.
3. Check for duplicate YAML keys.
4. Verify that referenced theme variables are valid.
5. Confirm that light and dark mode remain functional.
6. Check that HACS repository structure is preserved.
7. Consider desktop touchscreen and mobile behavior.
8. Check whether changes introduce additional runtime dependencies.

If a change affects responsive layout, explain the expected
behavior at narrow and wide viewport widths.

Do not claim that a visual change has been tested unless it
has actually been tested in a browser or Home Assistant instance.

Static validation alone does not prove visual correctness.

### 9. Research and verification

For questions involving Home Assistant frontend behavior:

- Consult current official Home Assistant documentation.
- Inspect Home Assistant frontend source when necessary.
- Prefer the behavior of the installed Home Assistant version.
- Do not rely on outdated community examples without verification.

Home Assistant frontend implementation details can change.

When uncertain, investigate rather than guessing.

### 10. Working practices

For each requested change:

1. Inspect the existing implementation.
2. Identify the simplest viable solution.
3. Prefer modifying existing variables over adding new mechanisms.
4. Implement only the requested changes.
5. Validate the result.
6. Summarize what changed and why.

Avoid unrelated refactoring.

Do not silently change visual styling outside the requested scope.

If multiple solutions exist, prefer the one with:
- Fewer dependencies
- Lower runtime overhead
- Less configuration duplication
- Better compatibility with Home Assistant updates
- Simpler long-term maintenance

## Guiding principle

The theme should remain as close as possible to native Home Assistant.

Every addition should justify its complexity and runtime cost.

Simple, maintainable solutions are preferred over clever workarounds.