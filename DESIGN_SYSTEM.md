# OnlyRound Design System
### Absolute AI Instruction File — Source of Truth for All Visual Decisions

> **This file is the single source of truth for all design decisions on this codebase.**
> Every AI assistant, developer, or contributor MUST read and follow this before touching any UI code.
> Do NOT invent new colors, font sizes, spacing values, or component patterns without first checking this file.

---

## 1. Color System

All colors are defined as CSS custom properties on `:root` and overridden per theme by the `THEMES` JS object.
**Never use raw hex values in markup. Always use the CSS token.**

### 1.1 Semantic Color Tokens

| Token | Role | Dark Mode | Light Mode |
|---|---|---|---|
| `--bg` | Page canvas background | `#07100D` | `#F2F7F4` |
| `--ink` | Primary text (headings, body, labels) | `#F1F6F3` | `#08130F` |
| `--mut` | Secondary/muted text (descriptions, captions) | `#8B9A94` | `#43544D` |
| `--line` | Dividers, borders, hairlines | `rgba(255,255,255,.11)` | `rgba(8,19,15,.14)` |
| `--card` | Surface 1 — default card, row, input background | `rgba(255,255,255,.04)` | `#FFFFFF` |
| `--card2` | Surface 2 — elevated panel, tag background | `rgba(255,255,255,.06)` | `#E6F0EA` |
| `--panel` | Surface 0 — deep panels, modals | `#0B1714` | `#FFFFFF` |
| `--head` | Header bar (with transparency for blur) | `rgba(7,16,13,.78)` | `rgba(242,247,244,.88)` |
| `--shadow` | Box shadow for elevated cards | `0 34px 80px -40px rgba(0,0,0,.9)` | `0 24px 60px -20px rgba(8,19,15,.14), 0 4px 16px -4px rgba(8,19,15,.06)` |

### 1.2 Brand Accent Tokens

| Token | Role | Dark | Light | Contrast on --card |
|---|---|---|---|---|
| `--accent` | Primary brand: CTAs, active states, green tags | `#3EBA8D` | `#147A51` | 5.2:1 AA ✅ |
| `--accent2` | Secondary brand: info/assessment, blue tags | `#7BB9E5` | `#1E58C8` | 6.1:1 AA ✅ |
| `--gold` | Tertiary: outbound/scheduled, amber tags | `#FFD975` | `#B45309` | 4.6:1 AA ✅ |
| `--glow1` | Decorative ambient green halo (bg only) | `rgba(62,186,141,.30)` | `rgba(21,128,85,.24)` | Decorative only |
| `--glow2` | Decorative ambient blue halo (bg only) | `rgba(123,185,229,.24)` | `rgba(37,99,235,.20)` | Decorative only |

### 1.3 Semantic Status Colors (Hardcoded — theme-independent)

| Color | Value | Usage |
|---|---|---|
| Destructive/Error | `#E8544A` | "End interview" button, red-flag tags, live recording dot |
| Orb play button bg | `#ffffff` | Always white — sits on dark orb |
| Orb play icon | `#0E1210` | Always dark — on white circle |

### 1.4 Hero Shimmer Gradient (Decorative — intentional hardcode)

```
linear-gradient(96deg, #74D7AE, #7BB9E5, #FFD975, #74D7AE)
background-size: 200% auto; animation: shimmer 7s linear infinite
```

Keep as-is. These are decorative accent hues only and not subject to contrast rules.

---

## 2. Typography System

### 2.1 Font Families

| Family | CSS Declaration | Usage |
|---|---|---|
| **Familjen Grotesk** | `font-family: "Familjen Grotesk", Helvetica, sans-serif` | ALL body text, headings, navigation, UI copy |
| **IBM Plex Mono** | `font-family: 'IBM Plex Mono', monospace` | Step numbers, tags, badges, timestamps, eyebrow labels, copyright |

> **Rule:** Mono is ONLY for metadata, labels, and codes. Never use it for paragraph text or headings.

### 2.2 Type Scale

| Role | Size | Weight | Letter-Spacing | Color Token |
|---|---|---|---|---|
| H1 Hero | `66px` (mobile: 32-38px) | 600 | `-.038em` | `--ink` |
| H2 Section | `42px` (mobile: 28px) | 600 | `-.03em` | `--ink` |
| H3 Card heading | `24px` | 600 | `-.02em` | `--ink` |
| H4 Sub-heading | `18.5-19px` | 600 | `-.015em` | `--ink` |
| Body large | `18-20px` | 400 | default | `--mut` |
| Body | `15-16px` | 400 | default | `--mut` |
| Body small | `13-14.5px` | 400 | default | `--mut` |
| Eyebrow label | `11-11.5px` Mono | 400 | `+.1em` + uppercase | `--accent` |
| Tag/badge | `10-11px` Mono | 500 | `+.05-.12em` | `--accent` / `--accent2` / `--gold` / `--mut` |
| Timestamp / step num | `10-11px` Mono | 400 | `+.08em` | `--mut` |

---

## 3. Spacing System (8px Grid)

| Level | Range | Where used |
|---|---|---|
| xs | 4-6px | Icon-to-text gaps, dot-to-label |
| sm | 8-12px | Between items in a card |
| md | 14-18px | Card internal padding, row gaps |
| lg | 20-28px | Card padding, element spacing |
| xl | 30-42px | Section sub-elements, hero spacing |
| 2xl | 44-56px | Section padding-top (88px 0 0) |
| 3xl | 88-96px | Section margin-top between major sections |

Card padding rule:
- Standard card: `padding: 24-26px`
- Small row items: `padding: 12-14px 14-16px`
- Never below `8px` inside a card

---

## 4. Border and Radius Tokens

| Token | Value | Usage |
|---|---|---|
| Default border | `1px solid var(--line)` | All cards, rows, dividers |
| Active/focus border | `1px solid var(--accent)` | Active step, focused interactive element |
| No border | `border: none` | Icon containers inside step cards |
| radius-sm | `8-11px` | Buttons, chips, skip-link |
| radius-md | `12-13px` | CTA buttons, row pill tags |
| radius-lg | `18px` | Step cards, feature mini-cards |
| radius-xl | `22-26px` | Preview panels, modal |
| radius-2xl | `28px` | Contact CTA section |
| radius-pill | `999px` | Tags, badges, announcement chip |
| radius-circle | `50%` | Icon circles, avatar, play button |

---

## 5. Named Component Patterns

### 5.1 Section Eyebrow Label
```css
font-family: 'IBM Plex Mono', monospace;
font-size: 11.5px; letter-spacing: .1em; text-transform: uppercase;
color: var(--accent);
```

### 5.2 Section H2
```css
font-size: 42px; line-height: 1.08; letter-spacing: -.03em;
font-weight: 600; margin: 14px 0 0; color: var(--ink);
```

### 5.3 Section Descriptor Paragraph
```css
font-size: 18px; line-height: 1.6;
color: var(--mut); margin: 18px 0 0;
```

### 5.4 Primary CTA Button
```css
background: var(--ink); color: var(--bg);
font-size: 15-16px; font-weight: 500;
padding: 13-15px 24-28px; border-radius: 12px; border: none;
/* hover: */ opacity: .85
```
For: "Talk to sales", "Contact sales", "Start interview".

### 5.5 Secondary CTA Button (Outlined)
```css
background: transparent; border: 1px solid var(--line); color: var(--ink);
font-size: 14-16px; font-weight: 500;
padding: 9-15px 18-24px; border-radius: 11-12px;
/* hover: */ border-color: var(--accent); color: var(--accent)
```
For: "Log in", "See demo library", ghost navigation buttons.

### 5.6 Destructive Button
```css
background: rgba(232,84,74,.12); border: 1px solid rgba(232,84,74,.35);
color: #E8544A; padding: 13px 28px; border-radius: 12px;
/* hover: */ background: rgba(232,84,74,.22); border-color: #E8544A
```
ONLY for: "End interview", irreversible destructive actions.

### 5.7 Feature Card (Default)
```css
background: var(--card); border: 1px solid var(--line);
border-radius: 18px; padding: 24px 22px 26px;
transition: transform .4s ease, border-color .4s ease;
/* hover: */ transform: translateY(-4px); border-color: var(--accent)
```

### 5.8 Panel / Preview Card (Elevated)
```css
background: var(--card2); border: 1px solid var(--line);
border-radius: 22px; padding: 26px;
backdrop-filter: blur(12px); box-shadow: var(--shadow);
```

### 5.9 Tag / Badge Pill
```css
font-family: 'IBM Plex Mono', monospace; font-size: 10-11px; font-weight: 500;
color: [see color rule]; background: var(--card2); border: 1px solid var(--line);
border-radius: 999px; padding: 4-5px 10-11px;
```

**Tag color rules (semantic assignment — do not randomize):**
- `var(--accent)` = success / pass / inbound / completed / green states
- `var(--accent2)` = informational / assessment / neutral-info / blue states
- `var(--gold)` = outbound / scheduled / in-progress / active / amber states
- `var(--mut)` = default neutral / language info / plain descriptive labels
- `#E8544A` = red flag / error / failed states ONLY

### 5.10 Step Card Icon Box
```css
width: 44px; height: 44px; border-radius: 13px;
background: var(--card);
border: none; /* NO border on icon containers */
display: flex; align-items: center; justify-content: center;
```
SVG stroke uses `var(--accent)`, `var(--accent2)`, or `var(--gold)` per step. Never hardcoded hex.

### 5.11 Announcement Chip (Hero)
```css
border: 1px solid var(--line); border-radius: 999px;
padding: 6px 14px 6px 10px; background: var(--card);
font-family: 'IBM Plex Mono'; font-size: 11px; letter-spacing: .08em;
text-transform: uppercase; color: var(--mut);
/* inner dot: */ background: var(--accent); animation: pulse 2s ease-out infinite
```

### 5.12 Sticky Header / Topbar
```css
position: fixed; top: 0; left: 0; right: 0; z-index: 100;
background: var(--head); backdrop-filter: blur(14px);
border-bottom: 1px solid var(--line); height: 78px;
```

---

## 6. Motion and Animation Catalogue

| Name | Description | Duration |
|---|---|---|
| `rise` | Cards entering: fade + translateY(20px to 0) | `.45s cubic-bezier(.22,.7,.2,1)` |
| `pulse` | Status dot glow ring expand | `2s ease-out infinite` |
| `breathe` | Orb halo scale and fade | `5s ease-in-out infinite` |
| `drift` | Background glow blob float | `14-18s ease-in-out infinite` |
| `morph` | Orb border-radius organic shift + rotate | `8-11s ease-in-out infinite` |
| `marq` | ATS logo horizontal marquee | `28s linear infinite` |
| `shimmer` | Hero gradient text background shift | `7s linear infinite` |
| `grow` | Step progress bar width: 0 to 100% | `4.2s linear forwards` |
| `spin` | Spinner rotation | n/a |

> **Rule:** Prefer `transition` over custom keyframes for hover and interaction states. Only use keyframes for looping/ambient/decorative effects.

---

## 7. Layout Grid

```
max-width: 1180px
margin: 0 auto
padding: 78px 28px 0   (78px top = sticky header height compensation)
```

**Mobile (640px and below):** `.page-container { padding: 0 20px !important }`

**Section spacing pattern:**
```
padding-top: 88px
margin-top: 96px
border-top: 1px solid var(--line)
```

---

## 8. Theme System Rules

- Themes defined in `const THEMES = { dark: {...}, light: {...} }` in the DC script block.
- Applied via `applyTheme(name)` which sets CSS custom properties on `document.documentElement`.
- Default theme: **dark**. Persisted in `localStorage('onlyround-theme')`.
- Toggle icon: moon = dark mode, sun = light mode.

**Adding a new design token:**
1. Add CSS variable to `:root` style block with dark-mode default value.
2. Add the key-value pair to BOTH `THEMES.dark` AND `THEMES.light`.
3. **Never** define a token in only one theme.

---

## 9. WCAG 2.1 / ADA Compliance Requirements

| Standard | Minimum Ratio | Applies To |
|---|---|---|
| AA | 4.5:1 | Normal text, tags, labels (below 18px) |
| AA Large | 3:1 | Text 18px or larger, or 14px bold (headings) |
| AAA | 7:1 | Critical body text (our target) |

**Verified passing combinations (light mode, the harder constraint):**
- `--ink` (#08130F) on `--bg` (#F2F7F4) = 18.2:1 AAA
- `--mut` (#43544D) on `--bg` = 7.2:1 AAA
- `--accent` (#147A51) on `--card` (#FFF) = 5.2:1 AA
- `--accent2` (#1E58C8) on `--card` = 6.1:1 AA
- `--gold` (#B45309) on `--card` = 4.6:1 AA

**Never use these combinations:**
- `--mut` on `--card2` for text below 14px (may fail AA in light mode)
- Raw `#FFD975` as text on white backgrounds (use `var(--gold)` which resolves to `#B45309` in light mode)
- `--line` as a text color (fails contrast in both modes)
- `--glow1` or `--glow2` as text colors (decorative only)

---

## 10. Non-Negotiable Rules for AI Assistants and Developers

Follow every rule, every time. No exceptions without explicit product team approval.

1. **Use CSS tokens always** — No raw hex or rgb() colors in style attributes. Use `var(--token)`.
2. **No new colors** — Map new needs to existing tokens. If truly new, extend THEMES with full documentation in this file.
3. **Verify contrast before changing colors** — Must pass WCAG 2.1 AA minimum (4.5:1 for normal text).
4. **Font family is binary** — Familjen Grotesk for UI/body, IBM Plex Mono for labels/metadata. No other fonts.
5. **No borders on icon boxes** — Step card icon containers (44x44) have `border: none`. Background provides depth.
6. **Tag color semantics** — Follow the color-role mapping in Section 5.9. Never randomize tag colors.
7. **No ad-hoc shadow values** — Use `var(--shadow)` or document the specific shadow with justification.
8. **Section structure is fixed** — Every section: eyebrow label then H2 then descriptor paragraph. Do not reorder.
9. **Mobile padding must hold** — All sections respect `padding: 0 20px` on 640px and below. No full-bleed text.
10. **Hover states are required** — Every interactive card, button, and link must have a defined hover/transition state.
11. **Destructive red is reserved** — `#E8544A` is ONLY for "End call", errors, and red-flag states. Never for decoration.
12. **Sync both files** — After every change to `index.html`, run: `cp index.html "Rounds Landing.dc.html"`

---

## 11. Color Audit — All Hardcoded Values in Codebase (Last audited: Aug 4, 2026)

| Location | Hardcoded Value | Status |
|---|---|---|
| Hero play button background | `#ffffff` | Intentional — orb play button always white |
| Hero play button icon | `#0E1210` | Intentional — always dark on white circle |
| Hero shimmer gradient | `#74D7AE`, `#7BB9E5`, `#FFD975` | Intentional — purely decorative |
| End Interview button | `rgba(232,84,74,...)`, `#E8544A` | Intentional — destructive red |
| Live recording dot | `#E8544A` | Intentional — live/danger indicator |
| Microphone icon stroke | `#0E1210` | Intentional — on white circle, always dark |
| pulse keyframe | `rgba(62,186,141,.4)` | Should use --accent alpha on next refactor |
| Orb halo/inner/orb colors | Per-card dynamic JS values | Intentional — per-demo decorative theming |
| Timeline event dots | data-driven from JS array | Data-driven — map to --accent / --gold / --mut tokens |
| Module icon colors | data-driven from JS array | Should be mapped to var(--accent) / var(--accent2) / var(--gold) |
| Governance icon colors | data-driven from JS array | Should be mapped to var(--accent) / var(--accent2) / var(--gold) |

---

Last updated: August 4, 2026
Owner: OnlyRound product team
All changes to this file require explicit review before deployment.
