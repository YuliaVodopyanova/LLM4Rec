# 🍽️ Random Lunch Menu Generator

Tired of deciding what to eat for lunch? This web app eliminates the daily dilemma by randomly generating a lunch idea for you! Say goodbye to endless scrolling and "I don't know, what do you want?" conversations.

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-222222?style=for-the-badge&logo=githubpages&logoColor=white)

## ✨ Features

*   **Randomized Selection:** Get a random lunch suggestion with a single click.
*   **No-Repeat Shuffle + Skip Sensing:** Consecutive picks are never the same meal (hard no-repeat). The picker is skip-sensing: clicking **Generate Lunch!** again while an item was shown for **under 750 ms** carries no dislike signal (such a click likely landed while the 500 ms spinner still hid the item), so nothing is demoted. A re-click after the item has been displayed for **750 ms or more** treats that meal as disliked: its weight ×0.5 (floored at 0.2) while all other meals slowly recover (×1.04 per pick, capped at 1.0). The old guarantee that "every meal appears once per 12-pick cycle" intentionally no longer holds.
*   **Visual Appeal:** Each suggestion is paired with a Font Awesome 6.4.0 solid icon.
*   **Single File, Zero Build:** Everything — markup, CSS, and JS — lives inline in `index.html`. Open it and it works.
*   **Mobile-Friendly:** Responsive design that works on desktop, tablet, and phone.

## 🚀 Live Demo

Check out the live application on GitHub Pages:  
👉 **[LIVE DEMO](https://YuliaVodopyanova.github.io/LLM4Rec/week1/)** 👈


## 🛠️ How It Works

1.  The app embeds a 12-item menu (`lunchMenu` array in the inline script), each item paired with a Font Awesome 6.4.0 free-solid icon class loaded from the cdnjs CDN.
2.  On page load — and on every **Generate Lunch!** click — the inline JS draws the next meal by **weighted proportional sampling excluding the currently displayed meal** (hard no-repeat: a meal can never be picked twice in a row, no matter its weight).
3.  The decision between "this was a reject" vs "no signal" uses a **750 ms display-time threshold**: a re-click while the shown item has been visible for ≥750 ms demotes that meal (×0.5, floored at 0.2, so it is served rarer but never starved); a re-click within the first 750 ms fires too early to have seen the item — no demotion. Every pick, all other meals recover toward weight 1.0 (×1.04, capped).
4.  State (per-meal weights, last pick, display timestamp, pick count) persists in `localStorage` under the **`lunch-picker-state-v2`** key, so the behavior holds across days; the old v1 key (`lunch-picker-state-v1`) is ignored.

## 🧩 Icon accuracy — semantics and validity

Every icon class was checked two ways: (1) does it exist in the real Font Awesome 6.4.0 Free Solid file (not just assumed from the name), and (2) does it actually look like the food it represents. Where the free set has no exact glyph, the closest real alternative was used and is flagged below — nothing was invented.

| Food | Icon class | Exists in FA 6.4.0? | Matches the food? |
|---|---|---|---|
| Pizza | `fa-pizza-slice` | ✅ yes | ✅ exact |
| Sushi | `fa-fish` | ✅ yes | ⚠️ closest available (no sushi glyph exists) |
| Burger | `fa-hamburger` | ✅ yes | ✅ exact |
| Salad | `fa-leaf` | ✅ yes | ⚠️ closest available (greens, no salad-bowl glyph) |
| Tacos | `fa-hotdog` | ✅ yes | ⚠️ closest available (no taco glyph exists at all) |
| Ramen | `fa-bowl-rice` | ✅ yes | ⚠️ closest available (no noodle glyph exists) |
| Sandwich | `fa-bread-slice` | ✅ yes | ⚠️ closest available (no sandwich glyph exists) |
| Pasta | `fa-plate-wheat` | ✅ yes | ⚠️ closest available (no pasta glyph exists) |
| Curry | `fa-pepper-hot` | ✅ yes | ✅ good match (spiced dish) |
| Steak | `fa-cow` | ✅ yes | ✅ good match (beef; previous icon was a drumstick, i.e. poultry — wrong) |
| Soup | `fa-bowl-food` | ✅ yes | ✅ good match |
| BBQ | `fa-fire` | ✅ yes | ✅ good match |

## 📁 Project Structure

This project is intentionally a **single file** — markup, styles, and logic are all inline:

```
random-lunch-generator/
├── index.html   # The entire app: HTML + inline CSS + inline JS (lunchMenu data + weighted skip-sensing picker)
└── README.md    # This file
```

There is no separate `style.css`, `script.js`, or `assets/` folder — nothing to build, bundle, or configure.

## 🧩 Installation & Local Development

1.  Copy `index.html` anywhere on your machine.
2.  Open it directly in a browser (double-click; `file://` works fine). Optionally serve it locally: `python3 -m http.server 8000` then visit `http://localhost:8000`.
3.  That's it. No build process, no package manager, no dependencies beyond the Font Awesome CDN.

## 🎯 How to Use

1.  Open the app (live demo or `index.html` directly).
2.  Click **"Generate Lunch!"**.
3.  Watch a random lunch idea appear. Click again as often as you like — consecutive picks are never the same meal.

## 🤝 Contributing

Add or tweak meals by editing the `lunchMenu` array inside the inline `<script>` in `index.html`:

1.  Open `index.html` in any editor.
2.  Add a line like `{ name: "Your Meal", icon: "fas fa-utensils" },`.
3.  Use only Font Awesome 6.4.0 **free solid** icon classes — a class renders only if it exists in the loaded 6.4.0 CSS (free set has no pasta/noodle/dedicated-soup bowl glyphs, no dedicated taco glyph — use a street-food glyph like hotdog — and no dedicated steak glyph — use the cow glyph; pick a bowl/plate icon for soups/pasta).
4.  Save and reload the page.

## 📝 License

This project is licensed under the MIT License — see `LICENSE` for details.

## 🙏 Acknowledgments

*   Icons by [Font Awesome](https://fontawesome.com/) (6.4.0, cdnjs).
*   The no-repeat/shuffle-bag idea follows [Spotify Engineering — "How to shuffle songs?"](https://engineering.atspotify.com/2014/02/how-to-shuffle-songs/) and the perceived-randomness literature (e.g., Tversky & Kahneman 1971; Bar-Hillel & Wagenaar 1991).
