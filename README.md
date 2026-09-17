# WildPrison - Gang Optimization Tool v3.3 🚀

A professional calculator and tactical dashboard designed for **WildPrison** (Minecraft OP Prison) players. The application optimizes **Token Sacrifice** management, **Ascension** upgrade prioritization, and **Research** tree tracking.

The application is delivered as a static Single Page Application (SPA) built around `index.html` and two local image assets. It relies on Tailwind CSS and browser `LocalStorage`, and is hosted on GitHub Pages: https://anonbotpl.github.io/wildprison-calculator/

---

## ⚠️ CRITICAL SERVER RULES & MECHANICS

> **WARNING:** Decisions made within the **Ascension** and **Research** systems on the server are **PERMANENT (IRREVERSIBLE)**. Purchased research and spent Ascension points cannot be reset. A mistake will permanently impair account performance for the entire season!

---

## 🧠 MATHEMATICAL LOGIC & STRATEGY (OFFICER NOTES)

### 1. 💱 Currency System & Suffixes
All internal engine calculations normalize to the base unit **SP (Sacrifice Points)**. The calculator automatically converts the following currency suffixes:

| Currency | Name | SP Equivalent |
| :--- | :--- | :--- |
| **QT** | Quintillion | `0.000001 SP` |
| **S** | Sextillion | `0.001 SP` |
| **SP** | Septillion (Sacrifice Points) | `1.0 SP` (Base Unit) |
| **O** | Octillion | `1,000 SP` |
| **N** | Nonillion | `1,000,000 SP` |

*The calculator automatically parses direct input suffixes (e.g., `10O` or `5S`) and adjusts the currency dropdown accordingly.*

---

### 2. 💎 Token Sacrifice Engine (Updated Ratio Rules)
Sacrifice Points (SP) are calculated as the sum of sacrificed resources: $SP = Money + XP$. 

Optimal allocation ratio (**Money Goal vs XP Goal**) — the ratio switches only **after** you exceed a threshold:
* **Up to ~1 SP:** **1:1** Ratio (50% Money / 50% XP)
* **After 1 SP (up to 100 SP):** **3:1** Ratio (75% Money / 25% XP)
* **After 100 SP (up to 1,000 SP / 1 O):** **10:1** Ratio (~90.9% Money / ~9.1% XP)
* **Above 1,000 SP (1 O):** Switch to **1:3** Ratio (25% Money / 75% XP)

---

### 3. 🚀 Ascension Advisor (9-Phase Roadmap)
The advisor evaluates current stat allocations and identifies the lowest stat in the active phase to guide progression:

* **Phase 1 (Early Balance 0 ➔ 20):** Balance `Money`, `Pet XP`, and `Armor XP` to level 20.
* **Phase 2 (Mid Balance 20 ➔ 50):** Balance `Tokens`, `Pet XP`, and `Armor XP` to level 50.
* **Phase 3 (Money Boost 20 ➔ 30):** Upgrade `Money` from 20 to 30.
* **Phase 4 (XP Rush 50 ➔ 100):** Upgrade `Pet XP` and `Armor XP` in parallel to 100.
* **Phase 5 (Tokens Rush 50 ➔ 100):** Upgrade `Tokens` to 100 (optionally alongside `Enchant Chance`).
* **Phase 6 (Enchant Chance 0 ➔ 100):** Max out `Enchant Chance` to 100.
* **Phase 7 (Money Push 30 ➔ 50):** Push `Money` from 30 to 50.
* **Phase 8 (Late Tokens 100 ➔ 150+):** Continue scaling `Tokens` past 100/150.
* **Phase 9 (Max Money 50 ➔ 100):** Final push for `Money` from 50 to 100.

*Overall Ascension Progress* is calculated based on total points relative to the max cap (550 points).

---

### 4. 🔬 Research Order & Audit Score
The research module includes an account audit score engine (**Research Audit Score** - max 100%):

1. **Starter Projects:** Token Boost ➔ Money Boost ➔ All XP Boosts ➔ Nocturnal 1
2. **Sacrificial Rush:** Sacrificial Level 4 ➔ Sacrificial Level 5 (Max)
3. **Main Currency Boosts:** Nocturnal 2 & 3 ➔ Resonance ➔ Geology 1 ➔ Enchant Chance ➔ Synergy 1 & 2 ➔ Attachment Mastery
4. **Utilities:** Tamer 1 & 2 ➔ Knowledgeable 1 & 2 ➔ Sacrificial 2
5. **Fillers:** Luckier & Dual Offering ➔ Street Rep 1, Geology 2, Overtime
6. ⛔ **NEVER BUY / AVOID (Audit Penalties):**
   * `Chain Reaction` (Penalty: **-30%** Audit Score)
   * `Street Rep 2 & Fast Learner` (Penalty: **-20%** Audit Score)

---

## 📊 UPGRADE TIER LIST

* **Tier A (Must Have):** XP Boosts, Sacrificial, Enchant Chance
* **Tier B (Main Boosts):** Starter Currency Boosts, Nocturnal, Synergy, Resonance, Geology, Attach Mastery
* **Tier C (Utilities):** Tamer, Knowledgeable, Luckier, Dual Offering
* **Tier D (Niche / Weak):** Street Rep 1, Geology 2, Overtime, Fast Learner
* **Chain Reaction Tier (AVOID):** Chain Reaction, Street Rep 2

---

## 💻 TECHNICAL ARCHITECTURE & CODE

Everything runs in the browser — no build step, no server-side runtime, no Node.js. All markup, styles and logic live in `index.html`; the only additional files are two local image assets.

### Files:
| File | Purpose |
| :--- | :--- |
| `index.html` | The entire application — markup, styles and logic. |
| `background.webp` | Hero background image (1920×1012), loaded relatively. |
| `wild.webp` | WildNetwork logo displayed in the header. |

### Tech Stack:
* **HTML5 / Vanilla JavaScript (ES6+)**
* **Tailwind CSS (via CDN)**, plus a small inline `<style>` block for the custom scrollbars and the page background
* **LocalStorage API** (Key: `wildprison_optimizer_data`)
* **GitHub Pages** hosting (`main` branch, root folder)

### Core JS Functions:
* `parseAmountWithUnit(inputId, unitSelectId)` — Extracts values, parses inline suffixes/dropdowns, and converts to base SP.
* `normalizeNumberInput(rawNumber)` — Normalizes separators: comma or dot as a decimal separator (`1,5` → `1.5`) and repeated 3-digit groups as thousands separators (`1,000` / `1.000` → `1000`).
* `formatSpToBestUnit(spVal)` — Converts raw SP values into readable units (QT, S, SP, O, N).
* `calculateTokens()` — Calculates SP split targets (1:1, 3:1, 10:1, 1:1) and emits allocation guidance.
* `calculateAscension()` — Evaluates the active Ascension phase, progress percentage, and mini-bar UI.
* `updateResearch()` — Determines the next priority node and calculates the audit penalty score.
* `saveProgress()` / `loadProgress()` — Handles persistent storage for user data and currency selections in `LocalStorage`.
* `resetAllProgress()` — Clears stored data for new server seasons.

---

## 🎨 DESIGN & ASSETS

The interface deliberately mirrors the official server website so players feel at home:
* **Palette:** dark `zinc` surfaces with the server's brand gold `#FFAA00`.
* **The logo (`wild.webp`) and the background image (`background.webp`) are borrowed from the official server website** — [wildnetwork.net](https://wildnetwork.net/).
* Custom dark scrollbars are defined in an inline `<style>` block (`::-webkit-scrollbar` for Chrome/Edge/Safari, `scrollbar-color` for Firefox).
* The tier list intentionally keeps its own semantic colours (`emerald` / `sky` / `yellow` / `orange` / `red`) — those are not part of the brand palette.

---

## 🤖 AI HANDOVER BRIEFING

Hello! If you are an AI model continuing development on this project, adhere to these guidelines:

1. **Structure:** Keep the entire interface and logic inside `index.html`. The only permitted extra files are local image assets (`background.webp`, `wild.webp`), always referenced with relative paths so the tool works both from disk and on GitHub Pages.
2. **Persistence:** Ensure all input fields, currency selections, and checkboxes remain wired to `saveProgress()` and `loadProgress()`.
3. **Sacrifice Ratios** (thresholds are exclusive — the ratio changes only *after* you exceed them):
   * `<= 1 SP`: 1:1
   * `> 1 to 100 SP`: 3:1
   * `> 100 to 1,000 SP (1 O)`: 10:1
   * `> 1,000 SP (> 1 O)`: 1:3 (per officer instructions).
4. **Currency Multipliers:** Modify unit conversions exclusively inside the `CURRENCY_MULTIPLIERS` object.
5. **UI Aesthetics:** Preserve the WildNetwork look — `zinc` surfaces, the brand gold `#FFAA00` (written as `[#FFAA00]` classes) and `emerald-400` for positive states. Do not reintroduce the old `slate` / `amber` palette.
