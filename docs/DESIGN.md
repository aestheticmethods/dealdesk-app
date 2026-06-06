# DealDesk Design System

## Brand Personality

Clean, direct, and trustworthy. DealDesk is a B2B deal management tool built for sales teams who need fast, confident decisions. The visual language takes cues from Cash App's design philosophy: high contrast, purposeful use of color, and a focus on data clarity over decoration. Whitespace is intentional. Color signals meaning — it is never ornamental.

---

## Color Palette

### Surface
| Token | Hex | Usage |
|---|---|---|
| `Surface` | `#FFFFFF` | Card and component backgrounds |

### Stroke / Border
| Token | Hex | Usage |
|---|---|---|
| `Stroke` | `#BDBDBD` | Dividers, input borders, card outlines |

### Semantic / Status
| Token | Hex | Usage |
|---|---|---|
| `Color.Positive` | `#4CAF50` | Positive trend, growth, success states |
| `Color.Negative` | `#F44336` | Negative trend, decline, error states |

### Text
| Token | Hex | Usage |
|---|---|---|
| `Color.Text.Primary` | `#000000` | Headings, metric values, primary labels |
| `Color.Text.Secondary` | `#616161` | Supporting labels, metadata, captions |

---

## Typography

Inspired by Cash App's tight, legible typographic system — favor geometric or grotesque sans-serifs that read clearly at small sizes and command attention at display sizes.

- **Font family:** Inter (fallback: system-ui, -apple-system, sans-serif)
- **Label / metadata:** 12px (`Text size.12`), weight 400, `Color.Text.Secondary`
- **Body / descriptions:** 14–16px, weight 400, `Color.Text.Primary`
- **Metric values / large numbers:** 24px (`Text size.24`), weight 700, `Color.Text.Primary`
- **Change indicators:** 12px, weight 400, semantic color (Positive or Negative)

---

## Spacing

All spacing uses a base-4 scale.

| Token | Value | Usage |
|---|---|---|
| `Spacing.24` | `24px` | Card internal padding, section gaps |
| `Spacing.32` | `32px` | Between-card spacing, section spacing |

---

## Shape

| Token | Value | Usage |
|---|---|---|
| `Corner radius.8` | `8px` | Card corner radius, button radius |

---

## Component Patterns

### Stat Card

A metric display card showing a single KPI with trend context.

**Structure (vertical stack):**
- **Header row** (horizontal, space-between): Label text (left) + Trend icon (right)
- **Value:** Large bold number
- **Change indicator:** Small text, colored by trend direction

**Token application:**
- Card background: `Surface` (`#FFFFFF`)
- Card border: 1px solid `Stroke` (`#BDBDBD`)
- Card padding: `Spacing.24` (24px) on all sides
- Corner radius: `Corner radius.8` (8px)
- Label: `Color.Text.Secondary`, 12px
- Value: `Color.Text.Primary`, 24px, bold
- Change text (positive): `Color.Positive` (`#4CAF50`)
- Change text (negative): `Color.Negative` (`#F44336`)
- Change text (neutral): `Color.Text.Secondary` (`#616161`)

**States:** positive · negative · neutral

---

## Layout

- **Dashboard grid:** 12 columns, 24px gutter
- **Max content width:** 1200px
- **Card grid gap:** `Spacing.24` (24px)
- **Section spacing:** `Spacing.32` (32px)
- **Base unit:** 4px
