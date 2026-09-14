# 🍽️ Random Lunch Menu Generator

Tired of deciding what to eat for lunch? This web app eliminates the daily dilemma by randomly generating a lunch idea for you! Say goodbye to endless scrolling and "I don't know, what do you want?" conversations.

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-222222?style=for-the-badge&logo=githubpages&logoColor=white)

## ✨ Features

*   **Randomized Selection:** Get a random lunch suggestion with a single click.
*   **No-Repeat Shuffle:** Draws come from a shuffled deck of all 12 meals, so you never get the same lunch on consecutive days, and every meal appears once per 12-pick cycle. (Pure uniform random would repeat a meal ~30 times a year — see the code comment in `index.html`.)
*   **Visual Appeal:** Each suggestion is paired with a Font Awesome 6.4.0 solid icon.
*   **Single File, Zero Build:** Everything — markup, CSS, and JS — lives inline in `index.html`. Open it and it works.
*   **Mobile-Friendly:** Responsive design that works on desktop, tablet, and phone.

## 🚀 Live Demo

Check out the live application on GitHub Pages:  
👉 **[LIVE DEMO](https://YuliaVodopyanova.github.io/LLM4Rec/week1/)** 👈


## 🛠️ How It Works

1.  The app embeds a 12-item menu (`lunchMenu` array in the inline script), each item paired with a Font Awesome 6.4.0 free-solid icon class loaded from the cdnjs CDN.
2.  On page load — and on every **Generate Lunch!** click — the inline JS draws the next meal **without replacement** from a freshly shuffled deck of all 12 items.
3.  When the deck is exhausted it reshuffles; a boundary guard ensures the first meal of a new deck is never the same as the last meal of the old deck.
4.  The remaining deck and last pick persist in `localStorage`, so the no-repeat guarantee holds across days, not just within one page session.

## 📁 Project Structure

This project is intentionally a **single file** — markup, styles, and logic are all inline:

```
random-lunch-generator/
├── index.html   # The entire app: HTML + inline CSS + inline JS (lunchMenu data + shuffle-bag picker)
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
3.  Use only Font Awesome 6.4.0 **free solid** icon classes — a class renders only if it exists in the loaded 6.4.0 CSS (free set has no pasta/noodle/dedicated-soup bowl glyphs, so pick a bowl/plate icon for those).
4.  Save and reload the page.

## 📝 License

This project is licensed under the MIT License — see `LICENSE` for details.

## 🙏 Acknowledgments

*   Icons by [Font Awesome](https://fontawesome.com/) (6.4.0, cdnjs).
*   The no-repeat/shuffle-bag idea follows [Spotify Engineering — "How to shuffle songs?"](https://engineering.atspotify.com/2014/02/how-to-shuffle-songs/) and the perceived-randomness literature (e.g., Tversky & Kahneman 1971; Bar-Hillel & Wagenaar 1991).
