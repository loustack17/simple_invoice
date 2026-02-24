# Typst Invoice Template

## Build

```bash
typst compile invoice.typ
```

## Structure

- `invoice.typ`: entrypoint.
- `module/data.typ`: invoice content and values.
- `module/model.typ`: calculation, formatting, and data transformation logic.
- `module/layout.typ`: rendering flow and section-level layout functions.
- `module/config.typ`: page, typography, color, stroke, spacing, and column settings.
- `assets/logo.png`: logo image.

## Common Edits

- Update invoice content in `module/data.typ`.
- Set `meta.date_override`:
  - `none`: auto use current date.
  - `"FEBRUARY 24, 2026"`: use a fixed date string.
- Service fields use numeric values (`rate: 100`, `quantity: 24`, `discount: 0`).
- Add `rate_unit` per service (e.g., `"hr"`).
- Detail rows only need `text` and `quantity`; amounts are auto-calculated from the service rate.
- Add multiple services in `table.services` (tuple of service objects).
- Change detail list marker in `module/data.typ` (`table.detail_marker`).
- Adjust typography, colors, spacing, or widths in `module/config.typ`.

## Auto-Calculated Fields

- Detail amounts: `service.rate * detail.quantity`.
- `total_amount`: sum of `rate * quantity - discount` across all services.
- `balance_amount`: `total_amount - payment_amount`.

## Automatic Layout Behavior

- Service and detail text wraps automatically based on column width.
- Detail rows grow or shrink with content length.
- No fixed 2-line padding is reserved for short text.
- Summary and payment sections flow downward automatically after the table.
