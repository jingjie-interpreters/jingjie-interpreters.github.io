# Design Specification

## Visual Concept
Terminal / ASCII-art aesthetics fused with subtle noise-art texture. Minimalist, avant-garde, functional beauty.

## Color Palette

| Role | Color | Hex |
|------|-------|-----|
| Background | Dark gray | `#303030` |
| Primary text | Light gray | `#D4D4D4` |
| Secondary text | Muted gray | `#A0A0A0` |
| Accent / Borders | Mid gray | `#666666` |
| Error text | Red | `#FF5555` |
| Success / Highlight | Green | `#50FA7B` |
| Input background | Darker gray | `#252525` |
| Button background | Charcoal | `#444444` |
| Button hover | Lighter charcoal | `#555555` |

## Typography
```css
font-family: "Courier New", "Consolas", "Monaco", "Liberation Mono", monospace;
```

| Element | Size | Weight | Color |
|---------|------|--------|-------|
| Body text | 14px | 400 | `#D4D4D4` |
| Headings (section titles) | 16px | 700 | `#E0E0E0` |
| Error messages | 12px | 400 | `#FF5555` |
| Button text | 14px | 700 | `#D4D4D4` |
| Input text | 14px | 400 | `#D4D4D4` |
| Placeholder | 14px | 400 | `#888888` |

## Layout & Spacing

### Width Constraints
- Stream container: `max-width: 800px`, centered
- Input area: same max-width as stream container
- Info section: same max-width as stream container
- Page padding: `20px` on mobile, `40px` on desktop

### Vertical Spacing
- Stream container → Input area: `16px`
- Input area → Info section: `40px`
- Between info items: `24px`
- Section internal padding: `16px`

### 16:9 Container
```css
.twitch-container {
  width: 100%;
  max-width: 800px;
  aspect-ratio: 16 / 9;
  position: relative;
  overflow: hidden;
}
```

## Noise Texture
CSS-only implementation using SVG filter applied via `::before` pseudo-element on `<body>`:
```css
body::before {
  content: "";
  position: fixed;
  top: 0; left: 0;
  width: 100%; height: 100%;
  opacity: 0.03;
  pointer-events: none;
  z-index: 9999;
  background-image: url("data:image/svg+xml,..."); /* SVG noise */
}
```
The noise is extremely subtle (3% opacity) — provides texture without distracting from content.

## Expandable Sections (`<details>` / `<summary>`)
- Custom disclosure marker: `▸` (collapsed) / `▾` (expanded) via `::marker` or `list-style`
- Summary text: monospace, uppercase, 14px, color `#E0E0E0`
- Content padding: `16px` left indent from summary
- Border: subtle left border `1px solid #555` on expanded content

## Buttons
- Background: `#444444`
- Border: `1px solid #666666`
- Padding: `8px 20px`
- Hover: background `#555555`
- Disabled: opacity `0.5`, cursor `not-allowed`
- Transition: `0.15s ease` on background-color

## Text Input
- Background: `#252525`
- Border: `1px solid #555555`
- Padding: `8px 12px`
- Focus border: `#888888`
- Placeholder color: `#888888`

## Responsive Breakpoints
| Breakpoint | Behavior |
|------------|----------|
| < 480px | Full-width containers, reduced padding (12px) |
| 480px - 768px | Containers at 95% width |
| > 768px | Containers capped at 800px, comfortable padding |

## Image Display
- Cover image: responsive `max-width: 100%`, centered
- Expandable section images: `max-width: 100%`, constrained to content area
- All images: `display: block`, `margin: 0 auto`
