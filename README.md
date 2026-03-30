# home-service-profit-calculator
Profit margin calculator for junk removal, lawn care &amp; pressure washing
# 🏠 Home Service Profit Margin Calculator

A mobile-friendly, single-file web app built for home service business owners to quote jobs and analyze profit margins in real time. Originally built for junk removal, expanded to cover **Lawn Care** and **Pressure Washing** as well.

Live at: [your-netlify-url.netlify.app](https://stalwart-kataifi-7a629d.netlify.app/)

---

## 📋 What It Does

Business owners enter their job price and costs, and the calculator instantly shows:

- **Gross profit margin %** with a color-coded progress bar (green = great, yellow = moderate, red = danger)
- **Revenue, costs, and profit** broken down clearly
- **Recommended pricing ranges** at 20–30%, 31–49%, and 50–65% margin targets — calculated automatically from your actual costs
- **National average pricing** reference tables per industry
- **Pro tips** specific to each trade

---

## 🗂️ Industries Covered

### 🗑️ Junk Removal
| Job Type | Details |
|----------|---------|
| Volume-Based | Priced by truck load size (minimum → full load) |
| Multiple Full Loads | Multi-load jobs with optional per-load discount |
| Specialty Item Removal | Hot tub, trampoline, play set, shed, pool, piano, custom |
| Mixed Jobs | Specialty item + additional volume combined |

**Complexity add-ons:** Stairs, disassembly, heavy items surcharge, demolition labor fee

**Cost inputs:** Landfill/dump fee, dumpster rental, demo machine rental, truck rental, fuel, labor

---

### 🌿 Lawn Care
| Service Type | Details |
|-------------|---------|
| Mow & Edge | Priced by yard size (small → XL) |
| Full Yard Cleanup | Light / medium / heavy scope |
| Mulching | Priced per yard of mulch |
| Bush / Hedge Trimming | Priced by number of bushes |
| Leaf Removal | Light / medium / heavy volume |
| Aeration / Overseeding | Priced by square footage |

**Add-ons:** Overgrown yard surcharge, debris haul-away, steep slope surcharge, travel/distance fee

**Cost inputs:** Fuel, labor wages, materials (mulch/seed/fertilizer), equipment rental, dump fee

---

### 💦 Pressure Washing
| Surface Type | Details |
|-------------|---------|
| Driveway | Single / double / large |
| House Exterior / Siding | Small → XL by square footage |
| Deck or Patio | Priced by square footage |
| Fence | Priced by linear feet |
| Roof Soft Wash | Small / medium / large |
| Commercial / Parking Lot | Priced by square footage |

**Add-ons:** Heavy mold/mildew treatment, multiple surfaces bundle, travel/distance fee

**Cost inputs:** Chemical/soap cost, fuel, labor wages, equipment rental, water/access fee

---

## 🏗️ Project Structure

```
/
├── index.html              ← The entire app (self-contained)
├── apple-touch-icon.png    ← App icon for browser tab + iOS home screen
└── README.md               ← This file
```

**No build process. No dependencies. No frameworks.** Open `index.html` in any browser and it works.

---

## ⚙️ Tech Stack

| Layer | Tech |
|-------|------|
| Markup | HTML5 |
| Styling | Pure CSS (no frameworks) — CSS variables, flexbox, grid, backdrop-filter |
| Logic | Vanilla JavaScript — no libraries, no bundler |
| Font | [Space Grotesk](https://fonts.google.com/specimen/Space+Grotesk) via Google Fonts CDN |
| Hosting | [Netlify](https://netlify.com) (auto-deploys from this repo) |
| PWA | Apple mobile web app meta tags for home screen install support |

---

## 🧮 How the Math Works

### Gross Profit Margin
```
margin = ((revenue - cost) / revenue) × 100
```

### Recommended Pricing (calculated from your costs)
| Tier | Formula |
|------|---------|
| 20–30% (minimum viable) | `cost ÷ 0.80` to `cost ÷ 0.70` |
| 31–49% (moderate) | `cost ÷ 0.69` to `cost ÷ 0.51` |
| 50–65% (target zone) | `cost ÷ 0.50` to `cost ÷ 0.35` |

### Input Sanitization
All numeric inputs are run through:
```javascript
Math.max(0, Number(value) || 0)
```
This handles: empty strings, text input, whitespace, and negative numbers — all safely defaulted to `0`.

---

## 🧪 Testing

The calculator logic was tested with a Node.js test suite covering **71 test cases** across both new services:

- Zero inputs, normal jobs, losing-money scenarios
- All add-ons stacked simultaneously
- Add-ons checked but set to $0 (no false inflation)
- Service/surface type switching (no value bleed-over)
- Break-even (cost = revenue)
- Large numbers, decimal precision
- Empty string, text input, whitespace, negative numbers
- Recommended pricing band math verification

**Result: 71/71 passing. One bug found and fixed during testing** — negative price inputs were passing through to the margin display. Fixed by wrapping all numeric reads with `Math.max(0, ...)`.

---

## 🚀 Deployment

This repo is connected to Netlify for automatic deployment.

- **Branch:** `main`
- **Build command:** *(none — plain HTML)*
- **Publish directory:** `/`

Every commit to `main` triggers a new deploy automatically (usually live within 60 seconds).

### To run locally
Just open the file — no server needed:
```bash
open index.html        # Mac
start index.html       # Windows
```
Or drag `index.html` into any browser window.

---

## ✏️ How to Edit

All content lives in `index.html`. It is organized into clear comment sections:

| Section | Lines | Content |
|---------|-------|---------|
| `<head>` + CSS | 1–135 | Page setup, all styles |
| Header + Tabs + Junk Panel | 136–294 | Page header, industry tabs, Junk Removal form |
| Lawn Care Panel | 295–405 | Lawn Care calculator |
| Pressure Washing Panel + Footer | 406–520 | Pressure Washing calculator + footer |
| JavaScript | 521–695 | All calculator logic |

To add a new industry tab, you would:
1. Add a new `<button class="tab-btn">` in the tabs section
2. Add a new `<div class="industry-panel">` with your form
3. Add corresponding JS functions following the same `prefix-elementId` naming pattern used by the existing tabs (`j-` for junk, `l-` for lawn, `p-` for pressure)

---

## 📌 Notes for Developers

- **Naming convention:** All element IDs are prefixed by industry — `j-` (junk), `l-` (lawn), `p-` (pressure). This prevents ID collisions since all three panels exist in the DOM simultaneously, just hidden.
- **No localStorage:** The app is intentionally stateless. Each session starts fresh — no data is saved between visits.
- **PWA-ready:** The Apple meta tags allow users to add the app to their iPhone home screen and run it like a native app (no browser chrome).
- **Responsive:** Layout uses CSS Grid with a single breakpoint at 1000px (two-column → one-column). Tabs wrap on small screens at 600px.
- **Font fallback:** If Google Fonts fails to load (no internet), the app falls back to `-apple-system` sans-serif. All functionality is unaffected.

---

## 👤 Created By

**Tex Mex Junk Removal** — Part of the *Pricing Mastery Template Pack*

> Built to help home service business owners stop guessing on price and start quoting with confidence.
