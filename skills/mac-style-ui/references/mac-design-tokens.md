# Mac Design Tokens (Detailed)

## Color Palette

### Light Mode
| Token | Value | Usage |
|-------|-------|-------|
| `--bg-primary` | `#f5f5f7` | Page background |
| `--bg-secondary` | `#ffffff` | Card, modal, surface |
| `--bg-tertiary` | `#f0f0f2` | Sidebar, inset |
| `--bg-glass` | `rgba(255,255,255,0.7)` | Frosted surfaces |
| `--text-primary` | `#1d1d1f` | Headings, body |
| `--text-secondary` | `#86868b` | Captions, labels |
| `--text-tertiary` | `#aeaeb2` | Placeholder, disabled |
| `--accent` | `#007aff` | Buttons, links, focus |
| `--accent-hover` | `#0056cc` | Hover state |
| `--red` | `#ff3b30` | Destructive, error |
| `--green` | `#34c759` | Success |
| `--orange` | `#ff9500` | Warning |
| `--border` | `rgba(0,0,0,0.06)` | Dividers |
| `--border-strong` | `rgba(0,0,0,0.12)` | Input border |
| `--shadow-sm` | `0 1px 3px rgba(0,0,0,0.08)` | Subtle elevation |
| `--shadow-md` | `0 4px 12px rgba(0,0,0,0.06)` | Cards |
| `--shadow-lg` | `0 8px 30px rgba(0,0,0,0.08)` | Dropdowns |
| `--shadow-xl` | `0 20px 60px rgba(0,0,0,0.12)` | Modals |

### Dark Mode
| Token | Value | Usage |
|-------|-------|-------|
| `--bg-primary` | `#1c1c1e` | Page background |
| `--bg-secondary` | `#2c2c2e` | Card, modal |
| `--bg-tertiary` | `#3a3a3c` | Sidebar |
| `--bg-glass` | `rgba(44,44,46,0.8)` | Frosted surfaces |
| `--text-primary` | `#f5f5f7` | Headings, body |
| `--text-secondary` | `#98989d` | Captions |
| `--text-tertiary` | `#636366` | Placeholder |
| `--accent` | `#0a84ff` | Buttons, links |
| `--accent-hover` | `#409cff` | Hover |
| `--border` | `rgba(255,255,255,0.08)` | Dividers |
| `--border-strong` | `rgba(255,255,255,0.15)` | Input border |

## Typography Scale

```
text-xs:    12px / 1.3
text-sm:    14px / 1.4
text-base:  16px / 1.5
text-lg:    20px / 1.4
text-xl:    24px / 1.3
text-2xl:   32px / 1.2
text-3xl:   48px / 1.15
text-4xl:   64px / 1.1
```

Font weights: 400 (regular), 500 (medium), 600 (semibold), 700 (bold).
SF Pro prefers 590 for "semibold" — use 600 as fallback.

## Frosted Glass Recipe

```css
.glass {
  background: var(--bg-glass);
  backdrop-filter: blur(20px) saturate(180%);
  -webkit-backdrop-filter: blur(20px) saturate(180%);
  border: 1px solid var(--border);
}
```

Variations:
- Light glass: `blur(10px)` for subtle overlays
- Heavy glass: `blur(40px)` for modals
- Dark glass: `rgba(30,30,32,0.85)` backdrop

## Component Specs

### Button Sizes
```
sm: h28, px12, text-sm, radius 6px
md: h36, px16, text-base, radius 8px
lg: h44, px24, text-lg, radius 10px
```

### Input
```
Height: 36px (default), 28px (small), 44px (large)
Padding: 0 12px
Border: 1px solid var(--border-strong)
Radius: 8px
Focus ring: 0 0 0 3px rgba(0,122,255,0.3)
```

### Card Variants
```
Default: white bg, shadow-md, radius 12px, p20
Glass: glass bg, shadow-sm, radius 12px, p20
Interactive: default + hover:shadow-lg, transition 200ms
```

### Sidebar
```
Width: 240px (compact), 260px (default)
Bg: glass or bg-tertiary
Item height: 40px
Item radius: 8px
Item padding: 0 12px
Active item: accent bg at 10% opacity
```

### Modal / Sheet
```
Bg: glass-heavy or bg-secondary
Radius: 16px (top for sheets)
Shadow: shadow-xl
Backdrop: rgba(0,0,0,0.3)
Animation: scale(0.95)->scale(1) + fade, 300ms
```

## CSS Variables Template

```css
:root {
  /* Colors */
  --bg-primary: #f5f5f7;
  --bg-secondary: #ffffff;
  --bg-tertiary: #f0f0f2;
  --bg-glass: rgba(255,255,255,0.7);
  --text-primary: #1d1d1f;
  --text-secondary: #86868b;
  --text-tertiary: #aeaeb2;
  --accent: #007aff;
  --accent-hover: #0056cc;
  --border: rgba(0,0,0,0.06);
  --border-strong: rgba(0,0,0,0.12);
  --red: #ff3b30;
  --green: #34c759;
  --orange: #ff9500;

  /* Shadows */
  --shadow-sm: 0 1px 3px rgba(0,0,0,0.08);
  --shadow-md: 0 4px 12px rgba(0,0,0,0.06);
  --shadow-lg: 0 8px 30px rgba(0,0,0,0.08);
  --shadow-xl: 0 20px 60px rgba(0,0,0,0.12);

  /* Radius */
  --radius-sm: 6px;
  --radius-md: 8px;
  --radius-lg: 12px;
  --radius-xl: 16px;
  --radius-full: 9999px;

  /* Typography */
  --font-sans: -apple-system, BlinkMacSystemFont, "SF Pro Text", "Helvetica Neue", sans-serif;
  --font-display: -apple-system, "SF Pro Display", "Helvetica Neue", sans-serif;
  --font-mono: "SF Mono", "Menlo", "Consolas", monospace;

  /* Spacing (8px grid) */
  --space-xs: 4px;
  --space-sm: 8px;
  --space-md: 16px;
  --space-lg: 24px;
  --space-xl: 32px;
  --space-2xl: 48px;
  --space-3xl: 64px;

  /* Motion */
  --ease-out: cubic-bezier(0.25, 0.1, 0.25, 1);
  --ease-spring: cubic-bezier(0.34, 1.56, 0.64, 1);
  --duration-fast: 150ms;
  --duration-normal: 250ms;
  --duration-slow: 400ms;
}

/* Dark mode */
@media (prefers-color-scheme: dark) {
  :root {
    --bg-primary: #1c1c1e;
    --bg-secondary: #2c2c2e;
    --bg-tertiary: #3a3a3c;
    --bg-glass: rgba(44,44,46,0.8);
    --text-primary: #f5f5f7;
    --text-secondary: #98989d;
    --text-tertiary: #636366;
    --accent: #0a84ff;
    --accent-hover: #409cff;
    --border: rgba(255,255,255,0.08);
    --border-strong: rgba(255,255,255,0.15);
    --shadow-sm: 0 1px 3px rgba(0,0,0,0.3);
    --shadow-md: 0 4px 12px rgba(0,0,0,0.25);
    --shadow-lg: 0 8px 30px rgba(0,0,0,0.3);
    --shadow-xl: 0 20px 60px rgba(0,0,0,0.4);
  }
}
```

## Tailwind Config (alternative)

```js
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
        mac: {
          bg: { primary: '#f5f5f7', secondary: '#ffffff', tertiary: '#f0f0f2' },
          text: { primary: '#1d1d1f', secondary: '#86868b', tertiary: '#aeaeb2' },
          accent: { DEFAULT: '#007aff', hover: '#0056cc' },
          border: { DEFAULT: 'rgba(0,0,0,0.06)', strong: 'rgba(0,0,0,0.12)' }
        }
      },
      fontFamily: {
        sans: ['-apple-system', 'BlinkMacSystemFont', '"SF Pro Text"', '"Helvetica Neue"', 'sans-serif'],
        display: ['-apple-system', '"SF Pro Display"', '"Helvetica Neue"', 'sans-serif'],
        mono: ['"SF Mono"', 'Menlo', 'Consolas', 'monospace']
      },
      borderRadius: { mac: { sm:'6px', md:'8px', lg:'12px', xl:'16px' } },
      boxShadow: {
        'mac-sm': '0 1px 3px rgba(0,0,0,0.08)',
        'mac-md': '0 4px 12px rgba(0,0,0,0.06)',
        'mac-lg': '0 8px 30px rgba(0,0,0,0.08)',
        'mac-xl': '0 20px 60px rgba(0,0,0,0.12)'
      }
    }
  }
};
```
