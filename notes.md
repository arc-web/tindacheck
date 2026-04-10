# Pod A - Build Notes

## Problem We're Solving

Shoppers in the Philippines waste money because grocery stores don't make it easy to compare prices across brands and pack sizes. A 500ml bottle and a 1L bottle have different prices — which one is actually cheaper per ml? Most people guess. TindaCheck does the math instantly.

**One-sentence version:** We built a mobile price comparison tool that tells you which grocery product is the best deal, even when sizes and units are different.

---

## Our Approach

A lightweight, no-install web app that works on any phone — open the link, start comparing. No sign-up, no download.

- Enter product name, size, how many packs, and price
- App normalizes everything to the same unit (per 100ml, per 100g, per piece)
- Color-coded results: green = best deal, red = most expensive
- Barcode scanner to fill in product names faster
- Grocery list tab so you can plan before you shop
- History tab so you can look up past comparisons

---

## What We Built

**TindaCheck** — a mobile-first, single-page web app (pure HTML/CSS/JS, no framework).

### Features
- **Price comparison engine** — Formula: `Price ÷ (Size × Quantity)`, normalized to per 100g or per 100ml so products with different sizes compare fairly (e.g. 500ml vs 1L)
- **Up to 5 products** compared at once with add/remove cards
- **Barcode scanner** — uses device camera to scan barcodes and pre-fill product name
- **Packaging type** — optional label (bottle, tetra pack, sachet, can, pouch, bag, box) shown in results
- **Live total** — as you type size and quantity, shows "Total: 1000ml" in real time
- **Color-coded results** — green for best deal, amber for middle, red for most expensive
- **My List tab** — save items to your shopping list; tap Compare to jump straight into a comparison with that item pre-filled
- **History tab** — every comparison is saved locally; browse past results, see which product won
- **Dark/light theme** — respects system preference, toggleable
- **Works offline** — no server, no internet needed after first load

### Tech
- Single `index.html` file — no build step, no dependencies
- Data persists in `localStorage` (grocery list, history, theme)
- Camera access via browser API for barcode scanning

---

## How to Use It

1. Open the app (or the link shared in Discord)
2. On the **Compare** tab, fill in each item card:
   - Product name (or tap the scan icon to use your camera)
   - Packaging type (optional — bottle, can, etc.)
   - Size per pack (e.g. 500) and unit (ml, g, L, kg, piece)
   - How many packs you're buying (default: 1)
   - Total price in ₱
3. Tap **Compare Prices**
4. The green card is the best deal. The savings line tells you exactly how much cheaper it is per unit.
5. Tap **New Comparison** to start over, or switch to **History** to see past results.

**My List tab:** Add items you plan to buy before heading to the store. Tap Compare on any item to jump straight into a comparison with that name pre-filled.

---

## 60-Second Demo Script

*Do this live — it takes about 60 seconds.*

**Setup:** Have two products ready — a small and large version of the same thing (e.g. Del Monte Tomato Sauce 250g ₱28 and 500g ₱52, or two cooking oils of different sizes).

---

**[0–10s]** Open TindaCheck on your phone. Show the two product cards on screen.

"I'm at the grocery store. I've got two tomato sauces in my hands. I want to know which one is actually cheaper."

**[10–25s]** Fill in Item 1:
- Product name: *Del Monte Tomato Sauce*
- Packaging: *Can*
- Size: *250* | *g*
- Quantity: *1*
- Price: *₱28*

**[25–40s]** Fill in Item 2:
- Product name: *UFC Tomato Sauce*
- Packaging: *Pouch*
- Size: *500* | *g*
- Quantity: *1*
- Price: *₱52*

Point to the live total updating as you type: "See this — it's already calculating the total weight."

**[40–55s]** Tap **Compare Prices**.

Green card appears. "Del Monte is ₱11.20 per 100g. UFC is ₱10.40 per 100g — that's the better deal, even though it costs more upfront."

**[55–60s]** Tap **History**. "Every comparison I make gets saved here. I can check what I looked up last week."

---

**Why it lands:** Most people have stood in a grocery aisle doing this math in their head and gotten it wrong. TindaCheck does it in under a minute, on the phone already in their pocket.

---

## What We'd Do Next

- **Camera OCR** — point camera at the price tag to fill in the price automatically
- **Share results** — send a comparison to a family member via link or screenshot
- **Store presets** — save common store prices to compare across shops (S&R vs SM vs Puregold)
- **Peso-per-serving** — for products like coffee or milk powder, compare cost per cup
- **PWA install** — add to home screen so it behaves like a native app

---

## Prompts That Worked Well

- *"Redesign each item card with these fields in order: [list]. For comparison, calculate Price ÷ (Size × Quantity) and convert all units to the same base before comparing."*
- *"Add a comparison history tab. Every time the user compares, save it to localStorage. Show date, products, per-unit prices, and the winner."*
- *"Below the Size field, add hint text. As the user types size and quantity, show a live total like 'Total: 1000ml' updated in real time."*
- *"Do a full UX pass — find anything broken, unfinished, or confusing to a first-time user. Fix it."*
