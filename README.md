# WildPrison - Gang Optimization Tool v3.1 🚀

A professional calculator and tactical dashboard for players of the **WildPrison** server (Minecraft OP Prison). The application assists with the optimal management of **Token Sacrifice**, prioritizing **Ascension** upgrades, and tracking the **Research** tree.

The tool is provided as a Single Page Application (SPA) via an `index.html` file and runs using the Tailwind CSS framework and browser **LocalStorage**.

---

## ⚠️ CRITICAL SERVER RULES & MECHANICS

> **WARNING:** Decisions made within the **Ascension** and **Research** systems on the server are **PERMANENT (IRREVERSIBLE)**. There is no way to reset purchased research or spent Ascension points. A mistaken purchase reduces account efficiency for the entire season!

---

## 🧠 MATHEMATICAL LOGIC & STRATEGY (OFFICER NOTES)

### 1. 💎 Token Sacrifice Engine
The Sacrifice Points (SP) value is calculated as the sum of sacrificed resources: $SP = Money + XP$. Bonuses are subject to diminishing returns (Power of 10 Rules: 1 SP, 10 SP, 100 SP...). Optimal point allocation ratio (**Money Goal vs XP Goal**):
* **Below 1 SP:** **1:1** ratio (50% Money / 50% XP)
* **1 SP to 100 SP:** **3:1** ratio (75% Money / 25% XP)
* **Above 100 SP:** **10:1** ratio (~90.9% Money / ~9.1% XP)

### 2. 🚀 Ascension Advisor (9-Phase Roadmap)
The calculator analyzes the entered values ​​and identifies the lowest stat for the current phase to pinpoint the exact upgrade target:

* **Phase 1 (Early Balance 0 ➔ 20):** Balance `Money`, `Pet XP`, and `Armor XP` to level 20.
* **Phase 2 (Mid Balance 20 ➔ 50):** Balance `Tokens`, `Pet XP`, and `Armor XP` to level 50.
* **Phase 3 (Money Boost 20 ➔ 30):** Raise `Money` from level 20 to 30.
* **Phase 4 (XP Rush 50 ➔ 100):** Raise `Pet XP` and `Armor XP` simultaneously to level 100.
* **Phase 5 (Tokens Rush 50 ➔ 100):** Raise `Tokens` to level 100 (optionally including `Enchant Chance`). * **Phase 6 (Enchant Chance 0 ➔ 100):** Maxing out `Enchant Chance` at 100.
* **Phase 7 (Money Push 30 ➔ 50):** Boosting `Money` from 30 to 50.
* **Phase 8 (Late Tokens 100 ➔ 150+):** Further development of `Tokens` beyond 100/150.
* **Phase 9 (Max Money 50 ➔ 100):** Final push for `Money` from 50 to 100.

The *Overall Progress* indicator is based on the total sum of points relative to the maximum cap (550 points). ### 3. 🔬 Research Order & Audit Score
The research tree features a built-in account audit calculator (**Research Audit Score** - max 100%):

1. **Starter Projects:** Token Boost ➔ Money Boost ➔ All XP Boosts ➔ Nocturnal 1
2. **Sacrificial Rush:** Sacrificial Level 4 ➔ Sacrificial Level 5 (Max)
3. **Main Currency Boosts:** Nocturnal 2 & 3 ➔ Resonance ➔ Geology 1 ➔ Enchant Chance ➔ Synergy 1 & 2 ➔ Attachment Mastery
4. **Utilities:** Tamer 1 & 2 ➔ Knowledgeable 1 & 2 ➔ Sacrificial 2
5. **Fillers:** Luckier & Dual Offering ➔ Street Rep 1, Geology 2, Overtime
6. ⛔ **NEVER BUY / AVOID (Audit penalties):**
* `Chain Reaction` (Penalty: **-30%** to audit score)
* `Street Rep 2 & Fast Learner` (Penalty: **-20%** to audit score)

---

## 📊 UPGRADE TIER LIST

* **Tier A (Must Have):** XP Boosts, Sacrificial, Enchant Chance
* **Tier B (Main Boosts):** Starter Currency Boosts, Nocturnal, Synergy, Resonance, Geology, Attach Mastery
* **Tier C (Utilities):** Tamer, Knowledgeable, Luckier, Dual Offering
* **Tier D (Niche / Weak):** Street Rep 1, Geology 2, Overtime, Fast Learner
* **Chain Reaction Tier (AVOID):** Chain Reaction, Street Rep 2

---

## 💻 TECHNICAL ARCHITECTURE AND CODE

The project consists of a single `index.html` file. It does not require a Node.js server or compilers. ### Technology:
* **HTML5 / Vanilla JavaScript (ES6+)**
* **Tailwind CSS (via CDN)**
* **LocalStorage API** (Key: `wildprison_optimizer_data`)

### Key JS Functions:
* `calculateTokens()` — calculates SP ratios and generates allocation recommendations.
* `calculateAscension()` — computes the current phase, completion percentage, and mini-progress bar status.
* `updateResearch()` — determines the next research tree goal and recalculates the audit score.
* `saveProgress()` / `loadProgress()` — automatic saving and loading of state from `LocalStorage`.
* `resetAllProgress()` — clears data for a new server season.
