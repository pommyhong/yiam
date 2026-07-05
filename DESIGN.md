# DESIGN.md -- Yiam

**In one line:** Minimal · mono-first expense tracker — พื้นขาว, ปุ่มหลักสีดำ, สีสื่อความหมายไม่ใช่ตกแต่ง

> import: `figma-cli import yiam/DESIGN.md --collection "Yiam"` → สร้าง Figma variables จริง

---

## 1. Colors

| Token | Value | ใช้ตรงไหน |
|---|---|---|
| `canvas` | `#FFFFFF` | พื้นหลังหลัก |
| `surface` | `#F5F5F5` | card / sheet / field |
| `surface-strong` | `#EBEBEB` | hover / pressed bg |
| `ink` | `#111111` | text หลัก + ปุ่ม primary + กราฟ |
| `ink-muted` | `#8E8E93` | label, secondary text |
| `ink-subtle` | `#C7C7CC` | placeholder, divider |
| `on-ink` | `#FFFFFF` | text บนปุ่มดำ |
| `border` | `#E5E5E5` | เส้นขอบ card / input |
| `income` | `#1FAA59` | ตัวเลข "+รับ" เท่านั้น |
| `expense` | `#111111` | ตัวเลขจ่าย = ink (คุม mono) |
| `danger` | `#E5484D` | ลบ / destructive เท่านั้น |
| `accent` | `#111111` | = ink (slot เผื่อใส่สีทีหลัง) |

> สีสื่อ "ความหมาย" ไม่ใช่ "ตกแต่ง" — เขียว=เงินเข้า, แดง=อันตราย, ที่เหลือ mono

## 2. Typography
font: Inter / SF Pro — น้ำหนักคือเครื่องมือหลัก ไม่ใช่สี

| Token | Size | Weight | ใช้ |
|---|---|---|---|
| `amount-hero` | 48 | 700 | ยอดรวม Stats / amount ตอนพิมพ์ |
| `amount-row` | 17 | 600 | ตัวเลขในรายการ |
| `title` | 22 | 700 | หัวข้อหน้า |
| `body` | 15 | 400 | ข้อความทั่วไป |
| `label` | 13 | 500 | label field / ชื่อหมวด |
| `caption` | 12 | 400 | วันที่ / %, secondary |

## 3. Spacing (4-pt base)
`xs` 4 · `sm` 8 · `md` 12 · `lg` 16 · `xl` 24 · `2xl` 32

## 4. Radius
`r-field` 12 (input/chip) · `r-card` 16 (card) · `r-sheet` 24 (sheet) · `r-pill` 999 (toggle/FAB)

## 5. Elevation
`shadow-sheet` `0 -4px 24px rgba(0,0,0,0.08)` · `shadow-fab` `0 4px 16px rgba(0,0,0,0.20)`

## 6. Components (สเปคย่อ)
```
ปุ่ม Primary     bg ink · text on-ink · h 52 · r-pill · weight 600
ปุ่ม Primary:off bg surface-strong · text ink-subtle (disabled)
ปุ่ม Secondary   bg surface · text ink · border
Field            bg surface · r-field · h 52 · label เล็กบน, value ใหญ่ล่าง
Toggle (จ่าย/รับ) pill เทา · selected = ใส้ขาว+เงา (segmented)
Period selector  pill เทา · selected = ใส้ขาว
List row         h 64 · ไอคอนหมวด (วงกลม surface 40px) + ชื่อ/วันที่ + amount ขวา
Chart            แท่ง/วง = ink ล้วน (เน้นด้วยความเข้ม ไม่ใช่หลายสี)
Toast success    pill เขียวอ่อน + ✓ · ลอยล่าง 2 วิ
```
anti-patterns: ❌ สีหมวดหลากสี · ❌ gradient กราฟ · ❌ เส้นขอบหนา (ใช้ fill แยกพื้นที่)

---

## 7. Machine-readable tokens

```json design-tokens
{
  "$schema": "https://figma-cli/design-tokens",
  "meta": { "source": "Yiam DESIGN.md", "generated": "2026-06-17" },
  "color": {
    "canvas": "#FFFFFF",
    "surface": "#F5F5F5",
    "surface-strong": "#EBEBEB",
    "ink": "#111111",
    "ink-muted": "#8E8E93",
    "ink-subtle": "#C7C7CC",
    "on-ink": "#FFFFFF",
    "border": "#E5E5E5",
    "income": "#1FAA59",
    "expense": "#111111",
    "danger": "#E5484D",
    "accent": "#111111"
  },
  "typography": {
    "amount-hero": { "fontFamily": "Inter", "fontSize": 48, "fontWeight": 700 },
    "amount-row":  { "fontFamily": "Inter", "fontSize": 17, "fontWeight": 600 },
    "title":       { "fontFamily": "Inter", "fontSize": 22, "fontWeight": 700 },
    "body":        { "fontFamily": "Inter", "fontSize": 15, "fontWeight": 400 },
    "label":       { "fontFamily": "Inter", "fontSize": 13, "fontWeight": 500 },
    "caption":     { "fontFamily": "Inter", "fontSize": 12, "fontWeight": 400 }
  },
  "spacing": { "xs": 4, "sm": 8, "md": 12, "lg": 16, "xl": 24, "2xl": 32 },
  "radius": { "r-field": "12px", "r-card": "16px", "r-sheet": "24px", "r-pill": "999px" },
  "shadow": {
    "shadow-sheet": "0 -4px 24px rgba(0,0,0,0.08)",
    "shadow-fab": "0 4px 16px rgba(0,0,0,0.20)"
  },
  "fonts": ["Inter"]
}
```
