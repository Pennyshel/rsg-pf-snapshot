# RSG UI Kit — Design System Spec

**Source of truth**: [Figma — RSG-Site-Work](https://www.figma.com/design/5WzwBxV2JZTiA3y44ja7t1/RSG-Site-Work?node-id=15-2124)
**Live reference implementation**: `AI Labs Nicolas/Projects/MeetRecorder/src/popup.{html,css}` (Chrome extension popup, dark theme, all button variants used)
**Maintained by**: Marketing / Design team
**Last updated**: 2026-05-12

A portable design-system spec extracted directly from the RSG Figma kit. Use it to integrate consistent visual language into any internal tool (Chrome extensions, Streamlit dashboards, Python GUIs, web apps, Slack integrations, etc.) without re-deriving values from Figma every time.

---

## 1. Quick Start

Three things to copy in this order:

1. **Color tokens** → § 2
2. **Typography scale** → § 3
3. **Button components** → § 4 (paste-ready in CSS, Tailwind, JSON, or SCSS — § 7)

The kit is **theme-agnostic**: same tokens work on light cards (`#F2F2F2 → #EEEEEE` gradient) and dark surfaces (with the `neutral` button variant designed for translucent overlay on dark).

---

## 2. Color Palette

### 2.1 Grey

| Token name | Hex | Usage |
|---|---|---|
| `grey/dark-grey` | `#191919` | Primary text on light backgrounds |
| `grey/deep-grey` | `#333333` | Secondary dark text, end of dark gradient |
| `grey/basic-grey` | `#4C4C4C` | Borders, dividers, disabled text on light |
| `grey/cold-grey` | `#B2B9BF` | Secondary text on dark, neutral icons |
| `grey/middle-grey` | `#D9D9D9` | Subtle backgrounds on light |
| `grey/soft-grey` | `#F2F2F2` | Card backgrounds (top), divider lines |
| `grey/grey-for-text` | `#9D9C9D` | Muted/secondary text on either theme |

### 2.2 Grey Gradients

| Token name | Definition | Usage |
|---|---|---|
| `gradient/soft-grey-gradient-100` | `linear-gradient(0deg, #F2F2F2 0%, #EEEEEE 100%)` | **Card backgrounds** (per Figma annotation) |
| `gradient/dark-grey-gradient-1` | `linear-gradient(180deg, #1D1D1D 0%, #333333 100%)` | Text fill on light "white" buttons (clip to text) |

### 2.3 Red

| Token name | Hex | Usage |
|---|---|---|
| `red/deep-red` | `#92152E` | **Primary button** default state — main brand red |
| `red/branded-red` | `#B61A39` | Hover/highlight state of deep-red, center of red gradients |
| `red/bright-red` | `#F71F20` | Recording indicators, error states, attention dots |
| `red/bright-branded-red` | `#FF1141` (with `rgba(0,0,0,0.2)` overlay) | Vibrant accent for promotional UI |
| `red/pressed` | `#7A0C22` | **Primary button** pressed state |
| `red/glow` (shadow) | `rgba(182, 26, 57, 0.35)` | Hover glow under red buttons |

### 2.4 Red Gradients

| Token name | Definition |
|---|---|
| `red/red-gradient` | `linear-gradient(90deg, #500B19 0%, #B61A39 50%, #500B19 100%)` |
| `red/red-gradient-2` | `linear-gradient(90deg, rgba(80,11,25,0) 0%, #500B19 18%, #B61A39 50%, #500B19 84%, rgba(80,11,25,0) 100%)` |

Both red gradients are designed for **section dividers, hero accents, or animated bands** — not for filling button backgrounds.

### 2.5 Beige

| Token name | Hex | Usage |
|---|---|---|
| `beige/deep-beige` | `#9D844E` | Dark beige accent, header/footer decorations |
| `beige/basic-beige` | `#B99D61` | **Secondary button** default state, premium accent |
| `beige/soft-beige` | `#CAB68A` | Background tints, subtle borders |
| `beige/soft-yellow` | `#E6C77F` | Warning highlights, soft callouts |
| `beige/light-yellow` | `#F8F2E5` | Background washes, info cards |
| `beige/pressed` | `#A08446` | Beige button pressed state |
| `beige/glow` (shadow) | `rgba(202, 182, 138, 0.35)` | Hover glow under beige buttons |
| `beige/gradient` | `linear-gradient(90deg, #B99D61 0%, #53462C 100%)` | Premium accent strips, hero dividers |

### 2.6 Neutral (translucent — for dark surfaces only)

| Token name | Definition | State |
|---|---|---|
| `neutral/default` | `linear-gradient(0deg, rgba(242,242,242,0.04) 0%, rgba(242,242,242,0.05) 100%)` | Default |
| `neutral/highlighted` | `linear-gradient(0deg, rgba(242,242,242,0.08) 0%, rgba(242,242,242,0.10) 100%)` | Hover |
| `neutral/glow` (shadow) | `rgba(54, 54, 54, 0.35)` | Hover shadow |

The neutral variant is intended for **secondary actions on a dark background** (passive buttons next to a red primary CTA). On light backgrounds, prefer the **white** button instead.

---

## 3. Typography

**Font family**: Montserrat (Google Fonts).
Weights used: **400 / 500 / 600 / 700**.

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600;700&display=swap" rel="stylesheet">
```

### 3.1 Full Scale

All sizes use Montserrat, color `#191919` (grey/dark-grey) by default. Override `color` for dark-themed surfaces.

| Token | Weight | Size | Line-height | Transform | Usage / Figma annotation |
|---|---|---|---|---|---|
| `H1` | 700 | 48px | 59px | — | Hero / page title |
| `H1_Mobile` | 700 | 35px | 43px | — | Mobile hero |
| `H2` | 600 | 34px | 41px | — | Section title |
| `H3` | 600 | 27px | 33px | — | Sub-section title |
| `H3_Mobile` | 600 | 27px | 33px | — | Mobile sub-section |
| `H3_Subtitles` | 700 | 27px | 33px | uppercase | "For very important subtitles" |
| `H4_Regular` | 400 | 16px | 160% (~26px) | — | Body paragraph |
| `H4_Medium` | 500 | 16px | 160% | — | Emphasized body |
| `H4_SemiBold` | 600 | 16px | 160% | — | Body with emphasis |
| `H4_Bold` | 700 | 16px | 160% | — | Strong inline emphasis |
| `H4_Subtitles_Semibold` | 600 | 16px | 160% | uppercase | **"For buttons and other"** ← canonical button label style |
| `H4_Subtitles_Bold` | 700 | 16px | 160% | uppercase | **"For menu"** ← navigation labels |
| `H5_Regular` | 400 | 13px | 20px (~154%) | — | Small body, captions, secondary status |
| `H5_Bold` | 700 | 13px | 16px | — | Small caps, table headers, compact section labels |

### 3.2 OpenType Feature Settings

| Style group | `font-feature-settings` |
|---|---|
| H4_Regular / H4_Medium | `'case' on, 'kern' off` |
| H4_SemiBold / H4_Bold / H4_Subtitles_Bold | `'liga' off, 'rclt' off` |
| H4_Subtitles_Semibold | (none specified — defaults) |
| All H5 / H1-H3 | (none specified — defaults) |

Set `'case' on` on body text so all-caps glyphs (acronyms, numbers next to caps) sit on the correct baseline. Set `'liga' off, 'rclt' off` on bold weights to avoid Montserrat's quirky ligatures swallowing brand names like "Rs" or "fi".

---

## 4. Buttons

All buttons share the same geometry — the variant is purely a fill style.

### 4.1 Base spec

| Property | Value |
|---|---|
| `padding` | `12px 20px` |
| `border-radius` | `10px` |
| `gap` (between text and icon) | `10px` |
| Typography | H4_Subtitles_Semibold (Montserrat 600 / 16px / 160% / uppercase) |
| `box-shadow` (default) | `0px 4px 35px rgba(0, 0, 0, 0.1)` |
| Border | none |

### 4.2 Variants × States

#### Red (primary CTA)

| State | Background | Box-shadow | Text |
|---|---|---|---|
| Default | `#92152E` | `0px 4px 35px rgba(0, 0, 0, 0.1)` | `#FFFFFF` |
| Highlighted (hover) | `#92152E` | `0px 4px 35px rgba(182, 26, 57, 0.35)` (red glow) | `#FFFFFF` |
| Pressed (active) | `#7A0C22` | `0px 4px 35px rgba(0, 0, 0, 0.1)` | `#FFFFFF` |
| Disabled | `#92152E` | base | `rgba(255,255,255,0.6)` + 0.4 opacity |

#### Beige (secondary CTA / distinct action)

| State | Background | Box-shadow | Text |
|---|---|---|---|
| Default | `#B99D61` | `0px 4px 35px rgba(0, 0, 0, 0.1)` | `#FFFFFF` |
| Highlighted (hover) | `#B99D61` | `0px 4px 35px rgba(202, 182, 138, 0.35)` (beige glow) | `#FFFFFF` |
| Pressed (active) | `#A08446` | base | `#FFFFFF` |
| Disabled | `#B99D61` | base | `rgba(255,255,255,0.6)` + 0.4 opacity |

#### Neutral (passive on dark)

| State | Background | Box-shadow | Text |
|---|---|---|---|
| Default | `linear-gradient(0deg, rgba(242,242,242,0.04) 0%, rgba(242,242,242,0.05) 100%)` | `0px 4px 35px rgba(0, 0, 0, 0.1)` | `#FFFFFF` |
| Highlighted (hover) | `linear-gradient(0deg, rgba(242,242,242,0.08) 0%, rgba(242,242,242,0.10) 100%)` | `0px 4px 35px rgba(54, 54, 54, 0.35)` | `#FFFFFF` |
| Pressed (active) | (no fill — only `filter: drop-shadow(0px 4px 35px rgba(0,0,0,0.1))`) | — | `#FFFFFF` |
| Disabled | same as default | base | `#4E4E4E` |

#### White (passive on light)

| State | Background | Box-shadow | Text |
|---|---|---|---|
| Default | `linear-gradient(0deg, rgba(242,242,242,0.8) 0%, #EEEEEE 100%)` | `0px 4px 35px rgba(0, 0, 0, 0.1)` | Dark grey gradient on text (clip) |
| Highlighted (hover) | `linear-gradient(0deg, #F2F2F2 0%, #EEEEEE 100%)` | `0px 4px 35px rgba(238, 238, 238, 0.35)` | Dark grey gradient |
| Pressed (active) | `linear-gradient(0deg, rgba(0,0,0,0.1), rgba(0,0,0,0.1)), linear-gradient(0deg, rgba(242,242,242,0.8) 0%, #EEEEEE 100%)` | base | Dark grey gradient |

White button text uses a clip-to-text gradient:

```css
background: linear-gradient(180deg, #1D1D1D 0%, #333333 100%);
-webkit-background-clip: text;
-webkit-text-fill-color: transparent;
background-clip: text;
```

### 4.3 Variants with icon

The kit supports buttons with a trailing circular arrow icon ("VIEW PORTFOLIO →" style). Add a `20×20px` circle to the right of the label:

```css
.btn-icon-circle {
  width: 20px;
  height: 20px;
  border-radius: 11.6667px;
  background: linear-gradient(180deg, rgba(29,29,29,0.5) 0%, rgba(51,51,51,0.5) 100%);
  display: inline-flex;
  align-items: center;
  justify-content: center;
}
/* The arrow inside is a 1px line, 6.67px long, rotated -45deg */
```

Use this **only on red/red+icon and white/white+icon variants** (per the kit).

### 4.4 Variant selection guide

| Action type | Variant | Example |
|---|---|---|
| Primary action (the main thing to click) | **red** | "Send", "Buy now", "Sign in", "Save", "Submit", "Record this meeting" |
| Premium / highlighted alternate action (distinct, brand-prominent) | **beige** | "Upgrade to pro", "Try free trial", "Featured" |
| Passive / secondary on dark | **neutral** | "Stop recording", "Test connection", "Sign out", "Skip", "Cancel" |
| Passive / secondary on light | **white** | "Learn more", "Read docs" |
| Destructive | **red** (with confirmation modal) | "Delete account" |

Avoid stacking two red buttons next to each other — pick one primary and use neutral (or beige if it's a brand-prominent alternate) for the other.

> **Note on Stop / Cancel actions**: these go to **neutral**, not red or beige. Stop is a deliberate passive action — the user wants to undo what's currently happening. Highlighting it red implies aggressive action; beige implies promotional. Neutral with `#4E4E4E` disabled text + translucent bg matches the Figma kit's "Color=neutral, State=disabled" / "State=pressed" spec exactly.

---

## 5. Spacing & Geometry

### Surfaces

- Card border-radius: **45px** (large hero cards), **60px** (extra-soft hero cards), **10px** (compact panels)
- Card padding: typically **60px** on desktop, **24-32px** on mobile
- Card background: `gradient/soft-grey-gradient-100` (light) or `#0F0F0F` / `#161616` (dark)

### Component spacing

- Buttons in a row: `gap: 10px`
- Button text → icon: `gap: 10px`
- Form label → input: `margin-top: 6px`
- Sections vertically: `padding: 18px 22px 20px` (compact tool) or `60px` (marketing surface)

### Borders & dividers

- Subtle vertical/horizontal section divider: `1px solid #4C4C4C` (basic-grey)
- Subtle divider on dark: `1px solid rgba(255, 255, 255, 0.06)`
- Input border focus: `1px solid rgba(146, 21, 46, 0.6)` (red-deep at 60%)

---

## 6. Status & Feedback Colors

These are derived tokens not in the base palette but standardized for cross-tool usage:

| Token | Hex | Usage |
|---|---|---|
| `success` | `#4ADE80` | Positive confirmations ("Saved", "Connected", "Signed in") |
| `error` | `#F71F20` (= `red/bright-red`) | Error text, validation failures |
| `recording` | `#F71F20` (= `red/bright-red`) | Live recording / live broadcast indicators (animate pulse) |
| `warning` | `#E6C77F` (= `beige/soft-yellow`) | Warnings, "may cause data loss" |

### Recording / live pulse animation

```css
@keyframes pulse {
  0%   { box-shadow: 0 0 0 0   rgba(247, 31, 32, 0.55); }
  70%  { box-shadow: 0 0 0 9px rgba(247, 31, 32, 0);    }
  100% { box-shadow: 0 0 0 0   rgba(247, 31, 32, 0);    }
}
.dot-recording {
  width: 10px; height: 10px; border-radius: 50%;
  background: #F71F20;
  animation: pulse 1.8s ease-out infinite;
}
```

---

## 7. Implementation Snippets

### 7.1 CSS Custom Properties (vanilla)

Drop this `:root` block at the top of your stylesheet. Reference variables anywhere.

```css
:root {
  /* Grey */
  --grey-dark:           #191919;
  --grey-deep:           #333333;
  --grey-basic:          #4C4C4C;
  --grey-cold:           #B2B9BF;
  --grey-middle:         #D9D9D9;
  --grey-soft:           #F2F2F2;
  --grey-for-text:       #9D9C9D;
  --gradient-grey-soft:  linear-gradient(0deg, #F2F2F2 0%, #EEEEEE 100%);
  --gradient-grey-dark:  linear-gradient(180deg, #1D1D1D 0%, #333333 100%);

  /* Red */
  --red-deep:            #92152E;
  --red-pressed:         #7A0C22;
  --red-branded:         #B61A39;
  --red-bright:          #F71F20;
  --red-bright-branded:  #FF1141;
  --red-glow:            rgba(182, 26, 57, 0.35);
  --gradient-red:        linear-gradient(90deg, #500B19 0%, #B61A39 50%, #500B19 100%);

  /* Beige */
  --beige-deep:          #9D844E;
  --beige-basic:         #B99D61;
  --beige-pressed:       #A08446;
  --beige-soft:          #CAB68A;
  --beige-soft-yellow:   #E6C77F;
  --beige-light-yellow:  #F8F2E5;
  --beige-glow:          rgba(202, 182, 138, 0.35);
  --gradient-beige:      linear-gradient(90deg, #B99D61 0%, #53462C 100%);

  /* Neutral (translucent on dark) */
  --neutral-bg:          linear-gradient(0deg, rgba(242, 242, 242, 0.04) 0%, rgba(242, 242, 242, 0.05) 100%);
  --neutral-bg-hover:    linear-gradient(0deg, rgba(242, 242, 242, 0.08) 0%, rgba(242, 242, 242, 0.10) 100%);

  /* Shadows */
  --shadow-base:         0px 4px 35px rgba(0, 0, 0, 0.1);
  --shadow-neutral-h:    0px 4px 35px rgba(54, 54, 54, 0.35);

  /* Status */
  --success:             #4ADE80;
  --error:               #F71F20;
  --warning:             #E6C77F;

  /* Geometry */
  --radius-btn:          10px;
  --radius-input:        8px;
  --radius-card:         45px;
}
```

### 7.2 Button — paste-ready CSS

```css
.btn {
  display: inline-flex; align-items: center; justify-content: center;
  gap: 10px;
  padding: 12px 20px;
  border-radius: var(--radius-btn);
  border: none;
  cursor: pointer;
  font-family: 'Montserrat', sans-serif;
  font-weight: 600;
  font-size: 16px;
  line-height: 1.6;
  text-transform: uppercase;
  letter-spacing: 0.4px;
  box-shadow: var(--shadow-base);
  transition: background .12s, box-shadow .15s, color .12s, transform .08s;
}

.btn--red          { background: var(--red-deep);    color: #FFF; }
.btn--red:hover    { box-shadow: 0 4px 35px var(--red-glow); }
.btn--red:active   { background: var(--red-pressed); }

.btn--beige        { background: var(--beige-basic); color: #FFF; }
.btn--beige:hover  { box-shadow: 0 4px 35px var(--beige-glow); }
.btn--beige:active { background: var(--beige-pressed); }

.btn--neutral        { background: var(--neutral-bg);       color: #FFF; }
.btn--neutral:hover  { background: var(--neutral-bg-hover); box-shadow: var(--shadow-neutral-h); }

.btn:disabled { opacity: 0.4; cursor: not-allowed; }
.btn:active:not(:disabled) { transform: translateY(1px); }
```

### 7.3 Tailwind config

```js
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
        grey:  {
          dark:    '#191919',
          deep:    '#333333',
          basic:   '#4C4C4C',
          cold:    '#B2B9BF',
          middle:  '#D9D9D9',
          soft:    '#F2F2F2',
          text:    '#9D9C9D',
        },
        red: {
          deep:           '#92152E',
          pressed:        '#7A0C22',
          branded:        '#B61A39',
          bright:         '#F71F20',
          'bright-brand': '#FF1141',
        },
        beige: {
          deep:           '#9D844E',
          basic:          '#B99D61',
          pressed:        '#A08446',
          soft:           '#CAB68A',
          'soft-yellow':  '#E6C77F',
          'light-yellow': '#F8F2E5',
        },
      },
      fontFamily: {
        sans: ['Montserrat', 'system-ui', 'sans-serif'],
      },
      fontSize: {
        // [size, { lineHeight, fontWeight }]
        'h1':           ['48px', { lineHeight: '59px', fontWeight: '700' }],
        'h1-mobile':    ['35px', { lineHeight: '43px', fontWeight: '700' }],
        'h2':           ['34px', { lineHeight: '41px', fontWeight: '600' }],
        'h3':           ['27px', { lineHeight: '33px', fontWeight: '600' }],
        'h3-sub':       ['27px', { lineHeight: '33px', fontWeight: '700' }],
        'h4-reg':       ['16px', { lineHeight: '160%', fontWeight: '400' }],
        'h4-med':       ['16px', { lineHeight: '160%', fontWeight: '500' }],
        'h4-semi':      ['16px', { lineHeight: '160%', fontWeight: '600' }],
        'h4-bold':      ['16px', { lineHeight: '160%', fontWeight: '700' }],
        'h4-sub-semi':  ['16px', { lineHeight: '160%', fontWeight: '600' }], // buttons
        'h4-sub-bold':  ['16px', { lineHeight: '160%', fontWeight: '700' }], // menu
        'h5-reg':       ['13px', { lineHeight: '20px', fontWeight: '400' }],
        'h5-bold':      ['13px', { lineHeight: '16px', fontWeight: '700' }],
      },
      borderRadius: {
        btn:   '10px',
        input: '8px',
        card:  '45px',
      },
      boxShadow: {
        base:       '0px 4px 35px rgba(0, 0, 0, 0.1)',
        'red-glow': '0px 4px 35px rgba(182, 26, 57, 0.35)',
        'beige-glow': '0px 4px 35px rgba(202, 182, 138, 0.35)',
        'neutral-glow': '0px 4px 35px rgba(54, 54, 54, 0.35)',
      },
    },
  },
};
```

Tailwind usage example:

```html
<button class="bg-red-deep hover:shadow-red-glow active:bg-red-pressed
               text-white px-5 py-3 rounded-btn font-semibold uppercase
               text-h4-sub-semi shadow-base transition">
  Sign in with Google
</button>
```

### 7.4 JSON Design Tokens (Style Dictionary / Figma Tokens compatible)

```json
{
  "color": {
    "grey": {
      "dark":       { "value": "#191919" },
      "deep":       { "value": "#333333" },
      "basic":      { "value": "#4C4C4C" },
      "cold":       { "value": "#B2B9BF" },
      "middle":     { "value": "#D9D9D9" },
      "soft":       { "value": "#F2F2F2" },
      "for-text":   { "value": "#9D9C9D" }
    },
    "red": {
      "deep":           { "value": "#92152E" },
      "pressed":        { "value": "#7A0C22" },
      "branded":        { "value": "#B61A39" },
      "bright":         { "value": "#F71F20" },
      "bright-branded": { "value": "#FF1141" }
    },
    "beige": {
      "deep":         { "value": "#9D844E" },
      "basic":        { "value": "#B99D61" },
      "pressed":      { "value": "#A08446" },
      "soft":         { "value": "#CAB68A" },
      "soft-yellow":  { "value": "#E6C77F" },
      "light-yellow": { "value": "#F8F2E5" }
    }
  },
  "shadow": {
    "base":         { "value": "0px 4px 35px rgba(0, 0, 0, 0.1)" },
    "red-glow":     { "value": "0px 4px 35px rgba(182, 26, 57, 0.35)" },
    "beige-glow":   { "value": "0px 4px 35px rgba(202, 182, 138, 0.35)" },
    "neutral-glow": { "value": "0px 4px 35px rgba(54, 54, 54, 0.35)" }
  },
  "typography": {
    "fontFamily":  { "value": "Montserrat, system-ui, sans-serif" },
    "h1":          { "value": { "fontWeight": 700, "fontSize": "48px", "lineHeight": "59px" } },
    "h1-mobile":   { "value": { "fontWeight": 700, "fontSize": "35px", "lineHeight": "43px" } },
    "h2":          { "value": { "fontWeight": 600, "fontSize": "34px", "lineHeight": "41px" } },
    "h3":          { "value": { "fontWeight": 600, "fontSize": "27px", "lineHeight": "33px" } },
    "h3-subtitles":      { "value": { "fontWeight": 700, "fontSize": "27px", "lineHeight": "33px", "textTransform": "uppercase" } },
    "h4-regular":        { "value": { "fontWeight": 400, "fontSize": "16px", "lineHeight": "160%" } },
    "h4-medium":         { "value": { "fontWeight": 500, "fontSize": "16px", "lineHeight": "160%" } },
    "h4-semibold":       { "value": { "fontWeight": 600, "fontSize": "16px", "lineHeight": "160%" } },
    "h4-bold":           { "value": { "fontWeight": 700, "fontSize": "16px", "lineHeight": "160%" } },
    "h4-subtitles-semi": { "value": { "fontWeight": 600, "fontSize": "16px", "lineHeight": "160%", "textTransform": "uppercase" }, "comment": "for buttons and other" },
    "h4-subtitles-bold": { "value": { "fontWeight": 700, "fontSize": "16px", "lineHeight": "160%", "textTransform": "uppercase" }, "comment": "for menu" },
    "h5-regular":        { "value": { "fontWeight": 400, "fontSize": "13px", "lineHeight": "20px" } },
    "h5-bold":           { "value": { "fontWeight": 700, "fontSize": "13px", "lineHeight": "16px" } }
  },
  "radius": {
    "button": { "value": "10px" },
    "input":  { "value": "8px"  },
    "card":   { "value": "45px" }
  }
}
```

### 7.5 SCSS Variables

```scss
// _rsg-tokens.scss
$grey-dark:    #191919;
$grey-deep:    #333333;
$grey-basic:   #4C4C4C;
$grey-cold:    #B2B9BF;
$grey-middle:  #D9D9D9;
$grey-soft:    #F2F2F2;
$grey-text:    #9D9C9D;

$red-deep:     #92152E;
$red-pressed:  #7A0C22;
$red-branded:  #B61A39;
$red-bright:   #F71F20;
$red-glow:     rgba(182, 26, 57, 0.35);

$beige-basic:    #B99D61;
$beige-pressed:  #A08446;
$beige-deep:     #9D844E;
$beige-soft:     #CAB68A;
$beige-soft-y:   #E6C77F;
$beige-light-y:  #F8F2E5;
$beige-glow:     rgba(202, 182, 138, 0.35);

$shadow-base:    0px 4px 35px rgba(0, 0, 0, 0.1);

$radius-btn:     10px;
$radius-input:   8px;
$radius-card:    45px;

$ff-base:       'Montserrat', system-ui, sans-serif;
```

### 7.6 Python (for tkinter / customtkinter / Streamlit Markdown / dash)

```python
# rsg_colors.py
GREY_DARK    = "#191919"
GREY_DEEP    = "#333333"
GREY_BASIC   = "#4C4C4C"
GREY_COLD    = "#B2B9BF"
GREY_MIDDLE  = "#D9D9D9"
GREY_SOFT    = "#F2F2F2"

RED_DEEP     = "#92152E"
RED_PRESSED  = "#7A0C22"
RED_BRANDED  = "#B61A39"
RED_BRIGHT   = "#F71F20"

BEIGE_BASIC   = "#B99D61"
BEIGE_PRESSED = "#A08446"
BEIGE_DEEP    = "#9D844E"

FONT_FAMILY = "Montserrat"

# customtkinter example
import customtkinter as ctk
btn = ctk.CTkButton(
    parent,
    text="SIGN IN WITH GOOGLE",
    fg_color=RED_DEEP,
    hover_color=RED_BRANDED,
    text_color="#FFFFFF",
    corner_radius=10,
    font=(FONT_FAMILY, 16, "bold"),
)
```

---

## 8. Reference Implementation

Working production code that uses every token described above:

**Meet Recorder Chrome extension** (dark theme):
- `AI Labs Nicolas/Projects/MeetRecorder/src/popup.html` — markup with section structure
- `AI Labs Nicolas/Projects/MeetRecorder/src/popup.css` — all tokens applied, button variants, pulse animation
- `AI Labs Nicolas/Projects/MeetRecorder/src/popup.js` — usage of `.recording` / `.ok` / `.err` / `.muted` status classes

Open the popup at `chrome://extensions` → Meet Recorder card → click extension icon. Live demo of red/beige/neutral buttons + animated recording dot + Montserrat hierarchy on a dark surface.

---

## 9. Open Questions / Gaps

Things not specified in the current Figma export that may need follow-up:

- **Light-theme button hover/pressed states for "neutral" variant** — Figma only defines neutral for dark. If a light-theme tool needs a passive button, use **white** variant instead.
- **Focus rings for accessibility (keyboard nav)** — Figma kit doesn't define `:focus` ring color. Recommend: `outline: 2px solid var(--red-deep); outline-offset: 2px;` for primary, or `outline-color: var(--grey-basic)` for neutral.
- **Error input border** — not in kit. Recommend: `border-color: var(--red-bright); background-color: rgba(247, 31, 32, 0.05);`
- **Icon set** — kit defines a single circular-arrow icon for buttons. A broader icon library (close, settings, expand, etc.) needs a parallel decision (Lucide / Heroicons / custom set).
- **Modal / dialog spec** — backgrounds, overlays, max-width — not yet derived from Figma.
- **Form validation states** (success/error/warning border + helper text styling) — partially implied by status colors but not formalized.

Resolve these centrally before adding new tools, or document local exceptions per integration.

---

## 10. Changelog

| Date | Change | Author |
|---|---|---|
| 2026-05-12 | Initial extraction from Figma export. Covers grey/red/beige palettes, full Montserrat type scale, button variants × states (red/beige/neutral/white), CSS variables, Tailwind config, JSON tokens, SCSS, Python. Reference impl: Meet Recorder popup. | (handoff to PM) |
